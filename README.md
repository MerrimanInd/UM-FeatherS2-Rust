# UM-FeatherS2-Rust
This is a template/guide to running Rust on the [Unexpected Maker](https://unexpectedmaker.com/) [FeatherS2](https://feathers2.io/). I was using the board for a personal project and wanted to add to the minimal documentation that existed for running Rust on this board.

There's nothing wildly unique about this board compared to other ESP32 dev boards but it's a nice unit with a good set of peripherals and commonly available from many resellers like [Adafruit](https://www.adafruit.com/product/4769). Getting the most basic Rust example running on this board can be done very quickly using the main ESP32 workflow but I had to do some reading and learning to make use of the peripherals like Flash.

# Rust on ESP32

With the ESP32 series' popularity in the hobbyiest embedded community, it was one of the earliest boards targeted by the Rust community. There was a HAL (Hardware Abstraction Layer) crate targeting the basic ESP32 board called [esp32-hal](https://crates.io/crates/esp32-hal) built that enabled some Rust support on some of the boards. This was overall a great effort but the rustc compiler doesn't support the Xtensa ISA used by some ESP boards.

In 2024 Espressif got behind the Rust efforts and brought the development in-house. They created a new HAL abstracted over the entire ESP32 series ([esp-hal](https://github.com/esp-rs/esp-hal)), a new Github org with a ton of useful resources, and some additional new tooling. This includes:

* `espup` - similar to rustup but installs the linker and compiler necessary for Xtensa
* `esp-generate` - a CLI tool for creating template projects
* `espflash` - a dedicated tool for flashing and debugging ESP boards

[!WARNING]
If you're searching the internet for Rust on ESP32 examples note that blog posts, code snippets, and repos from prior to mid-2024 may be using the older community HAL. While there's some similarities the two HALs were a breaking change and older examples may not play nicely with the current ecosystem.

## Resources
[Rust on Espressif Github org](https://github.com/esp-rs)
[The Rust on ESP Book](https://docs.espressif.com/projects/rust/book/)
[Embedded Rust (no_std) on Espressif Training](https://docs.espressif.com/projects/rust/no_std-training/)
[esp Crate Documentation](https://docs.espressif.com/projects/rust/)

# Rust on the FeatherS2

Supported functionality:
- [x] Basic functionality (compiling, flashing)
- [ ] Wifi
- [ ] Bluetooth
- [ ] External SPI Flash
- [ ] External PSRAM

# How To
1. Install Rust and ESP toolchain as described in the [Setting up a Dev Env](https://docs.espressif.com/projects/rust/book/installation/index.html) section of the Rust on ESP Book. The ESP32S2 is an Xtensa target so make sure to install that toolchain, as documented [here](https://docs.espressif.com/projects/rust/book/installation/riscv-and-xtensa.html).
2. Don't forget to run `. /home/$user/export-esp.sh` in every new terminal session you plan to build or run in.
3. Plug in your FeatherS2 and put it in bootloader mode. This can be done by pressing and holding the BOOT button then either pressing the RST button or power cycling the board.
4. Navigate to the repo directory and run `cargo run`.
5. Reset the board into normal mode. That's it! A blinky example should be running on the board.
