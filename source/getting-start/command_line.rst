Connect to OKChain
==================

``okchaincli`` is a command-line tool which connects to OKChain

1. Configure the operating environment of okchaincli:
-----------------------------------------------------

-  Set chain-id which should be okchain

   .. code:: bash

       okchaincli config chain-id okchain 

-  Set the output format of okchaincli request response

   .. code:: bash

       okchaincli config output json    
       okchaincli config indent true 

-  Configure RPC Interface

   .. code:: bash

       okchaincli config node tcp://$RpcInterface  

Sending transactions to OKChain or query information requires a specific
RPC Interface.

If you set up a full OKChain node locally, $RpcInterface can be
``localhost:26657``:

.. code:: bash

    okchaincli config node tcp://localhost:26657  

Or any of the following address ports:

::

    3.13.150.20:26657
    35.176.111.229:26657
    18.162.106.25:26657
    18.220.143.90:26657
    3.9.253.24:26657
    18.162.205.49:26657
    18.162.215.44:26657
    18.162.217.121:26657
    18.162.217.91:26657
    13.209.159.23:26657
    15.164.112.129:26657
    18.197.242.177:26657
    3.120.127.153:26657
    18.139.28.11:26657
    18.139.57.190:26657
    18.140.23.247:26657
    13.113.155.133:26657
    13.115.176.62:26657
    18.179.82.0:26657
    34.210.189.230:26657
    52.41.56.82:26657

-  Configure trust

   .. code:: bash

       okchaincli config trust-node true

   The delegator sets trust-node as true. The on-chain data is returned
   directly and the query efficiency is higher; if it is set as false,
   the authenticity of the data returned by the node is checked and the
   security is higher.

2. okchaincli user manual
-------------------------

-  `account <command/account.md>`__

   account management operations

-  `token <command/token.md>`__

   token-related operations, including token issuance, freezing and
   unfreezing as well as transfer of token ownership

-  `send <command/send.md>`__

   transfer operations, including threshold signature transfers

-  `order <command/order.md>`__

   transaction order operations

-  `gov <command/gov.md>`__

   governance operations

-  `backend <command/backend.md>`__


