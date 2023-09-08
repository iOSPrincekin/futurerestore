# Compiling Futurerestore

# Required/Optional Dependencies
* ## External libs
  Make sure these are installed
    * [curl](https://github.com/curl/curl) (Linux/Windows only, macOS already has curl preinstalled);
    * [openssl 3.0.3](https://github.com/openssl/openssl) (or CommonCrypto on macOS);
    * [libusb 1.0.25](https://github.com/libusb/libusb) (Linux/Windows only, macOS can use IOKit for libirecovery);
    * [libzip](https://github.com/nih-at/libzip);
    * [libplist](https://github.com/libimobiledevice/libplist) (commit 2d8d7ef272db06783989f77ba1ed80aa0f4d2dfd);
    * [libusbmuxd](https://github.com/libimobiledevice/libusbmuxd) (commit 8d30a559cf0585625d9d05dc8ce0dd495b1de4f4);
    * [libirecovery](https://github.com/libimobiledevice/libirecovery) (commit c7b488fbf2a9ab95e451df1319e68662fff7b9b7);
    * [libimobiledevice](https://github.com/libimobiledevice/libimobiledevice) (commit 6fc41f57fc607df9b07446ca45bdf754225c9bd9);
    * [libimobiledevice-glue](https://github.com/libimobiledevice/libimobiledevice-glue) (commit 214bafdde6a1434ead87357afe6cb41b32318495);
    * [libpng16](https://github.com/glennrp/libpng);
    * [xpwn](https://github.com/planetbeing/xpwn.git) (commit ac362d4ffe4d0489a26144a1483ebf3b431da899);
    * [libgeneral](https://github.com/tihmstar/libgeneral) (commit f6a74abb12e174af6768c13a265a7a2fbe43c33c);
    * [libfragmentzip](https://github.com/tihmstar/libfragmentzip) (commit 1f6b7af4eb113002c3473f873bb8d63598dd354f);
    * [libinsn](https://github.com/tihmstar/libinsn) (commit 64124fd2b1b57d7b76a0e2b0c06434a7048758d2);
    * [lzfse](https://github.com/lzfse/lzfse) (Linux/Windows only, macOS has built in libcompression);
    * [img4tool](https://github.com/tihmstar/img4tool) (commit aca6cf005c94caf135023263cbb5c61a0081804f);
    * [liboffsetfinder64](https://github.com/tihmstar/liboffsetfinder64) (commit e093adefc92e9c3b56d8f5989835f3247ea0e575);
    * [libipatcher(fork)](https://github.com/Cryptiiiic/libipatcher) (commit 1e855d70c84419014e363bdbcaead7b145fe3e1f)

* ## Submodules
  Make sure these projects compile on your system (install it's dependencies):

    * [tsschecker(fork)](https://github.com/1Conan/tsschecker);
    * * [jssy](https://github.com/tihmstar/jssy) (This is a submodule of tsschecker);
    * [idevicerestore(fork)](https://github.com/futurerestore/idevicerestore)

  If you are cloning this repository you may run:

  ```git clone https://github.com/futurerestore/futurerestore --recursive```

  which will clone these submodules for you.

# Building from source
* ## dep_root
  After obtaining all the required/optional dependencies you can either install them to your

  system for building dynamically or place the static libs in `dep_root/lib` and headers in

  `dep_root/include` for building statically
* ## build.sh
  Executing build.sh will configure and building in debug mode by default and an arch must be provided.
  * Example: `./build.sh -DARCH=x86_64` or `ARCH=x86_64 ./build.sh`
  
  If you want to build in release mode pass in the RELEASE=1 environment variable.
  * Example: `RELEASE=1 ./build.sh -DARCH=x86_64` or `RELEASE=0 ./build.sh -DARCH=x86_64`

  If you want to disable pkg-config linking you can provide the `NO_PKGCFG` flag. 

  By default pkg-config linking is enabled. dep_root will be used when disabled.
  * Example: `./build.sh -DARCH=x86_64 -DNO_PKGCFG=1`
  * or `NO_PKGCFG=1 ./build.sh -DARCH=x86_64`
  
  If you want to overwrite the compiler on mac you can provide `NO_XCODE` flag.
  * Example: `CC=gcc CXX=g++ ./build.sh -DARCH=x86_64 -DNO_XCODE=1` 
  * or `NO_XCODE=1 CC=gcc CXX=g++ ./build.sh -DARCH=x86_64`

  If you want to disable cmake reconfigure for each build, you can provide the `NO_CLEAN` flag.
  * Example: `NO_CLEAN=1 ./build.sh -DARCH=x86_64`
  * By default it will remove cmake and cache and reconfigure for each subsequent build.
  
  If you enable the os built in AddressSanitizer feature use the `ASAN` flag.
  * Example: `ASAN=1 ./build.sh -DARCH=x86_64`
  * or `./build.sh -DARCH=x86_64 -DASAN=1`
  
  The compiled binary will be located at:
  * `cmake-build-release/src/futurerestore` for release builds
  * `cmake-build-debug/src/futurerestore` for debug builds
  
  Otherwise you can install the binary via:
  * `make -C cmake-build-release install` for release builds
  * `make -C cmake-build-debug install` for debug builds