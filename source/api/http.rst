
HTTP API
--------

The OKChain HTTP API provides access to an OKChain Chain node deployment
and market data services.

1. Accounts
-----------

Obtain the account address
~~~~~~~~~~~~~~~~~~~~~~~~~~

http API:

.. code:: http

    GET okchain/v1/accounts/{address}

API parameters:

+-----------+----------+------------+-------------------+
| Name      | Type     | Required   | Mark              |
+===========+==========+============+===================+
| address   | String   | true       | account address   |
+-----------+----------+------------+-------------------+

Response:

::

        {
          "code": 0,
          "msg": "",
          "detailMsg": "",
          "data": {
            "address": "okchain1gaszdnrmghask7kz8n2tdxq0wk2a69z9336mjh",
            "currencies": [
              {
                "symbol": "okt",
                "available": "10000000.00000000",
                "freeze": "0",
                "locked": "0"
              }
            ]
          }
        }


Obtain information of all cryptocurrencies of a user
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

http API:

.. code:: http

    GET  okchain/v1/accounts/{address}?show=all

API parameters:

+-----------+----------+------------+---------------------------------------------------------------------------+
| Name      | Type     | Required   | Mark                                                                      |
+===========+==========+============+===========================================================================+
| address   | String   | true       | account address                                                           |
+-----------+----------+------------+---------------------------------------------------------------------------+
| show      | String   | false      | whether to show all cryptocurrencies, all or partial, default = partial   |
+-----------+----------+------------+---------------------------------------------------------------------------+

Response:

.. code:: json

    {
        "code": 0,
        "data": {
            "address": "okchain10q0rk5qnyag7wfvvt7rtphlw589m7frsmyq4ya",
            "currencies": [{
                "symbol": "acoin",
                "available": "10000000.00000000",
                "freeze": "0",
                "locked": "0"
              }, {
                "symbol": "bcoin",
                "available": "10000000.00000000",
                "freeze": "0",
                "locked": "0"
            }]
        },
        "detailMsg": "",
        "msg": ""
    }

Obtain information on a single cryptocurrency of a user
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

http API:

.. code:: http

    GET okchain/v1/accounts/{address}?symbol="bcoin"

API parameters:

+-----------+----------+------------+-------------------+
| Name      | Type     | Required   | Mark              |
+===========+==========+============+===================+
| address   | String   | true       | account address   |
+-----------+----------+------------+-------------------+
| symbol    | String   | true       | cryptocurrency    |
+-----------+----------+------------+-------------------+

Response:

.. code:: json

    {
        "code": 0,
        "data": {
            "address": "okchain10q0rk5qnyag7wfvvt7rtphlw589m7frsmyq4ya",
            "currencies": [{
                "symbol": "acoin",
                "available": "10000000.00000000",
                "freeze": "0",
                "locked": "0"
            }, {
          "symbol": "bcoin",
                "available": "10000000.00000000",
                "freeze": "0",
                "locked": "0"
        }]
        },
        "detailMsg": "",
        "msg": ""
    }

2. Market Data
--------------

Obtain information on all cryptocurrencies
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

http API:

.. code:: http

    GET okchain/v1/tokens

API parameters: Null

Response:

.. code:: json

    {
        "code": 0,
        "data": [{
        "desc": "bcoin",
            "symbol": "bcoin",
            "orginalSymbol": "bcoin",
        "wholeName": "bcoin",
            "totalSupply": "210000000",
            "owner": "okchain1kyh26rw89f8a4ym4p49g5z59mcj0xs4j045e39",
            "mintable": true
        }],
        "detailMsg": "",
        "msg": ""
    }

Obtain information on a single cryptocurrency
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

http API:

.. code:: http

    GET okchain/v1/token/{symbol}

API parameters:

+----------+----------+------------+-----------------------+
| Name     | Type     | Required   | Mark                  |
+==========+==========+============+=======================+
| symbol   | String   | true       | cryptocurrency name   |
+----------+----------+------------+-----------------------+

Response:

.. code:: json

    {
        "code": 0,
        "msg": "",
        "detailMsg": "",
        "data": {
            "desc": "",
            "symbol": "bcoin-805",
            "originalSymbol": "bcoin",
            "wholeName": "bcoin",
            "totalSupply": "200000",
            "owner": "okchain10q0rk5qnyag7wfvvt7rtphlw589m7frsmyq4ya",
            "mintable": false
        }
    }

Obtain information on all trading pairs
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

http API:

.. code:: http

    GET okchain/v1/products

API parameters: Null

Response:

.. code:: json

    {
        "code": 0,
        "msg": "",
        "detailMsg": "",
        "data": [{
            "baseAssetSymbol": "acoin",
            "quoteAssetSymbol": "okt",
            "price": "10.00000000",
            "maxPriceDigit": "1",
            "maxSizeDigit": "2",
            "minTradeSize": "0.10000000",
            "tokenPairId": "0"
        }]
    }

Obtain information on market depth
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

http API:

.. code:: http

    GET okchain/v1/order/depthbook

API parameters:

+--------------------+----------+------------+--------------------------------------+
| Name               | Type     | Required   | Mark                                 |
+====================+==========+============+======================================+
| product            | String   | true       | pair information, eg:btc\_okt        |
+--------------------+----------+------------+--------------------------------------+
| [STRIKEOUT:size]   | Number   | false      | tier(maxSize:200), v1 fixed at 200   |
+--------------------+----------+------------+--------------------------------------+

Response:

.. code:: json

    {
        "code": 0,
        "data": {
            "asks": [{
                #Seller depth  Order: asc
                "price": "string", #Price
                "quantity": "string" #Quantity
            }],
            "bids": [{
                #Buyer depth Order: desc
                "price": "string",#Price
                "quantity": "string"#Quantity
            }]
        },
        "msg": "string"
    }

Obtain candlestick data
~~~~~~~~~~~~~~~~~~~~~~~

http API:

.. code:: http

    GET okchain/v1/candles/{product}?granularity=21600&size=1000

API parameters:

\|Name \|Type \|Required\|Example\|Mark\| \|:---:\|:---:\|:------:\|:---
: \|:-------:\| \|product\|String\| true\|bcoin\_okt\|pair Name\|
\|granularity\|int\|false\|18060\|time granularity, time granularity,
unit=second, default = 60,
eg.[60/180/300/900/1800/3600/7200/14400/21600/43200/86400/604800]equal
to{1min,3min,5min,15min,30min,1hour,2hour,4hour,6hour,12hour,1day,1week}\|
\|size\|int\|false\|100\|number of candlestick data size: up to 1000
pieces of candlestick data, default = 100 \|

Response:

.. code:: json

    {
        "code": 0,#0:Successful, others: failed
        "data": [[
            "2018-07-12T04:00:00.000Z",#Creation time
            "6343.3587"#Open
            "6345.0453",#High
            "6142.2336",#Low
            "6186.8354",#Close
            "8429.75582698",#Volume
        ]],
        "detailMsg": "string",
        "msg": "string"
    }

Obtain all market data
~~~~~~~~~~~~~~~~~~~~~~

http API:

.. code:: http

    GET okchain/v1/tickers

API parameters:

+---------+--------+------------+--------------------------------------+
| Name    | Type   | Required   | Mark                                 |
+=========+========+============+======================================+
| count   | int    | false      | number of data size, default = 100   |
+---------+--------+------------+--------------------------------------+

Response:

.. code:: json

    {
        "code": 0,
        "data": [{
            "close": "29.777",#24 hour close
            "high": "55.44", #High
            "low": "22.22", #Low
            "open": "55.44",#24 hour open
            "price": "29.777",#Latest
            "product": "bcoin-2ac_okt",#Pair
            "symbol": "bcoin-2ac_okt",
            "timestamp": "2019-07-25T09:49:04.954Z",#Timestamp
            "volume": "266.64",#Volume
        }],
        "detailMsg": "",
        "msg": ""
    }

Obtain the latest transaction history of a pair
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

http API:

.. code:: http

    GET okchain/v1/matches

API parameters:

+-----------+----------+------------+-----------------------------------------+
| Name      | Type     | Required   | Mark                                    |
+===========+==========+============+=========================================+
| product   | String   | true       | pair                                    |
+-----------+----------+------------+-----------------------------------------+
| start     | int      | false      | start date (timestamp, unit = second)   |
+-----------+----------+------------+-----------------------------------------+
| end       | int      | false      | end date (timestamp, unit = second)     |
+-----------+----------+------------+-----------------------------------------+
| page      | int      | false      | page number                             |
+-----------+----------+------------+-----------------------------------------+
| perPage   | int      | false      | size per page                           |
+-----------+----------+------------+-----------------------------------------+

Response:

::

    {
      "code": 0,
      "msg": "",
      "detailMsg": "",
      "data": {
        "data": [
            {
              "timestamp": 1559790137,
              "blockHeight": 386355,
              "product": "acoin-564_okt",
              "price": 3,
              "volume": 0.25
            },
            {
              "timestamp": 1559789554,
              "blockHeight": 386159,
              "product": "acoin-564_okt",
              "price": 1.9999,
              "volume": 2.9999
            },
            {
              "timestamp": 1559788804,
              "blockHeight": 385931,
              "product": "acoin-564_okt",
              "price": 1,
              "volume": 1
            }
        ],
        "paramPage": {
            "page": 1,
            "perPage": 50,
            "total": 3
        }
      }
    }

3. Transactions
---------------

Placement (in base)
~~~~~~~~~~~~~~~~~~~

http API:

.. code:: http

    POST okchain/v1/txs

post order:

::


    {
        "tx": {
            "msg": [{
                "type": "order/new",
                "value": {
                    "BatchNumber": "0",//Optional (to be omitted), for backend testing
                    "Sender": "okchain1t2cvfv58764q4wdly7qjx5d2z89lewvwq2448n",//Sender address
                    "Product": "mycoin_okt",//Trading pair
                    "Side": "BUY",
                    "Price": "1",//Price
                    "Quantity": "0.1"//Quantity
                }
            }],
            "signatures": [{
                "pub_key": {
                    "type": "tendermint/PubKeySecp256k1",
                    "value": "AsfvubxdC51g5kpHh3ibtjEsm0INdvrpOgrzw/BcGExK"
                },
                "signature": "xce6VKVxf5nmOumEqVK2n8QiZG3mBi9P+SGTvDCHLAZxP9p8/zS/+VhVzWGI7tppW2uGNz/iToubTvHTd4y9KA=="
            }],
            "memo": "jin tian ye yao jia you ya"
        },
        "mode": "block"
    }

Signature: (use the private key to generate a signature on the
information signature)

::

    {
        "account_number": "0",
        "chain_id": "okchain",
        "memo": "jin tian ye yao jia you ya",
        "msgs": [{
             "BatchNumber": "0",
             "Price": "1",
             "Product": "mycoin_okt",
             "Quantity": "0.1",
             "Sender": "okchain1t2cvfv58764q4wdly7qjx5d2z89lewvwq2448n",
             "Side": "BUY"
        }],
        "sequence": “4”
    }

Response:

.. code:: json

    {
        "height": "97",
        "txhash": "E270C8DB83C1C1E03C090656BB96A8539B94A19F4C6F6D1A1E10428C6BA0CA8B",
        "logs": [{
            "msg_index": "0",
            "success": true,
            "log": ""
        }],
        "gas_wanted": "200000",
        "gas_used": "55151",
        "tags": [{
            "key": "action",
            "value": "new"
            }, {
                "key": "orderId",
                "value": "ID0000000097-1"
            }, {
                "key": "batch_number",//Optional
                "value": "1"
            }
        }]
    }

Taker (in base)
~~~~~~~~~~~~~~~

http API:

.. code:: http

    POST okchain/v1/txs

post order:

::


    {
        "tx": {
            "msg": [{
                "type": "order/cancel",
                "value": {
                    "Sender": "cosmos1ln5zguv3pccm59e4dmdtjxuw24a0cv7p4v8cl8",
                    "OrderId": "ID0000000006-0000"
                }
            }],
            "signatures": [{
                "pub_key": {
                    "type": "tendermint/PubKeySecp256k1",
                    "value": "AtXflms2umhaIZ4MX4pVFr23y3im37LXz+yvUNnDirtJ"//Public key
                },
                "signature": "/bPROoTE3yBBT9tLb6MzDIdHQHUeRvASRteoJ2aDW00/xEkUqS0zzWxf6GF87Fu1f3uNXle5b0rYOxqbi5IeuA=="
            }],
            "memo": ""//Remarks
        },
        "mode": "block"//sync mode returns after checkTx, async mode returns immediately, block mode returns after block generation
    }

Signature:

::


    {
        "account_number": "0",//Account serial number on blockchain
        "chain_id": "okchain",
        "memo": "",
        "msgs": [{
            "OrderId": "ID0000000006-0000",
            "Sender": "cosmos1ln5zguv3pccm59e4dmdtjxuw24a0cv7p4v8cl8"
        }],
        "sequence": "13"//The account sends transaction serial number
    }

Response:

::


    {
        "height": "99",//block height
        "txhash": "DD7B4552433912580431F58BBABADF93F50C511B9F7BDC711CFD81B6DD65364B",//transaction hash
        "logs": [{
            "msg_index": "0",
            "success": true,
            "log": ""
        }],
        "gas_wanted": "200000", // maximum gas wanted
        "gas_used": "91073", // gas used
        "tags": [{
            "key": "action",
            "value": "cancel"
            }, {
                "key": "orderId",
                "value": "ID0000000097-1"
            }
        }]
    }

Transfer (in base)
~~~~~~~~~~~~~~~~~~

http API:

.. code:: http

    POST okchain/v1/txs

post order:

::


    {
        "tx": {
            "msg": [{
                "type": "cosmos-sdk/MsgSend",
                "value": {
                    "from_address": "cosmos1jckxfddx3w8m288srv4m4ueyxpas2fuc3wclru",
                    "to_address": "cosmos1c97ekk5a5907a0wkd6wxy903sytnytr4mjfgze",
                    "amount": [{
                        "denom": "okt",
                        "amount": "1000000000000000000"
                    }]
                }
            }],
            "signatures": [{
                "pub_key": {
                    "type": "tendermint/PubKeySecp256k1",
                    "value": "Ar2qgMNVp0DHOuO3TRBHtirkEwV5LXign7kJomL6WeX2"
                },
                "signature": "wy4e2eQfJ0oew6Dta0SAV7qAmsc6YUDwYUqiIj1htdFVREGQz0inVNOS4YEuhLbFlV9ZvHMASCOf1hzqnhsB5w=="
            }],
            "memo": ""
        },
        "mode": "block"
    }

Signature: (use the private key to generate a signature on the
information signature)

.. code:: json

    {
        "account_number": "0",
        "chain_id": "okchain",
        "memo": "",
        "msgs": [{
            "type": "cosmos-sdk/MsgSend",
            "value": {
                "amount": [{
                    "amount": "1000000000000000000",
                    "denom": "okt"
                }],
                "from_address": "cosmos1jckxfddx3w8m288srv4m4ueyxpas2fuc3wclru",
                "to_address": "cosmos1c97ekk5a5907a0wkd6wxy903sytnytr4mjfgze"
            }
        }],
        "sequence": "13"
    }

Response:

.. code:: json

    {
        "height": "96",
        "txhash": "24EEA9C89959509F945792DD0AFD8A2064444CA3E863E2B7C6D78ED646FF8AAF",
        "logs": [
            {
                "msg_index": "0",
                "success": true,
                "log": ""
            }
        ],
        "gas_wanted": "200000",
        "gas_used": "39218",
        "tags": [{
            "key": "action",
            "value": "send"
            }, {
                "key": "sender",
                "value": "okchain1t2cvfv58764q4wdly7qjx5d2z89lewvwq2448n"
            }, {
                "key": "recipient",
                "value": "okchain1ejwsk9wgwrcwgmee785vjf2a7su7erryhet8eh"
        }]
    }

Unfilled order
~~~~~~~~~~~~~~

http API:

.. code:: http

    GET okchain/v1/order/list/open？product=mycoin_okt&address=cosmos1hghms6dtm8quxegrkcnw4wnzj5e5sc4am0gxyr&start=1556541851&end=1556541851&page=0&perPage=50

API parameters:

+-----------+----------+------------+-------------------+
| Name      | Type     | Required   | Mark              |
+===========+==========+============+===================+
| product   | String   | false      | pair              |
+-----------+----------+------------+-------------------+
| address   | String   | true       | address           |
+-----------+----------+------------+-------------------+
| start     | int      | false      | start timestamp   |
+-----------+----------+------------+-------------------+
| end       | int      | false      | end timestamp     |
+-----------+----------+------------+-------------------+
| side      | string   | false      | BUY/SELL          |
+-----------+----------+------------+-------------------+
| page      | int      | false      | page id           |
+-----------+----------+------------+-------------------+
| perPage   | int      | false      | size per page     |
+-----------+----------+------------+-------------------+

Response:

Parameters: No product parameters are sent when obtaining information on
all trading pair orders

Response:

.. code:: json

    {
        "code": "0",
        "msg": "",
        "detailMsg": "",
        "data": {
            "data":[
                {
                    "TxHash":"2144D0F85B67D9508066004400BF8044010ED5FC4B43417F9A44CDC3EBAD9765",
                    "OrderId": "O0000000008-0000",
                    "Sender": "cosmos1hghms6dtm8quxegrkcnw4wnzj5e5sc4am0gxyr",
                    "Product": "mycoin_okt",
                    "Side": "BUY",
                    "Price": "10.000000000000000000",
                    "Quantity": "1.100000000000000000",
                    "Status": "0",  //(0-5) -> (Open, Filled, Cancelled, Expired,
                    // PartialFilledCancelled, PartialFilledExpired)
                    "FilledAvgPrice": "10.000000000000000000",
                    "RemainQuantity": "0.100000000000000000",
                    "Timestamp": "1553842734"
                },
            ],
            "paramPage": {
                "total": "3",
                "page": 1,
                "perPage": 50,
            }
        }
    }

Past order
~~~~~~~~~~

http API:

.. code:: http

    GET okchain/v1/order/list/closed

API parameters:address, product, start, end, page, perPage. No product
parameters are sent when obtaining information on all trading pair
orders

+--------------+----------+------------+----------------------------------------------------+
| Name         | Type     | Required   | Mark                                               |
+==============+==========+============+====================================================+
| product      | String   | false      | pair                                               |
+--------------+----------+------------+----------------------------------------------------+
| address      | String   | true       | address                                            |
+--------------+----------+------------+----------------------------------------------------+
| side         | String   | false      | Need "BULL","SELL" even if the string is absent    |
+--------------+----------+------------+----------------------------------------------------+
| hideNoFill   | int      | false      | cancel orders or overdue orders 0:Open 1: Hidden   |
+--------------+----------+------------+----------------------------------------------------+
| start        | int      | false      | start timestamp                                    |
+--------------+----------+------------+----------------------------------------------------+
| end          | int      | false      | end timestamp                                      |
+--------------+----------+------------+----------------------------------------------------+
| page         | int      | false      | page id                                            |
+--------------+----------+------------+----------------------------------------------------+
| perPage      | int      | false      | size per page                                      |
+--------------+----------+------------+----------------------------------------------------+

Response:

.. code:: json

    {
        "code": "0",
        "msg": "",
        "detailMsg": "",
        "data": {
            "data":[
                {
                    "TxHash": "2144D0F85B67D9508066004400BF8044010ED5FC4B43417F9A44CDC3EBAD9765",
                    "OrderId": "O0000000008-0000",
                    "Sender": "cosmos1hghms6dtm8quxegrkcnw4wnzj5e5sc4am0gxyr",
                    "Product": "mycoin_okt",
                    "Side": "BUY",
                    "Price": "10.000000000000000000",
                    "Quantity": "1.100000000000000000",
                    "Status": "0",  //(0-5) -> (Open, Filled, Cancelled, Expired,
                     // PartialFilledCancelled, PartialFilledExpired)
                    "FilledAvgPrice": "10.000000000000000000",
                    "RemainQuantity": "0.100000000000000000",
                    "Timestamp": "1553842734"
                },
            ],
        "paramPage": {
            "total": "3",
            "page": 1,
            "perPage": 50,
        }
    }

Transaction history on-chain
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

http API:

.. code:: http

    GET okchain/v1/block_tx_hashes/{blockHeight}

parameters: blockHeight, int type

response: txHash table，string type

::

        [
            "hash1",
            "hash2",
            ...
        ]

Fee history
~~~~~~~~~~~

http API:

.. code:: http

    GET okchain/v1/fees

API parameters:

+-----------+----------+------------+-------------------+
| Name      | Type     | Required   | Mark              |
+===========+==========+============+===================+
| address   | String   | true       | account address   |
+-----------+----------+------------+-------------------+
| page      | int      | false      | page id           |
+-----------+----------+------------+-------------------+
| perPage   | int      | false      | size per page     |
+-----------+----------+------------+-------------------+

Response:

.. code:: json

    {
        "code": 0,
        "msg": "",
        "detailMsg": "",
        "data": {
            "data": [
                {
                    "address": "okchain1lzekrp7dezrs940m7c0nnhjvyhlzppnaf6vjsy",
                    "fee": "0.01250000okt",
                    "feeType": "transfer",  // Fee type: transfer/new/cancel/expire/deal
                    "timestamp": 1558407348
                }
            ],
        "paramPage": {
        "page": 1,
        "perPage": 50,
        "total": 1
            }
        }
    }

4. Orders
---------

Obtain transaction details
~~~~~~~~~~~~~~~~~~~~~~~~~~

http API:

.. code:: http

    GET okchain/v1/deals

API parameters:

+-----------+----------+------------+---------------------------------------------------+
| Name      | Type     | Required   | Mark                                              |
+===========+==========+============+===================================================+
| address   | String   | true       | account address                                   |
+-----------+----------+------------+---------------------------------------------------+
| product   | String   | false      | pair                                              |
+-----------+----------+------------+---------------------------------------------------+
| side      | String   | false      | need "BUY", "SELL" even if the string is absent   |
+-----------+----------+------------+---------------------------------------------------+
| start     | int      | false      | start date (timestamp, unit = second)             |
+-----------+----------+------------+---------------------------------------------------+
| end       | int      | false      | end date (timestamp, unit = second)               |
+-----------+----------+------------+---------------------------------------------------+
| page      | int      | false      | page id                                           |
+-----------+----------+------------+---------------------------------------------------+
| perPage   | int      | false      | size per page                                     |
+-----------+----------+------------+---------------------------------------------------+

Response:

.. code:: json

    {
        "code": 0,
        "msg": "",
        "detailMsg": "",
        "data": {
            "data": [
                {
                    "timestamp": 1558407585,
                    "blockHeight": 463,
                    "orderId": "ID0000000463-1",
                    "sender": "okchain15wv9q08rv0f8dg08scv2ps45hs6v8qx37466qj",
                    "product": "mycoin_okt",
                    "side": "SELL",
                    "price": 10,
                    "volume": 1,
                    "fee": "0.00400000okt"
                },
                {
                    "timestamp": 1558407585,
                    "blockHeight": 463,
                    "orderId": "ID0000000010-1",
                    "sender": "okchain1lzekrp7dezrs940m7c0nnhjvyhlzppnaf6vjsy",
                    "product": "mycoin_okt",
                    "side": "BUY",
                    "price": 10,
                    "volume": 1,
                    "fee": "0.00400000okt"
                }
            ],
            "paramPage": {
                "page": 1,
                "perPage": 50,
                "total": 2
            }
        }
    }

Obtain transaction records
~~~~~~~~~~~~~~~~~~~~~~~~~~

http API:

.. code:: http

    GET okchain/v1/transactions

API parameters:

+-----------+----------+------------+-----------------------------------------------------+
| Name      | Type     | Required   | Mark                                                |
+===========+==========+============+=====================================================+
| address   | string   | true       | user address                                        |
+-----------+----------+------------+-----------------------------------------------------+
| type      | int      | false      | order type, 1:Transfer, 2:NewOrder, 3:CancelOrder   |
+-----------+----------+------------+-----------------------------------------------------+
| start     | int      | false      | start date                                          |
+-----------+----------+------------+-----------------------------------------------------+
| end       | int      | false      | end date                                            |
+-----------+----------+------------+-----------------------------------------------------+
| page      | int      | false      | page id                                             |
+-----------+----------+------------+-----------------------------------------------------+
| perPage   | int      | false      | size per page                                       |
+-----------+----------+------------+-----------------------------------------------------+

Response:

.. code:: json

    {
        "code": 0,
        "msg": "",
        "detailMsg": "",
        "data": {
            "data": [
                {
                    "txHash":"3BEE2A0FDDD5EB077236879E139DC565580139F61ED6E391B2557D4A8F74BE83",
                    "type": 1,  // 1:Transfer, 2:NewOrder, 3:CancelOrder
                    "address": "okchain1lzekrp7dezrs940m7c0nnhjvyhlzppnaf6vjsy",
                    "symbol": "okt",
                    "side": 3,  // 1:buy, 2:sell, 3:from, 4:to
                    "quantity": "1.00000000",
                    "fee": "0.01250000okt",
                    "timestamp": 1558407348
                },
            ],
            "paramPage": {
                "page": 1,
                "perPage": 50,
                "total": 10
            }
        }
    }

5. Blocks
---------

Obtain the latest information on blocks
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

http API:

.. code:: http

    GET okchain/v1/blocks/latest

API parameters: Null

Response:

::

        {
          "block_meta": {
            "block_id": {
              "hash": "BF623CD9248E2721C12F757A9AAD505DACAD6166903AB0D4E7A6669B4E02BA84",
              "parts": {
                "total": "1",
                "hash": "368C05B48E428C71FCB0C5E2962BD1DC9C0BEC96759D5733C0F141FA7EA7C1A1"
              }
            },
            "header": {
              "version": {
                "block": "10",
                "app": "0"
              },
              "chain_id": "okchain",
              "height": "433",
              "time": "2019-07-23T06:57:30.775579Z",
              "num_txs": "0",
              "total_txs": "18",
              "last_block_id": {
                "hash": "0DBD77228438CA65F11DD675428E4B7DC9904AC11A9C9AB5D8182C1A250F0AF1",
                "parts": {
                  "total": "1",
                  "hash": "9222C8B073CA130AB057467DD63E45E556DA2314F2EC7CA7B0ACDC738170CCD5"
                }
              },
              "last_commit_hash": "761C584E0EF03D7812AB16B2A9DE27BB5E6DA954BC19F32D303A634ADE84DB6E",
              "data_hash": "",
              "validators_hash": "DEFD0C2394B21CF2DD2A49054E968C8754AB0CD20F31804028FA499A40358B19",
              "next_validators_hash": "DEFD0C2394B21CF2DD2A49054E968C8754AB0CD20F31804028FA499A40358B19",
              "consensus_hash": "048091BC7DDC283F77BFBF91D73C44DA58C3DF8A9CBC867405D8B7F3DAADA22F",
              "app_hash": "F8F901256CA9F12C253BB6E79144473BF41476A1BB49CA202A788D19CBD65683",
              "last_results_hash": "",
              "evidence_hash": "",
              "proposer_address": "D4640375843B281A9656B3B755D0B227ACDE13D9"
            }
          },
          "block": {
            "header": {
              "version": {
                "block": "10",
                "app": "0"
              },
              "chain_id": "okchain",
              "height": "433",
              "time": "2019-07-23T06:57:30.775579Z",
              "num_txs": "0",
              "total_txs": "18",
              "last_block_id": {
                "hash": "0DBD77228438CA65F11DD675428E4B7DC9904AC11A9C9AB5D8182C1A250F0AF1",
                "parts": {
                  "total": "1",
                  "hash": "9222C8B073CA130AB057467DD63E45E556DA2314F2EC7CA7B0ACDC738170CCD5"
                }
              },
              "last_commit_hash": "761C584E0EF03D7812AB16B2A9DE27BB5E6DA954BC19F32D303A634ADE84DB6E",
              "data_hash": "",
              "validators_hash": "DEFD0C2394B21CF2DD2A49054E968C8754AB0CD20F31804028FA499A40358B19",
              "next_validators_hash": "DEFD0C2394B21CF2DD2A49054E968C8754AB0CD20F31804028FA499A40358B19",
              "consensus_hash": "048091BC7DDC283F77BFBF91D73C44DA58C3DF8A9CBC867405D8B7F3DAADA22F",
              "app_hash": "F8F901256CA9F12C253BB6E79144473BF41476A1BB49CA202A788D19CBD65683",
              "last_results_hash": "",
              "evidence_hash": "",
              "proposer_address": "D4640375843B281A9656B3B755D0B227ACDE13D9"
            },
            "data": {
              "txs": null
            },
            "evidence": {
              "evidence": null
            },
            "last_commit": {
              "block_id": {
                "hash": "0DBD77228438CA65F11DD675428E4B7DC9904AC11A9C9AB5D8182C1A250F0AF1",
                "parts": {
                  "total": "1",
                  "hash": "9222C8B073CA130AB057467DD63E45E556DA2314F2EC7CA7B0ACDC738170CCD5"
                }
              },
              "precommits": [
                {
                  "type": 2,
                  "height": "432",
                  "round": "0",
                  "block_id": {
                    "hash": "0DBD77228438CA65F11DD675428E4B7DC9904AC11A9C9AB5D8182C1A250F0AF1",
                    "parts": {
                      "total": "1",
                      "hash": "9222C8B073CA130AB057467DD63E45E556DA2314F2EC7CA7B0ACDC738170CCD5"
                    }
                  },
                  "timestamp": "2019-07-23T06:57:30.775579Z",
                  "validator_address": "6B6B879EEC588AC6D6C0A925DF40142558D92EF9",
                  "validator_index": "0",
                  "signature": "ZQWxt3dKDp7Rl6WuHJDcUr4HPrvDFf1pIUk7L/+f5hP5koL2NNM5GwjgzMzXfUXDfY6FvswXccut9150j/V2Dw=="
                },
                {
                  "type": 2,
                  "height": "432",
                  "round": "0",
                  "block_id": {
                    "hash": "0DBD77228438CA65F11DD675428E4B7DC9904AC11A9C9AB5D8182C1A250F0AF1",
                    "parts": {
                      "total": "1",
                      "hash": "9222C8B073CA130AB057467DD63E45E556DA2314F2EC7CA7B0ACDC738170CCD5"
                    }
                  },
                  "timestamp": "2019-07-23T06:57:30.775579Z",
                  "validator_address": "77E268D7F58CA2A9C81E27481DA5F8947E99E67A",
                  "validator_index": "1",
                  "signature": "lVo31wzOjdbW2LuMwoktxSoEXvfqdYp19uGqVfaLfRdlJIOcCFUXIFm8sM98qLLdZaILuQCfGzycpTUCiOhvBA=="
                },
                {
                  "type": 2,
                  "height": "432",
                  "round": "0",
                  "block_id": {
                    "hash": "0DBD77228438CA65F11DD675428E4B7DC9904AC11A9C9AB5D8182C1A250F0AF1",
                    "parts": {
                      "total": "1",
                      "hash": "9222C8B073CA130AB057467DD63E45E556DA2314F2EC7CA7B0ACDC738170CCD5"
                    }
                  },
                  "timestamp": "2019-07-23T06:57:30.877204Z",
                  "validator_address": "B576DAE9CEC142CD0E932F5821253B3DAE19B7B2",
                  "validator_index": "2",
                  "signature": "cAlEne+vWKBjDLwc9hcUYPRHRQvkWHbW8kCEHSBxdkYJJQq/c8Th1lqLRKGGGbM5ZHe6GjMWLyo88HpjmoVaDg=="
                },
                {
                  "type": 2,
                  "height": "432",
                  "round": "0",
                  "block_id": {
                    "hash": "0DBD77228438CA65F11DD675428E4B7DC9904AC11A9C9AB5D8182C1A250F0AF1",
                    "parts": {
                      "total": "1",
                      "hash": "9222C8B073CA130AB057467DD63E45E556DA2314F2EC7CA7B0ACDC738170CCD5"
                    }
                  },
                  "timestamp": "2019-07-23T06:57:30.570501Z",
                  "validator_address": "D4640375843B281A9656B3B755D0B227ACDE13D9",
                  "validator_index": "3",
                  "signature": "/R7mSWoj3qP1YlGMrHtmyxla4gjrWqnx0W57Bpy7knxR6jdFDIK8aWCiCKBm7T76FekvK/3wMg/FYuWB31GHBA=="
                }
              ]
            }
          }
        }


Obtain information on block height
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

http API:

.. code:: http

    GET okchain/v1/blocks/{height}

API parameters:

+----------+----------+------------+----------------+
| Name     | Type     | Required   | Mark           |
+==========+==========+============+================+
| height   | number   | true       | Block height   |
+----------+----------+------------+----------------+

Response:

::

       {
         "block_meta": {
           "block_id": {
             "hash": "AE7D7FC321447A7F63031E28FD55CD9FF885EE73C38C62F63706C2ED3623ECFF",
             "parts": {
               "total": "1",
               "hash": "0E3BE14D6711CEEC468D44D1DB6FF702E92ACA521E8121698DD8BD521F07794F"
             }
           },
           "header": {
             "version": {
               "block": "10",
               "app": "0"
             },
             "chain_id": "okchain",
             "height": "1",
             "time": "2019-07-23T06:42:15.957762Z",
             "num_txs": "0",
             "total_txs": "0",
             "last_block_id": {
               "hash": "",
               "parts": {
                 "total": "0",
                 "hash": ""
               }
             },
             "last_commit_hash": "",
             "data_hash": "",
             "validators_hash": "DEFD0C2394B21CF2DD2A49054E968C8754AB0CD20F31804028FA499A40358B19",
             "next_validators_hash": "DEFD0C2394B21CF2DD2A49054E968C8754AB0CD20F31804028FA499A40358B19",
             "consensus_hash": "048091BC7DDC283F77BFBF91D73C44DA58C3DF8A9CBC867405D8B7F3DAADA22F",
             "app_hash": "",
             "last_results_hash": "",
             "evidence_hash": "",
             "proposer_address": "6B6B879EEC588AC6D6C0A925DF40142558D92EF9"
           }
         },
         "block": {
           "header": {
             "version": {
               "block": "10",
               "app": "0"
             },
             "chain_id": "okchain",
             "height": "1",
             "time": "2019-07-23T06:42:15.957762Z",
             "num_txs": "0",
             "total_txs": "0",
             "last_block_id": {
               "hash": "",
               "parts": {
                 "total": "0",
                 "hash": ""
               }
             },
             "last_commit_hash": "",
             "data_hash": "",
             "validators_hash": "DEFD0C2394B21CF2DD2A49054E968C8754AB0CD20F31804028FA499A40358B19",
             "next_validators_hash": "DEFD0C2394B21CF2DD2A49054E968C8754AB0CD20F31804028FA499A40358B19",
             "consensus_hash": "048091BC7DDC283F77BFBF91D73C44DA58C3DF8A9CBC867405D8B7F3DAADA22F",
             "app_hash": "",
             "last_results_hash": "",
             "evidence_hash": "",
             "proposer_address": "6B6B879EEC588AC6D6C0A925DF40142558D92EF9"
           },
           "data": {
             "txs": null
           },
           "evidence": {
             "evidence": null
           },
           "last_commit": {
             "block_id": {
               "hash": "",
               "parts": {
                 "total": "0",
                 "hash": ""
               }
             },
             "precommits": null
           }
         }
       }

Obtain Tx information based on Tx hash
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

http API:

.. code:: http

    GET okchain/v1/txs/{hash}

API parameters:

+--------+----------+------------+-----------+
| Name   | Type     | Required   | Mark      |
+========+==========+============+===========+
| hash   | string   | true       | Tx hash   |
+--------+----------+------------+-----------+

Response:

::

        {
          "height": "468",
          "txhash": "0020A8D7EB798F223319DB636109DC00D258F2756B52F494A92BCABB14BC8BCC",
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
              "value": "0.01250000 okt"
            },
            {
              "key": "action",
              "value": "send"
            }
          ],
          "tx": {
            "type": "auth/StdTx",
            "value": {
              "msg": [
                {
                  "type": "token/Send",
                  "value": {
                    "from_address": "okchain1gaszdnrmghask7kz8n2tdxq0wk2a69z9336mjh",
                    "to_address": "okchain1g7c3nvac7mjgn2m9mqllgat8wwd3aptdqket5k",
                    "amount": [
                      {
                        "denom": "okt",
                        "amount": "10000.00000000"
                      }
                    ]
                  }
                }
              ],
              "signatures": [
                {
                  "pub_key": {
                    "type": "tendermint/PubKeySecp256k1",
                    "value": "AnHEWKSC/pE4VIX8rbUpQFIRA88BNv/wC7e7mHAJ0+7I"
                  },
                  "signature": "SawuipMAXPkE/JFAv0SnS9rcsCbw1EIS8ZZo3qoW7QoPLa+60jPmvQhoRJaa3o+1b1/HnoBvIsn9On8UyKRv1A=="
                }
              ],
              "memo": ""
            }
          },
          "timestamp": "2019-07-23T06:58:22Z"
        }


6. Staking
----------

Obtain information on all validators
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

http API:

.. code:: http

    GET okchain/v1/staking/validators

API parameters:Null

Response:

::

       [
         {
           "operator_address": "okchainvaloper13q7gl0jvk79qz7fgcty3qc49g8h2prnaa4v8m4",
           "consensus_pubkey": {
             "type": "tendermint/PubKeyEd25519",
             "value": "eLwaM5se0V3xjSf1VSPNafbxo8duuPIKc/O2P4P/BQI="
           },
           "jailed": false,
           "status": 2,
           "tokens": "1.00000000",
           "delegator_shares": "1.00000000",
           "description": {
             "moniker": "node1",
             "identity": "",
             "website": "",
             "details": ""
           },
           "unbonding_height": "0",
           "unbonding_time": "1970-01-01T00:00:00Z",
           "commission": {
             "rate": "0.00000000",
             "max_rate": "0.00000000",
             "max_change_rate": "0.00000000",
             "update_time": "2019-07-23T06:42:15.957762Z"
           },
           "min_self_delegation": "1.00000000"
         },
         {
           "operator_address": "okchainvaloper1n0az59a0xt263ngeqndxqcuhx2d4yyd0mayyzc",
           "consensus_pubkey": {
             "type": "tendermint/PubKeyEd25519",
             "value": "UwQZC3vQ7mZJ0zgAh5+OiXxn4MLddjTuRsOcFoitGDE="
           },
           "jailed": false,
           "status": 2,
           "tokens": "1.00000000",
           "delegator_shares": "1.00000000",
           "description": {
             "moniker": "node0",
             "identity": "",
             "website": "",
             "details": ""
           },
           "unbonding_height": "0",
           "unbonding_time": "1970-01-01T00:00:00Z",
           "commission": {
             "rate": "0.00000000",
             "max_rate": "0.00000000",
             "max_change_rate": "0.00000000",
             "update_time": "2019-07-23T06:42:15.957762Z"
           },
           "min_self_delegation": "1.00000000"
         },
       ]


List all operator\_address-validator\_address pairs
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

http API:

.. code:: http

    GET okchain/v1/staking/address

API parameters: Null

Response:

::

       [
         {
           "operator_address": "okchainvaloper13q7gl0jvk79qz7fgcty3qc49g8h2prnaa4v8m4",
           "validator_address": "6B6B879EEC588AC6D6C0A925DF40142558D92EF9"
         },
         {
           "operator_address": "okchainvaloper1n0az59a0xt263ngeqndxqcuhx2d4yyd0mayyzc",
           "validator_address": "77E268D7F58CA2A9C81E27481DA5F8947E99E67A"
         },
       ]


Query corresponding account\_address through operator\_address
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

http API:

.. code:: http

    GET okchain/v1/staking/address/{OperatorAddr}/account_address

API parameters:

+----------------+----------+------------+---------------------+
| Name           | Type     | Required   | Mark                |
+================+==========+============+=====================+
| OperatorAddr   | string   | true       | operator\_address   |
+----------------+----------+------------+---------------------+

Response:

::

    "okchain13q7gl0jvk79qz7fgcty3qc49g8h2prnaptazwn"

Query corresponding operator\_address through validator\_address
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

http API:

.. code:: http

    GET okchain/v1/staking/address/{ValidatorAddr}/validator_address

API parameters:

+-----------------+----------+------------+----------------------+
| Name            | Type     | Required   | Mark                 |
+=================+==========+============+======================+
| ValidatorAddr   | string   | true       | validator\_address   |
+-----------------+----------+------------+----------------------+

Response:

::

    "okchainvaloper1uujtlcc9u6w8gh0quzhtml4llu8pj02v87plt0"

