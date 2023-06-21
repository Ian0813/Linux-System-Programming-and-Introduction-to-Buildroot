**Learning objectives**

 * Git submodules
 * Overview of Buoldroot Example Project


**Git submodules**

 * Add a git repository as a subdirectory
   of another repository

 * Keep two projects separate but reference one fron the other.

  * Keep your project specific changes out of a shared project  

 * We will use buildroot as a submodule for Assignment 4.

 * Your assignment 4 repository will contain buildroot as a submodule

 * @ XXXX references a specific commit hash corresponding to release specified in the assignment


**Buildroot Git Submodule**

 * Add as a submodule in the root using *git submodule add <buildroot-repo-url>* 

 * Check out the branch corresponding to the release referenced in the assignment 

**Example/Starter Code Overview**

 * See the buildroot-assignments-base repository for starter code 

   - https://github.com/cu-ecen-5013/buildroot-assignments-base 

 * See working hello-world example at

   - https://github.com/cu-ecen-5013/buildroot-external/tree/ecen5013-hello-world 

**aesd-assignments.mk file setup**

 * $(eval $(generic-package))

  * Cross compiles package for the target

  * Knows how to use LIBFOO_XXXX variables
    where LIBFOO is replaced with your package     name. See the manual for variable details. [3]_ 

  * $(INSTALL) maps to the install utility - see https://linux.die.net/manual/1/install


**Setting up base external**

 * Add base_external/Config.in,
   base/external/external.mk, and
   base_external/external.desc files to allow you to use package directories outside buildroot

 * Use project_base as your external name in external.desc

  * See buildroot link below for details

   * https://buildroot.org/downloads/manual/manual.html#outside-br-custom

  * See also example ecen5013-hello-world implementation

**Setting up aesd-assignments**

 * aesd-assignments.mk needs to reference your assignment 3 repository:

  * Reference the ssh repository URL to work properly with the autograder.

  * Needs to represent a specific commit to build.

 * It also needs to complete installation of scripts in the /bin directory 

 * See link below for template

   - https://github.com/cu-ecen-aeld/buildroot-assignments-base/blob/master/base_external/package/aesd-assignments/aesd-assignments.mk

**build.sh template**

 * See build script linked below

 * This script

  * Handles git submodule initialization/update 
  * Ensures .config file exists, using 

   * Project specific config if it exists OR

   * qemu_aarch64_virt_defconfig as fallback from buildroot 

**Initial Build**

 * After setting up base_external and aesd-assignments, run ./build.sh first time 

  * This creates your modified QEMU defconfig file

**Saving Configuration - 1**

 * Then run ./save_config.sh as instructed by the build script

 * You should see a new configuration file at /base_external/configs/aesd_qemu_defconfig 

**Adding your package**

 * You should see your package after running make menuconfig in the buildroot directory

 * Select the package and then run ./build.sh

 * Use save_configs.sh to save your configuration with the project external tree

   * Your coworkers(SAs) will need to delete their buildroot/.config file, then run ./build.sh to pick up config changes.

**Saving Configuration - 2**

 * Run ./save_config.sh again 

 * You should see your buildroot config at base_external/configs/aesd_qemu_defconfig to include the aesd-assignments package (BR2_PACKAGE_AESD_ASSIGNMENTS=y)

**Adding your new package**  

 * Now you ready to build your image with your custom package

  * Use ./build.sh

  * Or use make from the buildroot directory

  * Or use make aesd-assignments from the buildroot directory

**Rederence**

 * buildroot needed files.

   - https://github.com/cu-ecen-aeld/buildroot-assignments-base/tree/master/base_external/package/aesd-assignments

 * Building with Buildroot

   - https://buildroot.org/downloads/manual/manual.html#generic-package-tutorial

 * Buildroot generic package

   .. [3] https://buildroot.org/downloads/manual/manual.html#generic-package-reference

 * build.sh template 

   - https://github.com/cu-ecen-aeld/buildroot-assignments-base/blob/master/build.sh 

 * make-tips 

   - https://buildroot.org/downloads/manual/manual.html#make-tips
