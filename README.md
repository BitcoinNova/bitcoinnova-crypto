![image](https://camo.githubusercontent.com/98f307e50e222b95c1695c11208bd91565f8b7c7/687474703a2f2f706f6f6c2e626974636f696e6e2e62697a2f626974636f696e2d6e6f76612e706e67)
[![NPM](https://nodei.co/npm/bitcoinnova-crypto.png?downloads=true&stars=true)](https://nodei.co/npm/bitcoinnova-crypto/)
#### Master Build Status
[![Build Status](https://travis-ci.org/BitcoinNova/bitcoinnova-crypto.svg?branch=master)](https://travis-ci.org/BitcoinNova/bitcoinnova-crypto) [![Build status](https://ci.appveyor.com/api/projects/status/ecy3o2dhc4nm3306?svg=true)](https://ci.appveyor.com/project/BitcoinNovaProject/bitcoinnova-crypto)

# BitcoinNova: Standalone Cryptography Library

This repository contains the necessary files to compile the cryptography library used within [BitcoinNova](https://bitcoinnova.org) as a standalone library that can be included in various other projects in a variety of development environments, including:

* Node.js >= 6.x
* C++
* C# (via C++ shared library & P/Invoke)
* Native Javascript
* WASM

## Node.js Module

### Dependencies

* [Node.js](https://nodejs.org) >= +6.x LTS (or Node v11)

#### Windows

##### Prerequisites

Read very careful if you want this to work right the first time.

1) Open a *Windows Powershell* console as **Administrator**
2) Run the command: `npm install -g windows-build-tools --vs2015`
   ***This will take a while. Sit tight.***
   
#### Linux

### Installation

```bash
npm install bitcoinnova-crypto
```

### Intialization

```javascript
const BitcoinNovaCrypto = require('bitcoinnova-crypto')
```

## C++ Library

### How To Compile

#### Build Optimization

The CMake build system will, by default, create optimized *native* builds for your particular system type when you build the software. Using this method, the binaries created provide a better experience and all together faster performance.

However, if you wish to create *portable* binaries that can be shared between systems, specify `-DARCH=default` in your CMake arguments during the build process. Note that *portable* binaries will have a noticable difference in performance than *native* binaries. For this reason, it is always best to build for your particuar system if possible.

#### Linux

##### Ubuntu, using GCC

```bash
sudo add-apt-repository ppa:ubuntu-toolchain-r/test -y
sudo apt-get update
sudo apt-get install aptitude -y
sudo aptitude install -y build-essential git cmake
git clone -b master --single-branch https://github.com/BitcoinNova/bitcoinnova-crypto
cd bitcoinnova-crypto
mkdir build
cd build
cmake ..
make -j
```

The static library will be built as `libbitcoinnova-crypto.a` in the build folder.

##### Ubuntu, using Clang

```bash
sudo add-apt-repository ppa:ubuntu-toolchain-r/test -y
wget -O - https://apt.llvm.org/llvm-snapshot.gpg.key | sudo apt-key add -
```

You need to modify the below command for your version of ubuntu - see https://apt.llvm.org/

* Ubuntu 14.04 (Trusty)
- `sudo add-apt-repository "deb https://apt.llvm.org/trusty/ llvm-toolchain-trusty 6.0 main"`

* Ubuntu 16.04 (Xenial)
- `sudo add-apt-repository "deb https://apt.llvm.org/xenial/ llvm-toolchain-xenial 6.0 main"`

* Ubuntu 18.04 (Bionic)
- `sudo add-apt-repository "deb https://apt.llvm.org/bionic/ llvm-toolchain-bionic 6.0 main"`

```bash
sudo apt-get update
sudo apt-get install aptitude -y
sudo aptitude install -y -o Aptitude::ProblemResolver::SolutionCost='100*canceled-actions,200*removals'
sudo aptitude install build-essential clang-6.0 libstdc++-7-dev git cmake
export CC=clang-6.0
export CXX=clang++-6.0
git clone -b master --recursive --single-branch https://github.com/BitcoinNova/bitcoinnova-crypto
cd bitcoinnova-crypto
mkdir build
cd build
cmake ..
make -j
```

The following library files will be created in the `build` folder:

* `libbitcoinnova-crypto-static.a`

##### Generic Linux

Ensure you have the dependencies listed above.

If you want to use clang, ensure you set the environment variables `CC` and `CXX`.
See the ubuntu instructions for an example.

```bash
git clone -b master --single-branch https://github.com/BitcoinNova/bitcoinnova-crypto
cd bitcoinnova-crypto
mkdir build
cd build
cmake ..
make -j
```

The following library files will be created in the `build` folder:

* `libbitcoinnova-crypto-static.a`

#### OSX/Apple, using Clang

##### Prerequisites

- Install XCode and Developer Tools.

##### Building

```bash
which brew || /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
brew install --force cmake boost llvm
export CC=/usr/local/opt/llvm/bin/clang
export CXX=/usr/local/opt/llvm/bin/clang++
git clone -b master --recursive --single-branch https://github.com/BitcoinNova/bitcoinnova-crypto
cd bitcoinnova-crypto
mkdir build
cd build
cmake ..
make
```

The following library files will be created in the `build` folder:

* `libbitcoinnova-crypto-static.a`

#### Windows

##### Prerequisites

- Install [Visual Studio 2017 Community Edition](https://www.visualstudio.com/thank-you-downloading-visual-studio/?sku=Community&rel=15&page=inlineinstall)
- When installing Visual Studio, it is **required** that you install **Desktop development with C++**

##### Building

- From the start menu, open 'x64 Native Tools Command Prompt for vs2017'.
```
cd <your_bitcoinnova-crypto_directory>
mkdir build
cd build
set PATH="C:\Program Files (x86)\Microsoft Visual Studio\2017\Community\Common7\IDE\CommonExtensions\Microsoft\CMake\CMake\bin";%PATH%
cmake -G "Visual Studio 15 2017 Win64" ..
```

**Note:** If you have errors on this step about not being able to find the some libraries, you may need to update your cmake. Open 'Visual Studio Installer' and click 'Update'.

`MSBuild bitcoinnova-crypto.sln /p:Configuration=Release /m`

The following library files will be created in the `build/Release` folder:

* `bitcoinnova-crypto-static.lib`
* `bitcoinnova-crypto-shared.lib`
* `bitcoinnova-crypto-shared.dll`

## Native Javascript & WASM

### Prerequisites

You will need the following packages: CMake (2.8 or higher), make, and git.

### Compiling

```bash
git clone -b master --recursive --single-branch https://github.com/BitcoinNova/bitcoinnova-crypto
cd bitcoinnova-crypto
bash ./build_js.sh
```

This script will install the necessary dependencies on your machine and then proceed to compile the library to Native Javascript and WASM.

The following library files will be created in the `jsbuild` folder:

* Native Javascript
  * `bitcoinnova-crypto.js`
* WASM
  * `bitcoinnova-crypto-wasm.js`

## Thanks
Cryptonote Developers, Bytecoin Developers, Monero Developers, Forknote Project, BitcoinNova Community

## Copypasta for license when editing files

Hi BitcoinNova contributor, thanks for forking and sending back Pull Requests. Extensive docs about contributing are in the works or elsewhere. For now this is the bit we need to get into all the files we touch. Please add it to the top of the files.

```
// Copyright (c) 2012-2017, The CryptoNote developers, The Bytecoin developers
// Copyright (c) 2014-2018, The Monero Project
// Copyright (c) 2019, The Turtlecoin Developers
// Copyright (c) 2019-2020, The Bitcoin Nova Developers
//
// Please see the included LICENSE file for more information.
```
