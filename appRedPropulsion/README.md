# Zephyr STM32 Nucleo-H723ZG App

This repository contains a minimal Zephyr application configured for the STM32 Nucleo-H723ZG. It is structured as a **Zephyr Workspace Application**, meaning this repository acts as the manifest source.

## Setup Instructions
>we recommend developing in a linux enviroment (the following isntructions are for a UNIX system) but use what you have.

To build and run this application, you need to use `west` to initialize a workspace around it. This will automatically pull down the Zephyr kernel and the required STM32/ARM CMSIS dependencies.

### 1. Directory setup
```bash
mkdir your-zephyr-workspace
cd your-zephyr-workspace

```

### 2. Venv
```bash
python -m venv .venv

source .venv/bin/activate
```
if using `uv` instead of plain `pip`

```bash
uv venv

source .venv/bin/activate
```

### 3. Install Dependencies
Ensure you have the [Zephyr SDK and West installed](https://docs.zephyrproject.org/latest/develop/getting_started/index.html) on your system.
or you can use:

```bash
pip install west
```
or
```bash
uv pip install west
```

### 4. Create a Workspace & Clone
Create an empty directory for your workspace, then clone this repository inside it:

```bash
git clone <YOUR_GITHUB_REPO_URL> my_app
```

### 5. Update dependencies

```bash
west zephyr-export
west packages pip --install # or west packages pip | xargs uv pip install 
west sdk install --toolchain arm-zephyr-eabi
```

## Develop your app
Based on the project assigned to you develop everything in the `src` dir, create other files if needed, you may or may not have to edit the `prj.conf` and `nucleo_h723zg.overlay` files and look for documentation for `STM32 Nucleo-H723ZG`.
You will definetly have to look up documentation for the device subject of your project.

> note: `.overlay` file is an overlay for `.dts` aka device tree files.

you may contact who assigned you the project for assistance.

to submit the project make sure it compiles.

## Bulding your app
```bash
west build apps/my_app
```
# Projects
For all of the projects write a `Docs.MD` file explaining how the hardware works and what are the concept that a new developer editing your code would need to know, assume they have no knowledge (so just write what you would have liked to have while doing this project)

> If you aren't able to develope working code, proper documentation and understanding of the processes might be enough, so do it properly.

## 1. Servo Driver

Link: https://www.waveshare.com/st3215-servo.htm

| Function     | Pin |
| ------------ | --- |
| Servo Enable | PD7 |
| Servo RX     | PD6 |
| Servo TX     | PD5 |

## 2. RunCam library
https://support.runcam.com/hc/en-us/articles/360014537794-RunCam-Device-Protocol

for this project it is not required to setup a Zephyr workflow, you should use plain C and have console I/O to verify if the parser/packet generator work properly.
However if you want to get used with the development enviroment you can implement this comunication on an UART interface of your choice on the STM32 H7 chip.

User should be able to get RunCam recording status and Start/Stop Recording.



## 3. GPIO Neopixel(LED) Driver
| Function        | Pin |
| --------------- | --- |
| Neopixel Enable | PE5 |
| Neopixel Data   | PE6 |

4 LED
clock CPU: 550 MHz

> note: use GPIO only, no UART or SPI.