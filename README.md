# Avalyn

<img src="https://avyblocks.com/imgs/avy_iconv2.png" width="250" height="250">

`Scalable.` `Secure.` `Private.` `Untraceable.` `Fungible.` `Decentralized.`

Copyright (c) 2023, The Avalyn Project

## Table of Contents

  - [Development resources](#development-resources)
  - [About this project](#about-this-project)
  - [Supporting the project](#supporting-the-project)
  - [Compiling Avalyn from source](#compiling-avalyn-from-source)

## Development resources

- Web: [avyblocks.com](https://avyblocks.com)
- Mail: [dev@avyblocks.com](mailto:dev@avyblocks.com)
- GitHub: [https://github.com/avalyn-project/avalyn](https://github.com/avalyn-project/avalyn)

## Supporting the project

Avalyn is a 100% community-sponsored endeavor. If you want to join our efforts, the easiest thing you can do is support the project financially. Both Avalyn and Bitcoin donations can be made to **donate.avyblocks.com** if using a client that supports the [OpenAlias](https://openalias.org) standard. Alternatively, you can send AVY to the Avalyn donation address via the `donate` command (type `help` in the command-line wallet for details).

Avalyn [AVY] donation address is:  
`4fDMpt97JfFVevG1fzy8SnLoE86W4r5CCRirEa6NnAw8JPVjSegxKkif1B1N78GwEwTvUdFxAkH8UDnZqihR7bdU13f4gYv`

Monero [XMR] donation address is:  
`8415u84k8Sr17oeJE1KrrRgyZqwBd1eZzAGBhS2PNA7aPM4NRsPHvq3jPbqj9FHP5EJbzrU2zaVN8AEkTaUci5LDKj7y1nq`

Bitcoin [BTC] donation address is:  
`bc1q9k0mv2y35u0yss46hau0qx2dakaj0j5whtxmhw`

Ethereum [ETH] donation address is:  
`0xea5667bb66bc0b0fde33ed7abe562b82559088a1`

Core development funding and/or some supporting services are also graciously provided by [sponsors](https://www.getmonero.org/community/sponsorships/):

[<img width="150" src="https://www.getmonero.org/img/sponsors/tarilabs.png"/>](https://tarilabs.com/)
[<img width="150" src="https://www.getmonero.org/img/sponsors/globee.png"/>](https://globee.com/)
[<img width="150" src="https://www.getmonero.org/img/sponsors/symas.png"/>](https://symas.com/)
[<img width="150" src="https://www.getmonero.org/img/sponsors/forked_logo.png"/>](http://www.forked.net/)
[<img width="150" src="https://www.getmonero.org/img/sponsors/macstadium.png"/>](https://www.macstadium.com/)

There are also several mining pools that kindly donate a portion of their fees, [a list of them can be found on our Bitcointalk post](https://bitcointalk.org/index.php?topic=583449.0).


## Scheduled software/network upgrades

Avalyn uses a scheduled software/network upgrade (hard fork) mechanism to implement new features into the Avalyn software and network. This means that users of Avalyn (end users and service providers) should run current versions and upgrade their software when new releases are available. Software upgrades occur when new features are developed and implemented in the codebase. Network upgrades occur in tandem with software upgrades that modify the consensus rules of the Avalyn network. The required software for network upgrades will be available prior to the scheduled network upgrade date. Please check the repository prior to this date for the proper Avalyn software version. Below is the historical schedule and the projected schedule for the next upgrade.

Dates are provided in the format YYYY-MM-DD. The "Minimum" is the software version that follows the new consensus rules. The "Recommended" version may include bug fixes and other new features that do not affect the consensus rules.

## Compiling Avalyn from source

[1] On Debian/Ubuntu `libgtest-dev` only includes sources and headers. You must
build the library binary manually. This can be done with the following command `sudo apt-get install libgtest-dev && cd /usr/src/gtest && sudo cmake . && sudo make`
then:

* on Debian:
  `sudo mv libg* /usr/lib/`
* on Ubuntu:
  `sudo mv lib/libg* /usr/lib/`

[2] libnorm-dev is needed if your zmq library was built with libnorm, and not needed otherwise

Install all dependencies at once on Debian/Ubuntu:

`
sudo apt update && sudo apt install build-essential cmake pkg-config libssl-dev libzmq3-dev libunbound-dev libsodium-dev libunwind8-dev liblzma-dev libreadline6-dev libexpat1-dev libpgm-dev qttools5-dev-tools libhidapi-dev libusb-1.0-0-dev libprotobuf-dev protobuf-compiler libudev-dev libboost-chrono-dev libboost-date-time-dev libboost-filesystem-dev libboost-locale-dev libboost-program-options-dev libboost-regex-dev libboost-serialization-dev libboost-system-dev libboost-thread-dev python3 ccache doxygen graphviz
`

### Cloning the repository

Clone recursively to pull-in needed submodule(s):

`
git clone --recursive https://github.com/avalyn-project/avalyn
`

If you already have a repo cloned, initialize and update:

`
cd avalyn && git submodule init && git submodule update
`

Now, simply use `make` to build Avalyn.

*Note*: If there are submodule differences between branches, you may need 
to use `git submodule sync && git submodule update` after changing branches
to build successfully.

### Build instructions

Avalyn uses the CMake build system and a top-level [Makefile](Makefile) that
invokes cmake commands as needed.

* The resulting executables can be found in `build/release/bin`

* Add `PATH="$PATH:$HOME/avalyn/build/release/bin"` to `.profile`

* Run Avalyn with `avalynd --detach`

### Blockchain-based

Certain blockchain "features" can be considered "bugs" if misused correctly. Consequently, please consider the following:

- When receiving Avalyn, be aware that it may be locked for an arbitrary time if the sender elected to, preventing you from spending that Avalyn until the lock time expires. You may want to hold off acting upon such a transaction until the unlock time lapses. To get a sense of that time, you can consider the remaining blocktime until unlock as seen in the `show_transfers` command.
