---
title: "Compiling Native Node Addons on OS X 10.9"
date: 2014-08-28T18:00:00-04:00
toc: true
type: "article"
---

Recently I was working on building some native Node.js addons on OS X 10.9 and I kept running into a weird runtime issue. Everytime I invoked methods that should have existed in the native module, I got errors related to dynamic linking:

```
dyld: lazy symbol binding failed: Symbol not found:
__ZN3cln14print_rationalERSoRKNS_14cl_print_flagsERKNS_5cl_RAE
  Referenced from:
/Users/aaustin/code/question/node_modules/jinac/build/Release/rationalnumber.node
  Expected in: dynamic lookup
```

Not having any experience with C++ this issue puzzled me quite a bit. You see, the addon worked wonderfully on linux.  It was time to dive in.

The first thing to determine is what the heck the symbol ```_ZN3cln14print_rationalERSoRKNS_14cl_print_flagsERKNS_5cl_RAE``` resolves too. Luckily, there is a nice tool for this called ```c++filt``` which will display the unmangled output:

```
*cln::print_rational(std::ostream&, cln::cl_print_flags const&, cln::cl_RA const&)*
```

This is one of the symbol's exported by the library CLN that I expect to be there. So maybe there is a link error with the shared libraries?

Since I'm a linux guy and I've done some C development in the past I knew ```ldd``` would give me a list of the shared libraries.

```
andrew@yoda:~/code/go/bin$ ldd go-example
	linux-vdso.so.1 =>  (0x00007fff5a3fe000)
	libpthread.so.0 => /lib/x86_64-linux-gnu/libpthread.so.0 (0x00007f4d710c2000)
	libc.so.6 => /lib/x86_64-linux-gnu/libc.so.6 (0x00007f4d70cfc000)
	/lib64/ld-linux-x86-64.so.2 (0x00007f4d712fb000)
```

Unfortunately, running ```ldd``` on OS X results in command not found. As it turns out, OS X has its own tool, ```otool```. To list the shared libaries with ```otool``` you supply the argument ```-L```.

```
otool -L rationalnumber.node
 rationalnumber.node:
 /usr/local/lib/libcln.6.dylib (compatibility version 7.0.0, current  version (7.3.0)
 /usr/lib/libstdc++.6.dylib (compatibility version 7.0.0, current version  60.0.0)
 /usr/lib/libSystem.B.dylib (compatibility version 1.0.0, current version  (1197.1.1)
 /usr/lib/libgcc_s.1.dylib (compatibility version 1.0.0, current version ( 2577.0.0)
```

Okay, so the CLN shared library looks to be properly linked (my addon is linked to ```libcln.6.dylib``` which is the CLN library). Since I had installed CLN using homebrew, I suspected the version of CLN I was not exporting that symbol either because it was too new or too old. To confirm this I download CLN myself and grepped through the code looking for that signature.

I found the signature. Next, I thought that perhaps homebrew was building the shared library incorrectly. I built it. It wasn't. I still had the exact same issue as when it was built with homebrew. At this point I was thinking it might be an issue with CLN somehow, so I sent an email to the CLN mailing list.

I never got a response. At this point I gave up and just started developing on a linux vm.

But leaving the issue unresolved kept bothering me and soon I was back at it. One thing I had noticed when I was investigating before was that the code worked on OS X 10.8.5 but was failing on OS X 10.9.3, so I eventually took the time to compare the two compilier versions:

10.8.5:
```
g++ --version
> i686-apple-darwin11-llvm-g++-4.2 (GCC) 4.2.1 (Based on Apple Inc. build
> 5658) (LLVM build 2336.11.00)
```

10.9.3:
```
g++ --version
Configured with: --prefix=/Applications/Xcode.app/Contents/Developer//usr
--with-gxx-include-dir=/usr/include/c++/4.2.1
 Apple LLVM version 5.1 (clang-503.0.40) (based on LLVM 3.4svn)
 Target: x86_64-apple-darwin13.2.0
 Thread model: posix
```

Obviously, it seems like something important changed. (One thing that still isn't clear is why the 10.8.5 version has ```(GCC)``` in the name when it also says llvm.)

So I kept googling and finally found out that Apple changed the standard library from 10.8, where it is ```libstdC++```, and 10.9, where it is ```libC++```.

As it turns out, running ```otool -L``` on CLN indicated that CLN was linked with ```libC++```:

```
otool -L /usr/local/lib/libcln.6.dylib
/usr/local/lib/libcln.6.dylib:
/usr/local/lib/libcln.6.dylib (compatibility version 7.0.0, current version 7.3.0)
/usr/local/lib/libgmp.10.dylib (compatibility version 13.0.0, current version 13.0.0)
/usr/lib/libc++.1.dylib (compatibility version 1.0.0, current version 120.0.0)
/usr/lib/libSystem.B.dylib (compatibility version 1.0.0, current version 1197.1.1)
```

Apparently ```libstdc++``` and ```libc++``` mangle names differently. Since CLN's symbols were mangled in a different scheme, the names could not resolve properly. I'd found my bug.

So why was the above tool linking to ```libstdc++.6.dylib``` instead of ```libc++.1.dylib```?

It turns out this is a bug in node-gyp. I couldn't figure out a fix though, and I didn't want to waste any more time trying to fix an issue that could be more easily solved by somebody with C++ and node-gyp experience. So I [filed a bug](https://github.com/TooTallNate/node-gyp/issues/469) .

And almost a month and a half went by without a response. Its never a good sign for an open source project when a bug filed isn't triaged by the maintainers after a month (especially on github). At least respond and call me an idiot and close the ticket as WONTFIX. A lack of any response almost always indicates that the project is dead. What confused me about the lack of response is that node-gyp is still [**the** solution for developing native addons for node](http://nodejs.org/api/addons.html).

Luckily, another developer, [Dane Springmeyer](https://github.com/springmeyer), who  ran into this issue over a year ago, posted [a workaround](https://github.com/mapnik/node-mapnik/blob/e0041df852720f389ed6a4bd2e761f989d6368c1/common.gypi#L2-L14) after a month of no responses. He identified the issue as node-gyp incorrectly setting ```MACOSX_DEPLOYMENT_TARGET``` to 10.5. His workaround is conceptually simple. Detect if we are running on 10.9, and if so, tell gyp to set the ```MACOSX_DEPLOYMENT_TARGET``` to 10.9. Unfortunately, gyp doesn't have the ability to do this itself, so the complexity of the workaround is increased because of its reliance on python.

At least his workaround fixes my bug.

At one point I was motivated to write Node.js addons.  No longer. I'm not sure what it says about the Node.js platform when their official native addon tool is almost completely dead on github.
