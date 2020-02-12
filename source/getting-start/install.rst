Install OKChain
===============

| Currently, ``OKChain`` is not open source. You can download the
executable programs ``okchaind`` and ``okchaincli`` through the
`official website <https://github.com/ok-chain/binaries>`__.
| After downloading successfully, you can use the related functions of
``OKChain``.

    Note: The current version of ``OKChain`` used by the testnet is
    ``v0.1.0``.

1. Verify the version of OKChain
--------------------------------

After installing OKChain, you can verify the version information with
the following commands:

.. code:: sh

    $ okchaind version 
    $ okchaincli version

For example, ``okchaind version`` should output the information similar
to the following:

.. code:: sh

    $ okchaind version
    version: 0.1.0
    git commit: d465b5998b534772c53385370067ad08c7f7f40d
    vendor hash: 63a7a90a0a940f9213a1a57d7e76fcff1a2ccce1
    build tags: netgo
    cosmos-sdk: v0.34.7
    tendermint: v0.31.5
    go version go1.12 darwin/amd64

.. raw:: html

   <!--
   ## 2. Install from source (use TODO after opening source)
   ### 2.1 Install Go
   Install `go` according to the [official Go documentation](https://golang.org/doc/install). Configure environment variables `$GOPATH`, `$GOBIN` and `$PATH`. Examples are as follows:
   ```sh
   mkdir -p $HOME/go/bin
   echo "export GOPATH=$HOME/go" >> ~/.bash_profile
   echo "export GOBIN=$GOPATH/bin" >> ~/.bash_profile
   echo "export PATH=$PATH:$GOBIN" >> ~/.bash_profile
   source ~/.bash_profile
   ```

   Note: `OKChain` is based on `Go1.12.1+`

   ### Install OKChain 
   We install `OKChain` as below. We use the version `v0.1.0` here.

   > Note:
   > `v0.1.0` is the version of `OKChain` used by the testnet.

   ```sh
   mkdir -p $GOPATH/src/github.com/ok-chain
   cd $GOPATH/src/github.com/ok-chain
   git clone https://github.com/ok-chain/okchain
   cd okchain && git checkout master
   make tools install
   git checkout v0.1.0
   ```
   -->


