**Learning objectives**

 * General buildroot debug strategies Assignment 4 

**Builldroot issues**

 * Don't check binaries to keep them out 

   - Use .gitignore to keep them out

 * Don't hard-code gcc references in your makefile (use $(CC) $(CFLAGS) $(INCLUDE) -o $(TARGET) $(LDFLAGS) in your writer compile step) 

 * Pay attention to configuration changes, output of save_config.sh 

**General Buildroot Debug Strategies**

  * Create errors in files (.mk, Config.in) 

   * Determines whether the file is actually being included in the build

  * Try incremental builds first 

   * from buildroot subdirectory: make AESD_ASSIGNMENTS_OVERRIDE_SRCDIR=/path/to/local/sourcedir aesd-assignments-rebuild

  * Use clean build as a last resort

**General Buildroot Debug**

 * Specify DL_DIR to avoid download steps

  * You can share your DL_DIR with others.

 * Examine every character (includeing spaces/tabs) 

  * Look at working example side by side

 * Think of other ways to test implementation 

  * Native compile is one option  

**General Buildroot Debug Strategies - Important**

  * Prioritize long delay tasks like build system setup over programming tasks

  * Think about things you can do in parallel 

  * Step away from the problem for a few hours and come back to it 

**Reference**

 * git ignore files 

   - https://docs.github.com/en/get-started/getting-started-with-git/ignoring-files
