1. What is OKChain
------------------

1.1 Introduction of OKChain
~~~~~~~~~~~~~~~~~~~~~~~~~~~

OKChain is a set of business chains developed by OKEx with an aim to
establish a secure and efficient Defi infrastructure. As our first
self-developed chain, it is used to provide users with a more
comprehensive credit enhancement service given that efficiency issues
have been solved, and to cater for users’ demand for credit enhancement
services while they trade crypto assets.

OKChain currently includes two executable programs, okchaind and
okchaincli.

-  okchaind: OKChain’s background program that is used to run full nodes
   on OKChain
-  okchaincli: OKChain’s command-line client that is used to interact
   with full nodes on OKChain

The following modules are mainly included:

-  x/auth：account module
-  x/token：token module
-  x/order：order module
-  x/gov：governance module
-  x/staking：staking module
-  x/distribution：distribution module
-  x/upgrade：upgrade module
-  x/backend：backend module

2. OKChain
----------

2.1 okchaind backend application
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

okchaind is used to initialize and activate full nodes on OKChain. It is
OKChain's backend application. For further details, please refer to
``okchaind -h`` as follows:

.. code:: sh

    $ okchaind -h
    OKChain Daemon

    Usage:
      okchaind [command]

    Available Commands:
      init                Initialize genesis config, priv-validator file, and p2p-node file
      collect-gentxs      Collect genesis txs and output a genesis.json file
      testnet             Initialize files for a Okdexd testnet
      gentx               Generate a genesis tx carrying a self delegation
      add-genesis-account Adds an account to the genesis file
      validate-genesis    validates the genesis file at the default location or at the location passed as an arg
      start               Run the full node
      unsafe-reset-all    Resets the blockchain database, removes address book files, and resets priv_validator.json to the genesis state

      tendermint          Tendermint subcommands
      export              Export state to JSON

      version             Print the app version
      help                Help about any command

    Flags:
          --enable_distr false   Enable distribution module (default false)
      -h, --help                 help for okchaind
          --home string          directory for config and data (default "$HOME/.okchaind")
          --log_file string      Log file (default "$HOME/.okchaind/okchaind.log")
          --log_level string     Log level (default "main:info,state:info,*:error")
          --log_stdout           Print log to stdout, rather than a file (default true)
          --passwd string        Pass word of sender (default "12345678")
          --production_mode      Run in production mode or development mode. (default "false")
          --trace                print out full stack trace on errors

    Use "okchaind [command] --help" for more information about a command.

2.2 okchaincli client
~~~~~~~~~~~~~~~~~~~~~

okchaincli is a command-line client of OKChain that offers rich
functions to interact with the backend application of OKChain. It mainly
includes two types of functions: tx function and query function. For
further information, please refer to ``okchaincli -h`` as follows:

.. code:: sh

    $ okchaincli -h
    OKChain Client

    Usage:
      okchaincli [command]

    Available Commands:
      status      Query remote node for status
      config      Create or query an OKChain CLI configuration file
      query       Querying subcommands
      tx          Transactions subcommands
      backend     backend subcommands


      keys        Add or view local private keys

      version     Print the app version
      help        Help about any command

    Flags:
          --chain-id string   Chain ID of tendermint node
      -e, --encoding string   Binary encoding (hex|b64|btc) (default "hex")
      -h, --help              help for okchaincli
          --home string       directory for config and data (default "/Users/hanxueyang/.okchaincli")
      -o, --output string     Output format (text|json) (default "text")
          --passwd string     Pass word of sender (default "12345678")
          --trace             print out full stack trace on errors

    Use "okchaincli [command] --help" for more information about a command.

Meanwhile, users can also manage local private keys through the
sub-command ``okchaincli keys``.
