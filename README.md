# esp32c3-no-std-async-mqtt-demo

This is a simple demo that we will use on the upcoming Espressif DevCon23.

ESP32 variant: https://github.com/JurajSadel/esp32-no-std-async-mqtt-demo

ESP32S3 variant: https://github.com/JurajSadel/esp32s3-no-std-async-mqtt-demo

## What it does
The application measures temperature (`BMP180`) and sends the results to `MQTT` via WiFi - everything is done asynchronously.

It's `async no_std` application that uses [esp-hal](https://crates.io/crates/esp32c3-hal), [esp-wifi](https://github.com/esp-rs/esp-wifi/tree/main), and [rust-mqtt](https://crates.io/crates/rust-mqtt) crates. The main skeleton is made of [embassy_dhcp](https://github.com/esp-rs/esp-wifi/blob/68dc11bbb2c0efa29c4acbbf134d6f142441065e/examples-esp32c3/examples/embassy_dhcp.rs) and [no_std_temperature_logger](https://github.com/bjoernQ/esp32-rust-nostd-temperature-logger) with a bunch of changes.

The first change is `MQTT` part added. We are using `MQTTv5`. As a broker, we use[public-mqtt-broker](https://www.hivemq.com/public-mqtt-broker/) and [websocket-client](https://www.hivemq.com/demos/websocket-client/) to see the results.

As a next change, we had to make [bmp180.rs](https://github.com/bjoernQ/esp32-rust-nostd-temperature-logger/blob/main/src/bmp180.rs) `async`.

## Build and run
You have to set the `SSID` and `PASSWORD` environment variables before building/running the program

`cargo run --release`

> **_WARN:_** Be sure you are using `release` mode!
## License

Licensed under either of:

- Apache License, Version 2.0 ([LICENSE-APACHE](LICENSE-APACHE) or http://www.apache.org/licenses/LICENSE-2.0)
- MIT license ([LICENSE-MIT](LICENSE-MIT) or http://opensource.org/licenses/MIT)

at your option.

### Contribution

Unless you explicitly state otherwise, any contribution intentionally submitted for inclusion in
the work by you, as defined in the Apache-2.0 license, shall be dual licensed as above, without
any additional terms or conditions.

## Hardware 

Ref divider: 0.911K, 199.7R, Vref = 0.591V

Voltage dividers:
- L1: 388.3K 510R
- L2: 395.4K 506.5R
- L3: 393.1K 486.8R

Current sense:
- L1: 20.1R
- L2: 20.1R
- L3: 20.1R

Multimeter lead resistance: 0.3R

Current sense RC filter: 367.8K 5pF
Voltage sense RC filter: 5pF

