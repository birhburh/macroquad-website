+++
title = "Cross compilation of *quads project from Linux to iOS simulator and real device"
description = "Guide with instructions for cross compilation using zigbuild."
date = 2024-08-02T09:19:42+00:00
updated = 2024-08-02T09:19:42+00:00
draft = true
template = "blog/page.html"
+++

Moved this from [osx cross compilation article](/articles/zigbuild) because ios target is not implemented for cargo-zigbuild now and probably it needs iPhoneSimulatorSDK and not iPhoneSDK for simulator. But there is no convenient repositories with those.

## Add target:
### For iOS simulator:
```sh
rustup target add x86_64-apple-ios
```

## Download necessary sdk
Luckly there is [this repo](https://github.com/roblabla/MacOSX-SDKs) and [this repo](https://github.com/xybp888/iOS-SDKs). Use needed version. Replace in the lines below.
### For iOS simulator:
```sh
curl -L https://github.com/xybp888/iOS-SDKs/releases/download/iOS-SDKs/iPhoneOS16.1.sdk.zip -o iPhoneOS16.1.sdk.zip && unzip iPhoneOS16.1.sdk.zip && rm iPhoneOS16.1.sdk.zip
```

## Install Zig language compiler
Using [this guilde](https://github.com/ziglang/zig/wiki/Install-Zig-from-a-Package-Manager) for your distribution.
For Ubuntu 20.04 it was:
```sh
snap install zig --classic --beta
```

## Install zigbuild
### For OSX:
It's simple
```sh
cargo install --locked cargo-zigbuild
```
### For iOS simulator:
I have a fork now https://github.com/birhburh/cargo-zigbuild
But it is not working
Should dig deeper into build.zig file of this repository
https://github.com/kubkon/zig-ios-example

## Set SDKROOT for zigbuild to found
Add this to .bashrc if needed (replace `$(pwd)` of course)
### For iOS simulator:
```sh
export SDKROOT=$(pwd)/iPhoneOS16.1.sdk/
```

## Cross-compile using zigbuild
```sh
cargo zigbuild --release --target x86_64-apple-ios
```
