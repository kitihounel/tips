# masOS

- [A (not so) brief history of Darwin](#a-not-so-brief-history-of-darwin)

## A (not so) brief history of Darwin

**Note**: the following comes from a [thread](https://apple.stackexchange.com/questions/401832/why-is-macos-often-referred-to-as-darwin)
on why macOS is referred to as Darwin.

The history of macOS is long, convoluted, and complicated.

It starts with Steve Jobs (not entirely voluntary) "leaving" Apple and founding NeXT. NeXT wanted to revolutionize
the Personal Workstation. They built both a powerful computer, the NeXT Computer (later NeXTstation and NeXTcube),
and a powerful, modern Operating System, called NeXTStep. (Get it? The next step for the next computer. Really creative naming.)

The Operating System was based on porting BSD to a Mach microkernel, and adding object-oriented system libraries,
frameworks, and toolkits (called "kits", which you can still see in Apple's naming today), with an object-oriented
GUI framework and desktop, with object-oriented applications, all written in a modern object-oriented programming
language (Objective-C) as the systems language, on top of the base BSD system. The display system was based on PostScript,
and there was even an Intel i860 coprocessor running a stripped-down version of the OS, only for Display PostScript processing,
plus a powerful DSP for video and audio processing.

NeXTStep pioneered many things we see in modern GUI programming. It had one of the first graphical GUI Builders,
which still to this day is how you design GUIs for macOS, iOS, iPadOS, etc. (Today, it is called the Xcode Interface Builder.)
It had the first ever App Store. When Tim Berners-Lee invented the World Wide Web, he chose NeXTStep as the OS to write
the first browser for. Many game studios used NeXTStep and NeXT workstations for their development, e.g. id software for Doom,
Doom 2, and Quake. Lotus Improv, still considered by many to be miles ahead of Excel even now, was implemented on NeXTStep.

Later, NeXT divorced the higher-level frameworks from the underlying OS and made them available under the name OpenStep for Windows NT,
Sun Solaris, and under the name "OPENSTEP for Mach" still based on the same underpinnings as the original NeXTStep.

At this point, Apple had tried and failed multiple times to modernize MacOS, and they bought NeXT (thus bringing Steve Jobs back
into the company) and all of its Intellectual Property and technology to develop a successor to MacOS based on OPENSTEP for Mach.
They modernized the Mach kernel from 2.5 to 3 and extended it with concepts from the FreeBSD kernel to form a kernel known as xnu
(a reference to the failed nuKernel project at Apple which was to develop a "new kernel"), and the BSD underpinnings from 4.3BSD
to 4.4BSD and later FreeBSD.

Most importantly, they extended and expanded the OpenStep APIs and built new APIs on top. The collection of those APIs is known as
"Cocoa". They also built an API called "Carbon", which was a close, but not identical re-implementation of a subset of the MacOS API
on top of the new foundations. (The intention was that while it would not be possible to simply re-compile existing MacOS applications,
it should be fairly easy to port them to Carbon, and then over the years rewrite them in Cocoa.)

The first prototype of this system was called Rhapsody. The full system wasn't finished in time, so a subset was released
as MacOS X Server 1.0. And the rest is history: Rhapsody became MacOS X, then OS X, then macOS, and somewhere along the way,
iOS was split off, and then further divided into iOS, iPadOS, tvOS, and watchOS.

Now, back to Darwin: Darwin is basically the underpinnings of macOS, from the xnu kernel, IOKit, drivers, etc. up to the
BSD libraries and userland, plus some macOS-specific developments such as mDNSresponder and launchd. It does not, however,
include any parts of what used to be OpenStep, Cocoa, Aqua, Quartz, QuickTime, or any of the other higher-level stuff.
It does contain drivers and filesystems, although I am not entirely sure whether APFS is part of Darwin.

If you think back to the point in time where NeXT "divorced" the high-level OpenStep from its underpinnings, the low-level parts
that are not OpenStep would be the ones that would later become Darwin.

In the beginning, Apple used to make Darwin available as a separate OS, including compiled binaries, installers, ISOs, etc.
that you could install on Apple hardware. However, for many years now, Apple only provides a source code dump, every time
a new release of macOS comes out. It isn't even possible to compile this source code, because it depends on Apple's internal
build tools and build pipeline. There have been some projects trying to patch Darwin to compile it with publicly available tools,
but those projects have all died from lack of interest.

Since all of the things you mentioned were born on Unix and use Unix APIs and Unix libraries, they actually typically don't
even know about the "non-Darwin" parts of macOS, so it is only logical that they will consider the OS to be "Darwin".
Note that "Darwin" is also what gets returned as the name of the OS when you call the Unix/POSIX `int uname(struct utsname *buf)`
library function or the `uname` Unix/POSIX commandline utility.

So, to answer the question you didn't ask explicitly but is implicit in your question: why does Node.js return "Darwin" for the
name of macOS? Because when Node.js asks macOS for its name, that's what macOS tells it its name is!

**Source**: [SO](https://apple.stackexchange.com/a/401881)
