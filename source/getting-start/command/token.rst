Token
=====

Token attributes

+------------------+-------------------+-------------------------------------------------------------+
| Name             | Type              | Description                                                 |
+==================+===================+=============================================================+
| Symbol           | string            | unique token ticker, eg. bcoin-y60                          |
+------------------+-------------------+-------------------------------------------------------------+
| OriginalSymbol   | string            | original token ticker entered by the user, eg. bcoin        |
+------------------+-------------------+-------------------------------------------------------------+
| Desc             | string            | token description limited to 256 bytes                      |
+------------------+-------------------+-------------------------------------------------------------+
| WholeName        | string            | full token name                                             |
+------------------+-------------------+-------------------------------------------------------------+
| TotalSupply      | int64             | total token supply                                          |
+------------------+-------------------+-------------------------------------------------------------+
| Owner            | string(address)   | token owner                                                 |
+------------------+-------------------+-------------------------------------------------------------+
| Mintable         | Bool              | indicate whether whether to increase the supply of tokens   |
+------------------+-------------------+-------------------------------------------------------------+

Dex supports the token issuance function. Commands are as follows:

.. code:: bash

    okchaincli tx token [command]

Secondary sub-commands mainly include the following 7 functions

1. Issue tokens：
-----------------

parameter description:
~~~~~~~~~~~~~~~~~~~~~~

+----------------------+----------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Name                 | Type     | **Description**                                                                                                                                                                                                              |
+======================+==========+==============================================================================================================================================================================================================================+
| symbol               | string   | symbol is a non-case-sensitive token ticker limited to 6 alphanumeric characters, but the first character cannot be a number, eg. “bcoin” since the system will automatically add 3 random characters, such as "bcoin-gf6"   |
+----------------------+----------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| desc                 | string   | token description limited to 256 bytes                                                                                                                                                                                       |
+----------------------+----------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| total-supply(-n)     | int      | total token supply                                                                                                                                                                                                           |
+----------------------+----------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| whole-name(-w)       | string   | full token name                                                                                                                                                                                                              |
+----------------------+----------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| mintable             | string   | indicate whether to increase the supply of tokens                                                                                                                                                                            |
+----------------------+----------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| from                 | string   | token owner                                                                                                                                                                                                                  |
+----------------------+----------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| broadcast-mode(-b)   | string   | transaction broadcast modes (sync\|async\|block)                                                                                                                                                                             |
+----------------------+----------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Example:
~~~~~~~~

Issue a new token

.. code:: bash

    okchaincli tx token issue [flags]

Successful response:
~~~~~~~~~~~~~~~~~~~~

::

    okchaincli tx token issue --from alice --symbol bcoin -n 200000 -w 'bcoin' --desc 'blockchain coin' -b block --mintable  
    # example  
    {
      "height": "340949",
      "txhash":     "02978378301B38883C5CA9E17997B5CC5701DED817BA8B516851B1F706BD2544",
      "raw_log": "[{"msg_index":"0","success":true,"log":""}]",
      "logs": [
        {
          "msg_index": "0",
          "success": true,
          "log": ""
        }
      ],
      "tags": [
        {
          "key": "fee",
          "value": "20000.00000000 okt"
        },
        {
          "key": "action",
          "value": "issue"
        },
        {
          "key": "symbol",
          "value": "bcoin-254"
        }
      ]
    }

2. Increase the supply of tokens：
----------------------------------

Parameter description:
~~~~~~~~~~~~~~~~~~~~~~

+----------+----------+--------------------------------+
| Name     | Type     | **Description**                |
+==========+==========+================================+
| amount   | int      | amount of increase in supply   |
+----------+----------+--------------------------------+
| symbol   | string   | token symbol                   |
+----------+----------+--------------------------------+
| from     | string   | token owner                    |
+----------+----------+--------------------------------+

Example:
~~~~~~~~

A certain amount of supply of tokens issued is increased and only tokens
with mintable parameters upon issuance can be issued

.. code:: bash

    okchaincli tx token mint [flags]

Successful response:
~~~~~~~~~~~~~~~~~~~~

::

    okchaincli tx token mint --amount 10000000 --symbol okt --from alice -b block
    # Example output
    {
      "height": "341001",
      "txhash": "D890F0A3140797410179270BFF5353B15AAF0C14847715319DA64499754BECF6",
      "raw_log": "[{\"msg_index\":\"0\",\"success\":true,\"log\":\"\"}]",
      "logs": [
         {
           "msg_index": "0",
           "success": true,
           "log": ""
         }
        ],
      "tags": [
         {
           "key": "fee",
           "value": "2000.00000000 okt"
         },
         {
           "key": "action",
           "value": "mint"
         }
       ]
    }

3. Burn tokens：
----------------

Parameter description:
~~~~~~~~~~~~~~~~~~~~~~

+----------+----------+---------------------------------------------------+
| Name     | Type     | Description                                       |
+==========+==========+===================================================+
| amount   | string   | amount of tokens burnt (decimal places allowed)   |
+----------+----------+---------------------------------------------------+
| symbol   | string   | token symbol                                      |
+----------+----------+---------------------------------------------------+
| from     | string   | token owner                                       |
+----------+----------+---------------------------------------------------+

Example:
~~~~~~~~

A certain amount of tokens issued are burnt

.. code:: bash

    okchaincli tx token burn [flags]

Successful response:
~~~~~~~~~~~~~~~~~~~~

::

    okchaincli tx token burn --from alice --symbol okt --amount 100.0 -b block
      # Example output
    {
      "height": "341036",
      "txhash": "DB72C94B7D42EAEEE0AC129488DC637B270B9E389FFA5FD483DE927DB92D928F",
      "raw_log": "[{\"msg_index\":\"0\",\"success\":true,\"log\":\"\"}]",
      "logs": [
        {
          "msg_index": "0",
          "success": true,
          "log": ""
        }
      ],
      "tags": [
        {
          "key": "fee",
          "value": "10.00000000 okt"
        },
        {
          "key": "action",
          "value": "burn"
        }
      ]
    }

4. Freeze tokens:
-----------------

Parameter description:
~~~~~~~~~~~~~~~~~~~~~~

+----------+----------+----------------------------------------------------+
| Name     | Type     | Description                                        |
+==========+==========+====================================================+
| amount   | string   | amount of tokens frozen (decimal places allowed)   |
+----------+----------+----------------------------------------------------+
| symbol   | string   | token symbol                                       |
+----------+----------+----------------------------------------------------+
| from     | string   | token owner                                        |
+----------+----------+----------------------------------------------------+

Example:
~~~~~~~~

The user freezes the tokens in his account

.. code:: bash

    okchaincli tx token freeze [flags]

Successful response:
~~~~~~~~~~~~~~~~~~~~

::

    okchaincli tx token freeze --from alice --symbol okt --amount 0.1 -b block
      # Example output
    {
      "height": "341062",
      "txhash": "1760D4D004FBA262AF77502C7DAA080D86CDFFD1335D924431530BE0D2207597",
      "raw_log": "[{\"msg_index\":\"0\",\"success\":true,\"log\":\"\"}]",
      "logs": [
        {
          "msg_index": "0",
          "success": true,
          "log": ""
        }
      ],
      "tags": [
        {
          "key": "fee",
          "value": "0.10000000 okt"
        },
        {
          "key": "action",
          "value": "freeze"
        }
      ]
    }

5. Unfreeze tokens：
--------------------

Parameter description:
~~~~~~~~~~~~~~~~~~~~~~

+----------+----------+------------------------------------------------------+
| Name     | Type     | Description                                          |
+==========+==========+======================================================+
| amount   | string   | amount of tokens unfrozen (decimal places allowed)   |
+----------+----------+------------------------------------------------------+
| symbol   | string   | token symbol                                         |
+----------+----------+------------------------------------------------------+
| from     | string   | token owner                                          |
+----------+----------+------------------------------------------------------+

Example:
~~~~~~~~

The user unfreezes the tokens in his account

.. code:: bash

    okchaincli tx token unfreeze [flags]

Successful response:
~~~~~~~~~~~~~~~~~~~~

::

      okchaincli tx token unfreeze --from alice --symbol okt --amount 0.1 -b block
      
      # Example output
      {
        "height": "341129",
        "txhash": "BDABBFE9262A5ED46F38920434717EC90BF883620A30460FAC9E959D425E7176",
        "raw_log": "[{\"msg_index\":\"0\",\"success\":true,\"log\":\"\"}]",
        "logs": [
          {
            "msg_index": "0",
            "success": true,
            "log": ""
          }
        ],
        "tags": [
          {
            "key": "fee",
            "value": "0.10000000 okt"
          },
          {
            "key": "action",
            "value": "unfreeze"
          }
        ]
      }

6. Query token information:
---------------------------

Example:
~~~~~~~~

Query token information

.. code:: bash

      okchaincli query token info <symbol>

Successful response:
~~~~~~~~~~~~~~~~~~~~

::

      # Example output
      {
        "desc": "blockchain coin",
        "symbol": "bcoin-254",
        "originalSymbol": "bcoin",
        "wholeName": "bcoin",
        "totalSupply": "200000",
        "owner": "okchain10q0rk5qnyag7wfvvt7rtphlw589m7frsmyq4ya",
        "mintable": true
      }

7. Transfer multiple tokens to users at the same time:
------------------------------------------------------

Example:
~~~~~~~~

Transfer multiple tokens to users at the same time and specify the
transfer files through --transfers-file. When --transfers-file is
specified, --transfers is ignored

.. code:: bash

    okchaincli tx token multi-send [flags]

Successful response:
~~~~~~~~~~~~~~~~~~~~

::

      okchaincli tx token multi-send --from alice --transfers '[{"to":"okchain106205vgqv4fnn0yqcq7y7j936pv4kznv99yw85","amount":"1okt,2btc-254"}]' -b block
      
      # Example output
      {
        "height": "341487",
        "txhash": "1FA997F9557156A36AC8E3E2B5932888973796ABD0FB6FCEB3581B3BDF495D6B",
        "raw_log": "[{\"msg_index\":\"0\",\"success\":true,\"log\":\"\"}]",
        "logs": [
          {
            "msg_index": "0",
            "success": true,
            "log": ""
          }
        ],
        "tags": [
          {
            "key": "fee",
            "value": "0.02000000 okt"
          },
          {
            "key": "action",
            "value": "multi-send"
          }
        ]
      }

8. Transfer token ownership:
----------------------------

We support the function where token ownership can be transferred to
another person. In order to ensure the security of token ownership
transfer, multi signatures are required to validate the transfer. The
process consists of the following 4 steps:

original owner(from) generates an unsigned tx：
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Example:
^^^^^^^^

.. code:: bash

    okchaincli tx token chown [flags]

Successful response:
^^^^^^^^^^^^^^^^^^^^

::

    # from alice to jack
    okchaincli tx token chown --from okchain1pck0wndww84wtppc0vz9mcuvv7j5lcg00yf3gp --to okchain1x045ccxnwpurav2d5e25k25383qpmsr73293w0 --symbol okt > unsignedTx.json

    # unsignedTx.json
    {
        "type": "auth/StdTx",
        "value": {
            "msg": [{
                "type": "token/Chown",
                "value": {
                    "from_address": "okchain1pck0wndww84wtppc0vz9mcuvv7j5lcg00yf3gp",
                    "to_address": "okchain1x045ccxnwpurav2d5e25k25383qpmsr73293w0",
                    "symbol": "okt",
                    "to_signature": {
                        "pub_key": null,
                        "signature": null
                    }
                }
            }],
            "signatures": null,
            "memo": ""
        }
    }

owner(to) signs to validate the transfer：
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Example:
^^^^^^^^

.. code:: bash

    okchaincli tx token multisigns unsignedTx.json

Successful response:
^^^^^^^^^^^^^^^^^^^^

::

    okchaincli tx token multisigns unsignedTx.json --from jack > signedTx1.json -y

    # signedTx1.json
    {
        "type": "auth/StdTx",
        "value": {
            "msg": [{
                "type": "token/Chown",
                "value": {
                    "from_address": "okchain1pck0wndww84wtppc0vz9mcuvv7j5lcg00yf3gp",
                    "to_address": "okchain1x045ccxnwpurav2d5e25k25383qpmsr73293w0",
                    "symbol": "okt",
                    "to_signature": {
                        "pub_key": {
                            "type": "tendermint/PubKeySecp256k1",
                            "value": "A6zP2A10dBxpR6oNKD8Q+j285lJ63PEecFyK19mcYodh"
                        },
                        "signature": "lfL+i1YRtddruRpd2PloI7Ss1CYTyu5bBz4AmBm9eVYEvmghUqNrkERm12fetiGh1ux1R/WiXijeomjFQHNkrQ=="
                    }
                }
            }],
            "signatures": null,
            "memo": ""
        }
    }

original owner(from) signs：
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Example:
^^^^^^^^

.. code:: bash

    okchaincli tx sign [flags]

Successful response:
^^^^^^^^^^^^^^^^^^^^

::

    okchaincli tx sign --from alice signedTx1.json > signedTx.json -y

    # signedTx.json
    {
      "type": "auth/StdTx",
      "value": {
        "msg": [
          {
            "type": "token/Chown",
            "value": {
              "from_address": "okchain1pck0wndww84wtppc0vz9mcuvv7j5lcg00yf3gp",
              "to_address": "okchain1x045ccxnwpurav2d5e25k25383qpmsr73293w0",
              "symbol": "okt",
              "to_signature": {
                "pub_key": {
                  "type": "tendermint/PubKeySecp256k1",
                  "value": "A6zP2A10dBxpR6oNKD8Q+j285lJ63PEecFyK19mcYodh"
                },
                "signature": "lfL+i1YRtddruRpd2PloI7Ss1CYTyu5bBz4AmBm9eVYEvmghUqNrkERm12fetiGh1ux1R/WiXijeomjFQHNkrQ=="
              }
            }
          }
        ],
        "signatures": [
          {
            "pub_key": {
              "type": "tendermint/PubKeySecp256k1",
              "value": "A/EpsisD1SuP2aMjErP/RmCiPgFbMQcd2ADUM4dCmYvk"
            },
            "signature": "5G3e8VjKulShcgbp3gL4Wfk3QhFVRyQ/YgVdCsokJTplAT58P5jfkkn0Qjwuv3kKNIOYC8k1n4jhauqM0WCZWQ=="
          }
        ],
        "memo": ""
      }
    }

tx upon multi-signature broadcast：
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Example:
^^^^^^^^

.. code:: bash

    okchaincli tx broadcast signedTx.json

Successful response:
^^^^^^^^^^^^^^^^^^^^

::

    okchaincli tx broadcast signedTx.json -b block -y

    # Example
    {
      "height": "136",
      "txhash": "C59A61BE30A15D57702C32C2C2DBBEA740B372135E89831205C51B2880CBA0B9",
      "raw_log": "[{\"msg_index\":\"0\",\"success\":true,\"log\":\"\"}]",
      "logs": [
        {
          "msg_index": "0",
          "success": true,
          "log": ""
        }
      ],
      "tags": [
        {
          "key": "fee",
          "value": "10.00000000 okt"
        },
        {
          "key": "action",
          "value": "transfer"
        }
      ]
    }

The transfer of token ownership is successful only after the original
owner(from) and the owner(to) sign upon and after the transfer.
