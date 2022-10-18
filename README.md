# Embedded Rust Learning Resources

Embedded Rust is a new phenomenon at the time of this writing.  Fortunately, for those who want to learn how to do it, 
ample resources are available.  This page will serve as a basic aggregation point for learning how to do embedded programming with Rust.

I currently have a NUCLEO-f030R8 board.  I will be getting a bbc micro:bit v2 soon.  I will focus first upon the NUCLEO-f030R8 board and then work with the micro:bit board per the Rust documentation.

## Embedded Rust for NUCLEO-f030R8

* Source site:  [Alexander Sayapin's Tutorial](https://alstutor.work/nucleo-f030r8-embedded-rust-quick-start-tutorial-part-1.html)
* Board:  [NUCLEO-f030R8 Board](https://www.st.com/en/evaluation-tools/nucleo-f030r8.html)
* IDE:  [Microsoft Visual Studio Code](https://code.visualstudio.com/)

### Resources:

* [The Embedded Rust Book](https://docs.rust-embedded.org/book/intro/index.html)
* [Discovery Rust Book](https://docs.rust-embedded.org/discovery/)
* [The Debugonomicon](https://github.com/rust-embedded/debugonomicon)
* [Rust Toolchain Installer(https://rustup.rs/)

Review Sayapin's instructions.  

### For the Impatient:

Install Rust and rustup.  There are several ways to do this.  I used brew since I am using OS X.  Additionally, I installed extensions into VS Code (rust-analyzer) and it may not be the correct way to go.  I will figure this out soon and update this page.



Test Rust
```
rustc -V
```
Install toolchains:
```
rustup target add thumbv6m-none-eabi
rustup target add thumbv7m-none-eabi
rustup target add thumbv7em-none-eabi
rustup target add thumbv7em-none-eabih
```

Install cargo-binutils
```
cargo install cargo-binutils
```

Install LLVM compiler
```
rustup component add llvm-tools-preview
```

Install itmdump
```
cargo install itm
```

### Installgdb, openocd, qemu, screen
#### **Linux:**
```
sudo apt install gdb-arm-none-eabi openocd screen qemu-system-arm

If you are using Ubuntu 18.04, you would need the following command:

sudo apt install gdb-multiarch openocd screen qemu-system-arm
```

Create the file /etc/udev/rules.d/70-st-link.rules:
```
nano /etc/udev/rules.d/70-st-link.rules
```
Containing:
```
# STM32F3DISCOVERY rev A/B - ST-LINK/V2
ATTRS{idVendor}=="0483", ATTRS{idProduct}=="3748", TAG+="uaccess"

# STM32F3DISCOVERY rev C+ - ST-LINK/V2-1
ATTRS{idVendor}=="0483", ATTRS{idProduct}=="374b", TAG+="uaccess"
```

Reload rules:
```
sudo udevadm control --reload-rules
```

Verify it loads.  Connect your board to your computer, open terminal and run:
```
openocd -f interface/stlink-v2-1.cfg -f target/stm32f0x.cfg
```


### **OS X:** (check this -- was from another tutorial.  May need to find gdb package for OS X)
```
brew install qemu openocd armmbed/formulae/arm-none-eabi-gcc
```

Verify:
```
cd Cellar/open-ocd/0.11.0/share/openocd/scripts/target
ls stm* (choose the right one)
```
Output:

```$ /usr/local/Cellar/open-ocd/0.11.0/share/openocd/scripts/target
└─ ▶ ls stm*
stm32f0x.cfg		stm32g4x.cfg		stm32l4x.cfg		stm8l.cfg
stm32f1x.cfg		stm32h7x.cfg		stm32l5x.cfg		stm8l152.cfg
stm32f2x.cfg		stm32h7x_dual_bank.cfg	stm32mp15x.cfg		stm8s.cfg
stm32f3x.cfg		stm32l0.cfg		stm32w108xx.cfg		stm8s003.cfg
stm32f4x.cfg		stm32l0_dual_bank.cfg	stm32wbx.cfg		stm8s103.cfg
stm32f7x.cfg		stm32l1.cfg		stm32wlx.cfg		stm8s105.cfg
stm32g0x.cfg		stm32l1x_dual_bank.cfg	stm32xl.cfg
```
.cfg file that worked for me was stm32f0x.cfg.

```
openocd -f interface/stlink.cfg -f target/stm32f0x.cfg
```

### Windows:
```
Good luck
```

### Create Project Templates

```
cargo install cargo-generate
```

Change directories to your git directory where you store your projects:
```
cargo generate --git https://github.com/rust-embedded/cortex-m-quickstart
```

Now read the rest of [Alexander Sayapin's Tutorial](https://alstutor.work/nucleo-f030r8-embedded-rust-quick-start-tutorial-part-1.html)
