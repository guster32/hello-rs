# SDK Extra setup
ln -s /etc/ssl /home/guster32/odroidxu4_sdk/sysroots/x86_64-arcadiasdk-linux/etc/ssl
<br>

# Odroid Build
. /home/guster32/odroidxu4_sdk/environment-setup-cortexa15t2hf-neon-vfpv4-arcadia-linux-gnueabi
<br>
RUSTFLAGS="$RUSTFLAGS -C link-arg=-Wl,-dynamic-linker=/lib/ld-linux-armhf.so.3 -C linker=arm-arcadia-linux-gnueabi-gcc" cargo --offline build --target=armv7-arcadia-linux-gnueabihf

# Qemu Build

```
ln -s /etc/ssl "$HOME/qemux86-64_sdk/sysroots/x86_64-arcadiasdk-linux/etc/ssl"
ln -s "$HOME/qemux86-64_sdk/sysroots/x86_64-arcadiasdk-linux/usr/lib/libclang-cpp.so.15" "$HOME/qemux86-64_sdk/sysroots/x86_64-arcadiasdk-linux/usr/lib/libclang.so.15"
cp "$HOME/git/guster32/scripts/.build/buildArcadiaDevQemu/build/tmp-glibc/sysroots-components/x86_64-nativesdk/nativesdk-clang/usr/local/oe-sdk-hardcoded-buildpath/sysroots/x86_64-arcadiasdk-linux/usr/lib/libclang.so.15.0.7" "$HOME/qemux86-64_sdk/sysroots/x86_64-arcadiasdk-linux/usr/lib/"

export RUST_ARCADIA_TARGET_LIBS=$HOME/qemux86-64_sdk/sysroots/core2-64-arcadia-linux/usr/lib/rustlib/x86_64-arcadia-linux-gnu/lib
mv $RUST_ARCADIA_TARGET_LIBS/libstd-f1beb7fa065ddb8a.rlib $RUST_ARCADIA_TARGET_LIBS/_libstd-f1beb7fa065ddb8a.rlib
mv $RUST_ARCADIA_TARGET_LIBS/libstd-f1beb7fa065ddb8a.so $RUST_ARCADIA_TARGET_LIBS/_libstd-f1beb7fa065ddb8a.so
mv $RUST_ARCADIA_TARGET_LIBS/libcore-529b855680093334.rlib $RUST_ARCADIA_TARGET_LIBS/_libcore-529b855680093334.rlib
mv $RUST_ARCADIA_TARGET_LIBS/libcompiler_builtins-f4bf402e27e86439.rlib $RUST_ARCADIA_TARGET_LIBS/_libcompiler_builtins-f4bf402e27e86439.rlib


. "$HOME/qemux86-64_sdk/environment-setup-core2-64-arcadia-linux"
export CLANG_PATH="$HOME/qemux86-64_sdk/sysroots/x86_64-arcadiasdk-linux/usr/bin/clang"
export LIBCLANG_PATH="$HOME/qemux86-64_sdk/sysroots/x86_64-arcadiasdk-linux/usr/lib/"
export LLVM_CONFIG_PATH="$HOME/qemux86-64_sdk/sysroots/x86_64-arcadiasdk-linux/usr/bin/llvm-config"
export BINDGEN_EXTRA_CLANG_ARGS="--sysroot=$HOME/qemux86-64_sdk/sysroots/core2-64-arcadia-linux/"
RUSTFLAGS="$RUSTFLAGS -L /usr/lib/rustlib/x86_64-arcadiasdk-linux-gnu/lib -C link-arg=-Wl,-dynamic-linker=/lib/ld-linux-x86-64.so.2 -C linker=x86_64-arcadia-linux-gcc" cargo build

```