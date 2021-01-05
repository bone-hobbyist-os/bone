# Bone OS

This organization contains all the repositories for the Bone hobbyist operating system.

Bone is an operating system based on the concept of a microkernel. The kernel of Bone will have a reduced API set, and small interface. For performance reasons, we will not stick precisely to the microkernel paradigm though; daemons that are needed by most processes will live in the kernel memory space. Still, the address spaces will be distinct and only the Core will access them all.

Code organization in this repository:

* `/Arch` will contain architecture specific drivers and handlers. F.e. `/Arch/x86_32` will contain all the support specific to `x86_32` architecture.
* `/Arch/*/Drivers` will contain architecture specific drivers. Note that these drivers shall not cover processor functionality or build system quirks, but actual per-architecture hardware such as the VESA video card.
* `/Core` contains the core of the operating system. You shall not refer directly to any API in here.
* `/CoreKernel` contains the in-kernel interface to `Core`. Kernel drivers shall use this.
* `/CoreUser` contains the userspace interface to `Core`. Generic parts of system call implementation happen here.
* `/Drivers` will contain generic drivers that work on all architectures. No architecture specific code here, if it can be reasonably avoided.
* `/FS` will contain file system drivers for the core file systems. These file systems shall be unrestricted.
  * `/FS/Core` will contain core functionality common to all file systems, as well as the API itself.
  * `/FS/User` will contain functionality for implementing file systems in userspace, including API, plus some built in examples

Todo:

* [ ] Set up full repository, with initial source code files
* [ ] Come up with the full design of how code is organized (directories, files). Partial details above.
* [ ] Get a build system working, have a version that builds
* [ ] Get a version that boots to kernel mode and initializes all structures
* [ ] Get a version that boots to userspace, and can load kernel-hardcoded executables
* [ ] Add support for ramfs/tmpfs
* [ ] Add support for initramfs (so that the initial tools can read and write from the file system)
* [ ] Define a basic service API and initial system call API
