Portable Operating System Interface is a family of standards for maintaining compatibility between operating systems. It describes utilities, APIs, and services that a compliant OS should provide to software, thus making it easier to port programs from one system to another.

In relation to [[Linux]], while most Linux distributions are not officially POSIX-certified due to the cost of certification, they do adhere to the POSIX standards to varying degrees. This is because the Linux community values the interoperability that POSIX compliance offers [makeuseof.com](https://www.makeuseof.com/what-is-posix-how-it-relates-to-linux/). As such, Linux distributions such as Red Hat Enterprise Linux (RHEL) and Ubuntu are considered de facto standards in the Linux world [makeuseof.com](https://www.makeuseof.com/what-is-posix-how-it-relates-to-linux/).

In the case of Windows, Microsoft initially implemented the POSIX.1 standard in the first versions of Windows NT to meet US federal government requirements that certain types of government purchases be POSIX-compliant. However, this subsystem only covered the kernel and C library programming interfaces, not the interactive user environment parts of POSIX [en.wikipedia.org](https://en.wikipedia.org/wiki/Microsoft_POSIX_subsystem). The POSIX subsystem in Windows was later replaced by "Windows Services for UNIX" (SFU) in Windows XP and Windows Server 2003, and then by the Windows Subsystem for Linux (WSL) in the Windows 10 Anniversary Update and Windows Server 2016 Version 1709 [en.wikipedia.org](https://en.wikipedia.org/wiki/Microsoft_POSIX_subsystem).

According to [Ciro Santilli](https://unix.stackexchange.com/users/32558/ciro-santilli-ourbigbook-com) in [Unix Stack Schange](https://unix.stackexchange.com/questions/11983/what-exactly-is-posix/220877#220877), here are the big picture of POSIX:
**Most important things [POSIX 7](http://pubs.opengroup.org/onlinepubs/9699919799/nfindex.html) defines**

1. [C API](http://pubs.opengroup.org/onlinepubs/9699919799/functions/contents.html)
    
    Greatly [extends ANSI C](https://stackoverflow.com/questions/9376837/difference-bewteen-c-standard-library-and-c-posix-library/37969420#37969420) with things like:
    
    - more file operations: `mkdir`, `dirname`, `symlink`, `readlink`, `link` (hardlinks), [`poll()`](https://stackoverflow.com/questions/12444679/how-does-the-poll-c-linux-function-work/44127590#44127590), `stat`, `sync`, [`nftw()`](https://stackoverflow.com/questions/8436841/how-to-recursively-list-directories-in-c-on-linux/29402705)
    - process and threads: `fork`, `execl`, [`wait`](https://stackoverflow.com/questions/7248031/meaning-of-dollar-question-mark-in-shell-scripts/57303942#57303942), `pipe`, semaphors [`sem_*`](https://stackoverflow.com/questions/16400820/how-to-use-posix-semaphores-on-forked-processes-in-c/52042490#52042490), shared memory (`shm_*`), `kill`, scheduling parameters (`nice`, `sched_*`), `sleep`, `mkfifo`, [`setpgid()`](https://stackoverflow.com/questions/6108953/how-does-ctrl-c-terminate-a-child-process/52042970#52042970)
    - networking: [`socket()`](https://stackoverflow.com/questions/11208299/how-to-make-an-http-get-request-in-c-without-libcurl/35680609#35680609)
    - memory management: `mmap`, `mlock`, `mprotect`, `madvise`, [`brk()`](https://stackoverflow.com/questions/6988487/what-does-the-brk-system-call-do/31082353#31082353)
    - utilities: regular expressions (`reg*`)
    
    Those APIs also determine underlying system concepts on which they depend, e.g. `fork` requires a concept of a process.
    
    Many [Linux system calls](https://unix.stackexchange.com/questions/421750/where-do-you-find-the-syscall-table-for-linux) exist to implement a specific POSIX C API function and make Linux compliant, e.g. `sys_write`, `sys_read`, ... Many of those syscalls also have Linux-specific extensions however.
    
    Major Linux desktop implementation: glibc, which in many cases just provides a shallow wrapper to system calls.
    
2. [CLI utilities](http://pubs.opengroup.org/onlinepubs/9699919799/utilities/contents.html)
    
    E.g.: `cd`, `ls`, `echo`, ...
    
    Many utilities are direct shell front ends for a corresponding C API function, e.g. `mkdir`.
    
    Major Linux desktop implementation: GNU Coreutils for the small ones, separate GNU projects for the big ones: `sed`, `grep`, `awk`, ... Some CLI utilities are implemented by Bash [as built-ins](https://unix.stackexchange.com/questions/11454/what-is-the-difference-between-a-builtin-command-and-one-that-is-not).
    
3. [Shell language](http://pubs.opengroup.org/onlinepubs/9699919799/utilities/V3_chap02.html#tag_18)
    
    E.g., `a=b; echo "$a"`
    
    Major Linux desktop implementation: [GNU Bash](https://en.wikipedia.org/wiki/Bash_(Unix_shell)).
    
4. [Environment variables](http://pubs.opengroup.org/onlinepubs/9699919799/basedefs/V1_chap08.html#tag_08)
    
    E.g.: `HOME`, `PATH`.
    
    `PATH` [search semantics are specified](http://pubs.opengroup.org/onlinepubs/9699919799/utilities/V3_chap02.html#tag_18_09_01_01), including [how slashes prevent `PATH` search](https://stackoverflow.com/questions/6331075/why-do-you-need-dot-slash-before-executable-or-script-name-to-run-it-in-bas/6331085#6331085).
    
5. [Program exit status](http://pubs.opengroup.org/onlinepubs/9699919799/utilities/V3_chap02.html#tag_18_08)
    
    ANSI C says `0` or `EXIT_SUCCESS` for success, `EXIT_FAILURE` for failure, and leaves the rest implementation defined.
    
    POSIX adds:
    
    - `126`: command found but not executable.
        
    - `127`: command not found.
        
    - `> 128`: terminated by a signal.
        
        But POSIX does not seem to specify the `128 + SIGNAL_ID` rule used by Bash: [Default exit code when process is terminated?](https://unix.stackexchange.com/questions/99112/default-exit-code-when-process-is-terminated)
        
    
    See also: [What is the meaning of `$?` (dollar question mark) in shell scripts?](https://stackoverflow.com/questions/7248031/meaning-of-dollar-question-mark-in-shell-scripts/57303942#57303942)
    
6. [Regular expression](http://pubs.opengroup.org/onlinepubs/9699919799/basedefs/V1_chap09.html#tag_09)
    
    There are two types: BRE (Basic) and ERE (Extended). Basic is deprecated and only kept to not break APIs.
    
    Those are implemented by C API functions, and used throughout CLI utilities, e.g. `grep` accepts BREs by default, and EREs with `-E`.
    
    E.g.: `echo 'a.1' | grep -E 'a.[[:digit:]]'`
    
    Major Linux implementation: glibc implements the functions under [regex.h](http://pubs.opengroup.org/onlinepubs/9699919799/basedefs/regex.h.html) which programs like `grep` can use as backend.
    
7. [Directory struture](http://pubs.opengroup.org/onlinepubs/9699919799/basedefs/V1_chap10.html#tag_10)
    
    E.g.: `/dev/null`, `/tmp`
    
    The Linux [FHS](https://en.wikipedia.org/wiki/Filesystem_Hierarchy_Standard) greatly extends POSIX.
    
8. [Filenames](http://pubs.opengroup.org/onlinepubs/9699919799/basedefs/V1_chap03.html#tag_03_267)
    
    - `/` is the path separator
    - `NUL` cannot be used
    - `.` is `cwd`, `..` parent
    - portable filenames
        - use at most max 14 chars and 256 for the full path
        - can only contain: `a-zA-Z0-9._-`
    
    See also: [https://stackoverflow.com/questions/18550253/what-is-posix-compliance-for-filesystem](https://stackoverflow.com/questions/18550253/what-is-posix-compliance-for-filesystem)
    
9. [Command line utility API conventions](http://pubs.opengroup.org/onlinepubs/9699919799/basedefs/V1_chap12.html)
    
    Not mandatory, used by POSIX, but almost nowhere else, notably not in GNU. But true, it is too restrictive, e.g. single letter flags only (e.g. `-a`), no double hyphen long versions (e.g. `--all`).
    
    A few widely used conventions:
    
    - `-` means stdin where a file is expected
    - `--` terminates flags, e.g. `ls -- -l` to list a directory named `-l`
    
    See also: [https://stackoverflow.com/questions/8957222/are-there-standards-for-linux-command-line-switches-and-arguments](https://stackoverflow.com/questions/8957222/are-there-standards-for-linux-command-line-switches-and-arguments)
    
10. "POSIX ACLs" (Access Control Lists), e.g. as used as backend for [`setfacl`](https://askubuntu.com/questions/487527/give-specific-user-permission-to-write-to-a-folder-using-w-notation/809562#809562).
    
    This [was withdrawn](https://unix.stackexchange.com/questions/489820/why-was-posix-1e-withdrawn) but it was implemented in several OSes, including [in Linux with `setxattr`](https://www.linuxquestions.org/questions/linux-kernel-70/system-call-to-set-file-acls-in-linux-537615/#post5988355).
    

**Who conforms to POSIX?**

Many systems follow POSIX closely, but few are actually certified by the Open Group which maintains the standard. Notable certified ones include:

- OS X (Apple) X stands for both 10 and [[UNIX]]. Was the first Apple POSIX system, released circa 2001. See also: [https://stackoverflow.com/questions/5785516/is-osx-a-posix-os](https://stackoverflow.com/questions/5785516/is-osx-a-posix-os)
- AIX (IBM)
- HP-UX (HP)
- Solaris (Oracle)

Most Linux distros are very compliant, but not certified because they don't want to pay the compliance check. [Inspur's K-UX](https://en.wikipedia.org/wiki/Inspur_K-UX) and [Huawei's EulerOS](https://www.huawei.com/en/press-events/news/2016/9/huawei-kunlun-euleros-unix-certification) are two certified examples.

The official list of certified systems be found at: [https://www.opengroup.org/openbrand/register/](https://www.opengroup.org/openbrand/register/) and also at the [wiki page](https://en.wikipedia.org/wiki/POSIX#POSIX-oriented_operating_systems).

**[[Windows]]**

Windows implemented POSIX on some of its professional distributions.

Since it was an optional feature, programmers could not rely on it for most end user applications.

Support was deprecated in Windows 8:

- [https://stackoverflow.com/questions/4746043/where-does-microsoft-windows-7-posix-implementation-currently-stand](https://stackoverflow.com/questions/4746043/where-does-microsoft-windows-7-posix-implementation-currently-stand)
- [https://superuser.com/questions/495360/does-windows-8-still-implement-posix](https://superuser.com/questions/495360/does-windows-8-still-implement-posix)
- Feature request: [https://windows.uservoice.com/forums/265757-windows-feature-suggestions/suggestions/6573649-full-posix-support](https://windows.uservoice.com/forums/265757-windows-feature-suggestions/suggestions/6573649-full-posix-support)

In 2016 a new official Linux-like API called "Windows Subsystem for Linux" was announced. It includes Linux system calls, ELF running, parts of the `/proc` filesystem, Bash, GCC, (TODO likely glibc?), `apt-get` and more: [https://channel9.msdn.com/Events/Build/2016/P488](https://channel9.msdn.com/Events/Build/2016/P488) so I believe that it will allow Windows to run much, if not all, of POSIX. However, it is focused on developers / deployment instead of end users. In particular, there were no plans to allow access to the Windows GUI.

Historical overview of the official Microsoft POSIX compatibility: [http://brianreiter.org/2010/08/24/the-sad-history-of-the-microsoft-posix-subsystem/](http://brianreiter.org/2010/08/24/the-sad-history-of-the-microsoft-posix-subsystem/)

[Cygwin](http://www.cygwin.com/) is a well known GPL third-party project for that "provides substantial POSIX API functionality" for Windows, but requires that you "rebuild your application from source if you want it to run on Windows". [MSYS2](https://sourceforge.net/projects/msys2/) is a related project that seems to add more functionality on top of Cygwin.

**Android**

Android has its own C library (Bionic) which does not fully support POSIX as of Android O: [https://stackoverflow.com/questions/27604455/is-android-posix-compatible](https://stackoverflow.com/questions/27604455/is-android-posix-compatible)

**Bonus level**

The [Linux Standard Base](https://en.wikipedia.org/wiki/Linux_Standard_Base) further extends POSIX.

Use the non-frames indexes, they are much more readable and searchable: [http://pubs.opengroup.org/onlinepubs/9699919799/nfindex.html](http://pubs.opengroup.org/onlinepubs/9699919799/nfindex.html)

Get a full zipped version of the HTML pages for grepping: [https://stackoverflow.com/questions/453993/is-there-a-listing-of-the-posix-api-functions/45832939#45832939](https://stackoverflow.com/questions/453993/is-there-a-listing-of-the-posix-api-functions/45832939#45832939)