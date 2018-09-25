GreenCoin integration/staging tree
================================

http://greencoin.life

Copyright (c) 2009-2018 GreenCoin Developers

What is GreenCoin?
----------------

GreenCoin is an experimental new digital currency that enables instant payments to
anyone, anywhere in the world. GreenCoin uses peer-to-peer technology to operate
with no central authority: managing transactions and issuing money are carried
out collectively by the network. GreenCoin is also the name of the open source
software which enables the use of this currency.

For more information, as well as an immediately useable, binary version of
the GreenCoin client software, see http://greencoin.life

License
-------

GreenCoin is released under the terms of the MIT license. See `COPYING` for more
information or see http://opensource.org/licenses/MIT.

For desktop Windows or Ubuntu use qt version of wallet
------------------------------------------------------

Windows - https://github.com/CryptorClub/GreenCoin/raw/master/greencoin-qt-windows.zip

Linux\Ubuntu - https://github.com/CryptorClub/GreenCoin/raw/master/greencoin-qt-linux.tar.gz


How to compile daemon node on Ubuntu 16.04
------------------------------------------

Use the following instructions

Update your Ubuntu machine.

    sudo apt-get update
    sudo apt-get upgrade

Install the dependencies to compile from source code.

    sudo apt-get install build-essential libssl-dev libdb-dev libdb++-dev libboost-all-dev git libssl1.0.0-dbg
    sudo apt-get install libdb-dev libdb++-dev libboost-all-dev libminiupnpc-dev libminiupnpc-dev libevent-dev libcrypto++-dev libgmp3-dev

Create a directory for the source code.

    mkdir source_code
    cd source_code

    sudo apt-get -y install git
    git clone https://github.com/CryptorClub/GreenCoin.git

Go to the src directory of your source code.

    cd GreenCoin/src

Execute the following command to compile the daemon.

    make -f makefile.unix RELEASE=1

The compiling will take about 30 minutes depending on your system. Required 2GB+ of RAM memory

Your compiled daemon named `greencoind` can be found in the src folder when compiling is finished.

Installation of daemon
----------------------

On Ubuntu 16.04 Move compiled daemon to your Home folder and follow instruction

    mv greencoind $HOME
    
On Ubuntu 14.04 You do not need compile daemon, just download and untar

    wget https://github.com/CryptorClub/GreenCoin/raw/master/greencoin-daemon-linux.tar.gz
    tar -xzvf greencoin-daemon-linux.tar.gz

Install the daemon.

    chmod +x greencoind
    sudo mv greencoind /usr/bin/

Create the config file.

    mkdir $HOME/.greencoin
    nano $HOME/.greencoin/greencoin.conf

Paste the following lines in greencoin.conf.

    rpcuser=rpc_greencoin
    rpcpassword=69c863e3356d3dae95df454a1
    rpcallowip=127.0.0.1
    listen=1
    server=1
    txindex=1
    daemon=1

Start your node with the following command.

    greencoind

Development process
-------------------

Developers work in their own trees, then submit pull requests when they think
their feature or bug fix is ready.

If it is a simple/trivial/non-controversial change, then one of the GreenCoin
development team members simply pulls it.

If it is a *more complicated or potentially controversial* change, then the patch
submitter will be asked to start a discussion (if they haven't already) on the
[mailing list](http://sourceforge.net/mailarchive/forum.php?forum_name=greencoin-development).

The patch will be accepted if there is broad consensus that it is a good thing.
Developers should expect to rework and resubmit patches if the code doesn't
match the project's coding conventions (see `doc/coding.md`) or are
controversial.

The `master` branch is regularly built and tested, but is not guaranteed to be
completely stable. [Tags](https://github.com/CryptorClub/GreenCoin/tags) are created
regularly to indicate new official, stable release versions of GreenCoin.

Testing
-------

Testing and code review is the bottleneck for development; we get more pull
requests than we can review and test. Please be patient and help out, and
remember this is a security-critical project where any mistake might cost people
lots of money.

### Automated Testing

Developers are strongly encouraged to write unit tests for new code, and to
submit new unit tests for old code.

Unit tests for the core code are in `src/test/`. To compile and run them:

    cd src; make -f makefile.unix test

Unit tests for the GUI code are in `src/qt/test/`. To compile and run them:

    qmake BITCOIN_QT_TEST=1 -o Makefile.test greencoin-qt.pro
    make -f Makefile.test
    ./greencoin-qt_test

Every pull request is built for both Windows and Linux on a dedicated server,
and unit and sanity tests are automatically run. The binaries produced may be
used for manual QA testing — a link to them will appear in a comment on the
pull request posted by [GreenCoinPullTester](https://github.com/CryptorClub/GreenCoinPullTester). See https://github.com/TheBlueMatt/test-scripts
for the build/test scripts.

### Manual Quality Assurance (QA) Testing

Large changes should have a test plan, and should be tested by somebody other
than the developer who wrote the code.

See https://github.com/CryptorClub/GreenCoin/ for how to create a test plan.
