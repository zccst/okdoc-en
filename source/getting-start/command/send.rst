Transfer
========

1. Transfer
-----------

.. code:: bash

    okchaincli tx send <addr> <amount> --from <name>

Parameter description
~~~~~~~~~~~~~~~~~~~~~

\| **Name** \| **Type** \| **Description** \| \| :------: \| :------: \|
:---------------------------------------------------: \| \| addr \|
string \| recipient address \| \| amount \| string \| transfer amount,
covering various cryptocurrencies separated by commas, eg. 1okt, 2bcoin
\| \| from \| String \| token owner \|

Example
~~~~~~~

.. code:: bash

    okchaincli tx send okchain1jrhfgvmun4wd5qekxg2ma4xr405pn4dpwtx2qf 2okt --from alice -b block

Successful response:
~~~~~~~~~~~~~~~~~~~~

::

    {
      "height": "63",
      "txhash": "AF5742022E2A183AB0C9BB90F130BFBBFEE1E69C05B20F4E417C2C9E93A52A16",
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
      ]
    }

2. Multi-signature transfer
---------------------------

Multi-signature transfer consists of multiple steps:

2.1. Creat accounts p1, p2, p3：
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Example:

.. code:: bash

    okchaincli keys add --pubkey=cosmospub1addwnpepqtg367t3j6myh4ces0luq3f6g87ptzwszpl9g5r28tgavypkdmm2w5l4zuq p1

    okchaincli keys add --pubkey=cosmospub1addwnpepqg334a4my6ufrs7r0ajsd6lxac9arsvtqljf0fzrgr27xvf3n5uugpsxna8 p2

    okchaincli keys add --pubkey=cosmospub1addwnpepqd7jd60n88tk98hyh72xsw48pjpfhdw0cd77ju59eqc88sxscfjkgx7tyfc p3

2.2. Generate multi-signature public keys:
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

-  Aggregate multi-signature public keys p1, p2 and p3 and set the
   signature threshold as N, which means the transfer is effective after
   obtaining N people's signatures.

-  Set the signature threshold as 2 in the example:

   .. code:: bash

       okchaincli keys add --multisig-threshold=2 --multisig=p1,p2,p3 p1p2p3

``--multisig-threshold`` is the threshold for the number of private keys
involved in multi-signature transactions.

``--multisig`` tag must contain the names of sub-public keys to be
aggregated into a single public key, which will be generated in a local
database and stored as ``new_key_name``. All names provided via
``--multisig`` must have already existed in the local database.

-  Display user addresses and deposit into them: Display user addresses
   p1, p2, p3 and deposit 100.1 OKT into them
-  Example:

   .. code:: bash

       okchaincli keys show -a p1p2p3
       okchaincli tx send cosmos1553hrs03kl2tlq47d9f6j477xdjp362l2cfetl 100.1okt --from=alice
       okchaincli query account cosmos1553hrs03kl2tlq47d9f6j477xdjp362l2cfetl

   2.3. Multi-signature:
   ~~~~~~~~~~~~~~~~~~~~~

   Create an unsigned transaction:
   ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

   Create an unsigned transaction ``unsignedTx.json`` ##### Example:

   .. code:: bash

       okchaincli tx send cosmos1xd07r5a3e2mf4srqck3hvzww24c65hpt604ge5 10okt \
         --chain-id=okchain \
         --from=cosmos1553hrs03kl2tlq47d9f6j477xdjp362l2cfetl \
         --generate-only > unsignedTx.json

   p1, p2, p3 sign:
   ^^^^^^^^^^^^^^^^

   Example:
   ''''''''

   | \`\`\`bash okchaincli tx sign
   |  --multisig=cosmos1553hrs03kl2tlq47d9f6j477xdjp362l2cfetl
   |  --from=alice
   |  --output-document=p1signature.json
   |  unsignedTx.json

| okchaincli tx sign
|  --multisig=cosmos1553hrs03kl2tlq47d9f6j477xdjp362l2cfetl
|  --from=jack
|  --output-document=p2signature.json
|  unsignedTx.json
``#### Create an aggregate signature:  Create an aggregate signature `signedTx.json` since the default threshold is set to 2 so that a transaction with p1p2 can be executed. ##### Example:``\ bash
okchaincli tx multisign
|  unsignedTx.json
|  p1p2p3
|  p1signature.json p2signature.json > signedTx.json
``### 2.4. Execute a transaction signedTx.json： Execute a signed `signedTx.json` offline and query the balance for confirmation. #### Example:``\ bash
okchaincli tx broadcast signedTx.json

okchaincli query account cosmos1553hrs03kl2tlq47d9f6j477xdjp362l2cfetl
\`\`\`
