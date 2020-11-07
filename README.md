# CI system for the Gentoo Portage tree
If you are visiting this page, it is very likely that the software you maintain has been analyzed by my tinderbox system.

What is a tinderbox?  
It is a machine that compiles 24/7 that aims to find build failures, test failures, QA issues and so on in the portage tree.  
It can be differentiated into:  

– **tinderbox**  
– **ci**  


### TINDERBOX:
It compiles the entire portage tree against a particular change like:  
– a new version of compiler/libc/linker  
– a new C/CXX/LD FLAG  
– a different toolchain like clang/llvm/lld  
– and so on  

In short it uses uncommon but supported settings and looks for breakage.  

### CI:
It is a continuous integration; the CI system compiles the packages after they have been touched in gentoo.git  

The CI system uses a standard set of settings, so if you get a bug report from it, it is very likely that the failure is reproducible for users too.  


What are the rules that you may know when you see a report from those systems?  
1) The reports are filed automatically.  
2) Because of the first, it is not possible for me to set an exact error in the bug summary. Instead a general error is used.  
3) Because of the above, maintainer is encouraged to set an appropriate summary at its convenience  
4) Common additional logs (like test-suite.log testlog.txt CMakeOutput.log CMakeError.log LastTest.log config.log testsuite.log autoconf.out) are automatically attached but before of the first if you need something else please ask for them.  
5) If you ask for another log, I have to stop the tinderbox service, so there may be a delay between your request and my reaction.  
6) There may be an internal reference between round brackets on the “Discovered on” line. This is for me to understand where that failure was reproduced.  
7) If you see ‘ci’ as internal reference after you pushed a fix, it is very probably that the bug still exist, or there is another failure in the same ebuild phase. Please inspect deeply the build log. Point 8 may help you about that.  
8) At the beginning of the build log a git SHA of the repository at the time of emerging is provided. For convenience there is a link.  
9) To avoid making a separate attachment on bugzilla, at the beginning of the build log there is the ’emerge –info’, please check it DEEPLY to understand the system configuration and what differs respect to a more ‘standard’ system.  
10) If you see a compressed build log, is because the plain text version exceeds the limits on our bugzilla (1MB).  
11) This system is not perfect. There may be duplicates or invalid bugs.  
12) My best suggestion is try to reproduce the issue on empty stage3 (or docker for convenience).  
13) When you close the bug with a resolution different from RESOLVED/FIXED please not be cryptic.  
14) If new points will be added, there may be a mention like “Valid from YY:MM:DD”  


## The CI system produces a bugreport in case:  

* A package calls ar directly
* A package calls as directly
* A package calls cc directly
* A package calls commands that do not exist
* A package calls cpp directly
* A package calls g++ directly
* A package calls ld directly
* A package calls nm directly
* A package calls objcopy directly
* A package calls objdump directly
* A package calls ranlib directly
* A package calls readelf directly
* A package calls size directly
* A package calls strings directly
* A package calls strip directly
* A package collides with other packages
* A package compiles in src_install phase
* A package does not respect CFLAGS
* A package does not respect LDFLAGS
* A package fails tests
* A package fails tests (hang)
* A package fails to compile
* A package fails to compile if CPP is set to CC -E
* A package fails to compile with -fno-common
* A package fails to link with LLD because of /usr/lib in the link command line
* A package has a configure.in file which has long been deprecated
* A package has unrecognized configure options
* A package installs broken png files
* A package installs colliding files (found by ecompress)
* A package installs compressed files (manpages, documentation)
* A package installs .desktop files that do not pass validation
* A package installs .desktop files with MimeType but does not update desktop mimeinfo cache
* A package installs files into unexpected paths
* A package installs files that contain a TEXTREL
* A package installs files that contain insecure RUNPATHs
* A package installs files that contain writable and executable sections
* A package installs files with broken symlink
* A package installs files with name not encoded with UTF-8
* A package installs files with unresolved SONAME dependencies
* A package installs icons but does not update icon cache
* A package installs into paths that should be created at runtime
* A package installs metainfo files into /usr/share/appdata
* A package installs mime-info files but does not update mime-info cache
* A package installs modules that are not byte-compiled
* A package installs pkg-config files with wrong LDFLAGS
* A package installs pre-stripped files
* A package installs shared libraries that lack a SONAME
* A package installs shared libraries that lack NEEDED entries
* A package installs static libraries without IUSE static-libs
* A package installs udev rules into wrong directory
* A package uses automake in maintainer-mode
* A package uses LD instead of CC/CXX
* A package uses -Werror CFLAGS
