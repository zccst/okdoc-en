Genesis File
------------

A genesis file is a JSON file which defines the initial state of your
blockchain. It can be seen as height 0 of your blockchain. The first
block, at height 1, will reference the genesis file as its parent.

The state defined in the genesis file contains all the necessary
information, like initial token allocation, genesis time, default
parameters, and more. The following are the details of the genesis file
of OKChain testnet (for omissions and deletions, please refer to `launch
repo <http://gitlab.okcoin-inc.com/dex/launch>`__):

.. code:: sh

    {
          "genesis_time": "2019-03-13T23:00:00Z",
          "chain_id": "okchain",
          "consensus_params": {
            "block": {
              "max_bytes": "22020096",
              "max_gas": "-1",
              "time_iota_ms": "1000"
            },
            "evidence": {
              "max_age": "100000"
            },
            "validator": {
              "pub_key_types": [
                "ed25519"
              ]
            }
          },
          "app_hash": "",
          "app_state": {   
            }
          }
    # ...

Let us take a look at the below information.

Genesis Time and Chain\_id
~~~~~~~~~~~~~~~~~~~~~~~~~~

The genesis\_time is defined at the top of the genesis file. It is a UTC
timestamp which specifies when the blockchain is due to start. At this
time, genesis validators are supposed to come online and start
participating in the consensus process. The blockchain starts to
generate blocks when more than 2/3rd of the genesis validators (weighted
by voting power) are online.

Note: Genesis validators are the first validators participating in the
consensus process on OKchain network From the genesis file:

.. code:: sh

    "genesis_time": "2019-03-13T23:00:00Z"

The chain\_id is a unique identifier for your chain. It helps
differentiate between different chains using the same version of the
software. chain\_id on OKChain testnet is as follows:

.. code:: sh

    "chain_id": "okchain",

