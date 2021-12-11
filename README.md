# m4port
Place to share information about configure/build of m4 for z/OS (only deltas to open source)

# pre-reqs
You need gmake, c99, and either manually upload the M4 tarball to your system or use curl/gunzip to do it automatically

# Build m4
```
. ./setenv.sh
./m4build.sh
```

This will generate the m4 executable in the 'src' sub-directory of the M4 tree

# Creating a new patch

If you need a new patch file, the following technique works:

- create a _new_ version of the file updated as required and give it a distinct name                         
- run _diff_ on the file and write the output to a patch file in the patches directory
- add code to the build script to apply the patch before building

For example, assume I want to change _src/builtin.c_ 
- create _src/builtin-new.c_
- cd into the _patches_ directory
- issue _diff -c ../*/src/builtin.c ../*/src/builtin-new.c_ >builtin.patch
- update _m4build.sh_ by looking for the _Apply Patches_ comment header and inserting a new patch statement

# Known issues

Only very basic testing has been done. Input m4 files need to be in a tagged ISO8859-1 file with auto-conversion on (see setenv.sh for expected settings)
