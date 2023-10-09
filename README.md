. /home/guster32/odroidxu4_sdk/environment-setup-cortexa15t2hf-neon-vfpv4-arcadia-linux-gnueabi
ln -s /etc/ssl /home/guster32/odroidxu4_sdk/sysroots/x86_64-arcadiasdk-linux/etc/ssl
RUSTFLAGS="$RUSTFLAGS -C link-arg=-Wl,-dynamic-linker=/lib/ld-linux-armhf.so.3 -C linker=arm-arcadia-linux-gnueabi-gcc" cargo --offline build --target=armv7-arcadia-linux-gnueabihf