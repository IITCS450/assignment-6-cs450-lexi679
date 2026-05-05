Assignment 6 Results Write=Up

----------------------------------------------------------------------------------------

Workload: Update syscall number list, the user-level declaration, syscall stub, and syscall dispatch table. Kernel-side implementation added in sysfile.c as sys_symlink() which creates a new inode T_SYMLINK. It also write the target path string into the inode's data blocks using writei(). The string is storeed as NUL-terminated text to be read later and resolved. Path opening logic within sys_open() was changed so that if the opened inode is a symbolic link, xv6 reads the stpred target path from the inode and continues to liikup using namei(). This is repeated until a non-symlink inode is reached. Max resulution depth was set to 10 to prevent infinite loops.

----------------------------------------------------------------------------------------

Modified/Added files:
    Makefile
    fs.h
    stat.h
    syscall.h
    syscall.c
    sysfile.c
    testsymlink.c
    user.h
    usys.S
    
----------------------------------------------------------------------------------------

Testing: testsymlink.c added to create a file, write known contents to it, create a symbolic link to the file, and open symlink to verify the contents are read correctly. It attempts to read the first file (open() is expected to fail since symlink resolution depth limit is reached, confirming cycle detection works properly).

----------------------------------------------------------------------------------------

Results:

$ testsymlink
PASS: symlink created
PASS: read through symlink
PASS: loop detection (open failed)
testsymlink done