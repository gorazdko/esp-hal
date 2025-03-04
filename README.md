<p align="center">
  <img src="./resources/esp-rs.svg" alt="esp-rs logo" width="100px" />
</p>

<h1 align="center">esp-hal</h1>

<p align="center">
  <img src="https://img.shields.io/github/actions/workflow/status/esp-rs/esp-hal/ci.yml?labelColor=1C2C2E&label=CI&logo=github&style=flat-square" alt="GitHub Actions Workflow Status" />
  <img src="https://img.shields.io/github/actions/workflow/status/esp-rs/esp-hal/hil.yml?labelColor=1C2C2E&label=HIL&logo=github&style=flat-square&event=merge_group" alt="GitHub Actions Workflow Status" />
  <img src="https://img.shields.io/badge/license-MIT%2FApache--2.0-blue?labelColor=1C2C2E&style=flat-square" alt="MIT/Apache-2.0 licensed" />
  <a href="https://matrix.to/#/#esp-rs:matrix.org">
    <img src="https://img.shields.io/matrix/esp-rs:matrix.org?labelColor=1C2C2E&label=join%20matrix&color=BEC5C9&logo=matrix&style=flat-square" alt="Matrix" />
  </a>
</p>

Bare-metal (`no_std`) hardware abstraction layer for Espressif devices. Currently supports, to varying degrees, the following devices:

- ESP32 Series: _ESP32_
- ESP32-C Series: _ESP32-C2, ESP32-C3, ESP32-C6_
- ESP32-H Series: _ESP32-H2_
- ESP32-S Series: _ESP32-S2, ESP32-S3_

Additionally provides limited support for programming the low-power RISC-V cores found on the _ESP32-C6_, _ESP32-S2_, and _ESP32-S3_ via the [esp-lp-hal] package.

For additional information regarding any of the crates in this repository, please refer to the relevant crate's `README.md` file. If you have any questions, comments, or concerns, please [open an issue], [start a new discussion], or join us on [Matrix].

If you are currently using (or considering using) `esp-hal` in a production environment and have any feedback or require support, please feel free to contact us at <rust.support@espressif.com>.

> [!NOTE]
>
> This repository includes crates that are at various stages of maturity and stability. While many functionalities have already been implemented and are usable for most tasks, certain advanced or less common features may still be under development. Each crate may offer different levels of functionality and guarantees.

[esp-lp-hal]: https://github.com/esp-rs/esp-hal/tree/main/esp-lp-hal
[esp-idf-svc]: https://github.com/esp-rs/esp-idf-svc
[open an issue]: https://github.com/esp-rs/esp-hal/issues/new
[start a new discussion]: https://github.com/esp-rs/esp-hal/discussions/new
[matrix]: https://matrix.to/#/#esp-rs:matrix.org

## Getting Started

For information relating to the development of Rust applications on ESP devices, please first read [The Rust on ESP Book].

For information about the HAL and how to use it in your own projects, please refer to the [documentation].

When browsing the examples, we recommend viewing the tag for the `esp-hal` release you are using to ensure compatibility, e.g. [esp-hal-v1.0.0-beta.0], as the `main` branch is used for development and APIs may have changed in the meantime.

[The Rust on ESP Book]: https://esp-rs.github.io/book/
[documentation]: https://docs.espressif.com/projects/rust/
[esp-hal-v1.0.0-beta.0]: https://github.com/esp-rs/esp-hal/tree/esp-hal-v1.0.0-beta.0/examples

### Getting Started by Gorazd

## Install Toolchain

$ rustup toolchain install nightly --component rust-src   // source: https://docs.esp-rs.org/book/installation/riscv.html

$ rustup target add riscv32imc-unknown-none-elf
$ rustup target add riscv32imac-unknown-none-elf


$ cargo install espup    // source: https://docs.esp-rs.org/book/installation/riscv-and-xtensa.html
$ espup install

```
 To get started, you need to set up some environment variables by running: '. /home/gorazd/export-esp.sh'
        This step must be done every time you open a new terminal.
            See other methods for setting the environment in https://esp-rs.github.io/book/installation/riscv-and-xtensa.html#3-set-up-the-environment-variables
```


$ cargo install cargo-espflash    // source:  https://docs.esp-rs.org/book/tooling/espflash.html#espflash-1
$ cargo install espflash

## Build, flash and run example

Run command from the root folder of the repository.

```
gorazd@gorazd-Victus-by-HP-Laptop-16-e0xxx:~/Projects/esp-hal$ cargo xtask run-example esp-hal esp32 embassy_hello_world
    Finished `dev` profile [unoptimized + debuginfo] target(s) in 0.07s
     Running `target/debug/xtask run-example esp-hal esp32 embassy_hello_world`
[2025-03-04T20:10:45Z WARN  xtask] Package 'esp-hal' specified, using 'examples' instead
[2025-03-04T20:10:45Z INFO  xtask] Building example 'src/bin/embassy_hello_world.rs' for 'esp32'
[2025-03-04T20:10:45Z INFO  xtask]   Features:      embassy, esp-hal/unstable
    Updating crates.io index
    Finished `release` profile [optimized + debuginfo] target(s) in 2.05s
     Running `espflash flash --monitor target/xtensa-esp32-none-elf/release/embassy_hello_world`
[2025-03-04T20:10:47Z INFO ] Serial port: '/dev/ttyUSB0'
[2025-03-04T20:10:47Z INFO ] Connecting...
[2025-03-04T20:10:48Z INFO ] Using flash stub
Chip type:         esp32 (revision v3.1)
Crystal frequency: 40 MHz
Flash size:        4MB
Features:          WiFi, BT, Dual Core, 240MHz, Coding Scheme None
MAC address:       b0:b2:1c:a1:03:f0
App/part. size:    95,088/4,128,768 bytes, 2.30%
[00:00:01] [========================================]      17/17      0x1000    [00:00:00] [========================================]       1/1       0x8000    [00:00:02] [========================================]      27/27      0x10000   [2025-03-04T20:10:54Z INFO ] Flashing has completed!
Commands:
    CTRL+R    Reset chip
    CTRL+C    Exit

ets Jul 29 2019 12:21:46

rst:0x1 (POWERON_RESET),boot:0x1b (SPI_FAST_FLASH_BOOT)
configsip: 0, SPIWP:0xee
clk_drv:0x00,q_drv:0x00,d_drv:0x00,cs0_drv:0x00,hd_drv:0x00,wp_drv:0x00
mode:DIO, clock div:2
load:0x3fff0030,len:7104
load:0x40078000,len:15576
load:0x40080400,len:4
ho 8 tail 4 room 4
load:0x40080404,len:3876
entry 0x4008064c
I (31) boot: ESP-IDF v5.1-beta1-378-gea5e0ff298-dirt 2nd stage bootloader
I (31) boot: compile time Jun  7 2023 07:48:23
I (33) boot: Multicore bootloader
I (37) boot: chip revision: v3.1
I (41) boot.esp32: SPI Speed      : 40MHz
I (46) boot.esp32: SPI Mode       : DIO
I (50) boot.esp32: SPI Flash Size : 4MB
I (55) boot: Enabling RNG early entropy source...
I (60) boot: Partition Table:
I (64) boot: ## Label            Usage          Type ST Offset   Length
I (71) boot:  0 nvs              WiFi data        01 02 00009000 00006000
I (79) boot:  1 phy_init         RF data          01 01 0000f000 00001000
I (86) boot:  2 factory          factory app      00 00 00010000 003f0000
I (94) boot: End of partition table
I (98) esp_image: segment 0: paddr=00010020 vaddr=3ffb0000 size=00798h (  1944) load
I (107) esp_image: segment 1: paddr=000107c0 vaddr=3f4007c0 size=0297ch ( 10620) map
I (119) esp_image: segment 2: paddr=00013144 vaddr=3ffb0798 size=00008h (     8) load
I (123) esp_image: segment 3: paddr=00013154 vaddr=40080000 size=01610h (  5648) load
I (134) esp_image: segment 4: paddr=0001476c vaddr=00000000 size=0b8ach ( 47276) 
I (157) esp_image: segment 5: paddr=00020020 vaddr=400d0020 size=0732ch ( 29484) map
I (169) boot: Loaded app from partition at offset 0x10000
I (169) boot: Disabling RNG early entropy source...
Init!
Bing!
Hello world from embassy using esp-hal-async!
Hello world from embassy using esp-hal-async!
Hello world from embassy using esp-hal-async!
Hello world from embassy using esp-hal-async!
Hello world from embassy using esp-hal-async!
Bing!
Hello world from embassy using esp-hal-async!
Hello world from embassy using esp-hal-async!
Hello world from embassy using esp-hal-async!
Hello world from embassy using esp-hal-async!
Hello world from embassy using esp-hal-async!
Bing!
Hello world from embassy using esp-hal-async!
Hello world from embassy using esp-hal-async!
Hello world from embassy using esp-hal-async!
Hello world from embassy using esp-hal-async!
Hello world from embassy using esp-hal-async!
Bing!
Hello world from embassy using esp-hal-async!

```





## Resources

- [The Rust Programming Language](https://doc.rust-lang.org/book/)
- [The Embedded Rust Book](https://docs.rust-embedded.org/book/index.html)
- [The Embedonomicon](https://docs.rust-embedded.org/embedonomicon/)
- [The Rust on ESP Book](https://esp-rs.github.io/book/)
- [Embedded Rust (no_std) on Espressif](https://esp-rs.github.io/no_std-training/)

## Contributing

We have a number of living documents to aid contributing to the project, please give these a read before modifying code:

- [API-GUIDELINES](https://github.com/esp-rs/esp-hal/blob/main/documentation/API-GUIDELINES.md)
- [CONTRIBUTING-GUIDE](https://github.com/esp-rs/esp-hal/blob/main/documentation/CONTRIBUTING.md)

## License

All packages within this repository are licensed under either of:

- Apache License, Version 2.0 ([LICENSE-APACHE](LICENSE-APACHE) or http://www.apache.org/licenses/LICENSE-2.0)
- MIT license ([LICENSE-MIT](LICENSE-MIT) or http://opensource.org/licenses/MIT)

at your option.

### Contribution notice

Unless you explicitly state otherwise, any contribution intentionally submitted for inclusion in
the work by you, as defined in the Apache-2.0 license, shall be dual licensed as above, without
any additional terms or conditions.
