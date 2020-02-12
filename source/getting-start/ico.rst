Token issuance and listing
==========================

Users who hold a certain number of OKTs can issue new tokens on
OKChain’s network; after passing the dexList proposal and upon
activation, the newly issued tokens can be freely traded on OKChain’s
network. ## 1. Issue tokens Before token listing, you need to issue
tokens. Take ``mycoin`` as an example (the account name is alice for
testing):

.. code:: sh

    $ okchaincli tx token issue --from alice --symbol mycoin -n 21000000 --whole-name 'mycoin'
    {
     "height": "9",
     "txhash": "7D3797B43CF2144CB0B740404C1549A71381E0BB90A35BFE5DC3BE9C86103226",

     ...
    }

Among them, ``--from alice`` represents the new token owner, and
``--symbol mycoin`` represents the symbol of the tokens issued. For
further details of parameter descriptions, please refer to [`issue
tokens <./command/token.md##issue%20tokens>`__\ ], The query results are
as follows:

.. code:: sh

    $ okchaincli query token info mycoin
    #example
    {
     "symbol": "mycoin-254",
     "original_symbol": "mycoin",
     "total_supply": "21000000",
     "owner": "okchain15vfcagv9m56xn6j52l4eqf796z8tkfayz9qu2q",
     "mintable": false
    }

For more details of other functions, please refer to `increase the
supply of tokens <./command/token.md##increase%20the%20supply>`__ and
`burn tokens <./command/token.md##burn>`__

The amount of fees for issuing tokens is currently ``20000okt``, so that
after successfully issuing new tokens, 20,000okt will be deducted from
alice’s account balance; if the balance is too low, the issuance will
fail.

2. Initiate a dexList proposal
------------------------------

Transfer is allowed only after the tokens are issued successfully. Only
after passing the **dexList proposal**, the initial price becomes
effective and users are allowed to buy and sell tokens.

::

    $ okchaincli tx gov submit-dex-list-proposal --title="list mycoin/okt" --description="" --type=DexList --deposit="500okt" --listAsset="mycoin" --quoteAsset="okt" --initPrice="40.25" --maxPriceDigit=4 --maxSizeDigit=4 --minTradeSize="0.001" --from alice
    {
     "height": "137",
     "txhash": "D78534FBA22688F482CCE36F368A99DB77F9886CA4016C7A3325DEA940C34B83",
    }

Among them, ``--deposit 1000okt`` represents the initial deposit
specified when the proposal is initiated, ``--initPrice`` represents the
initial price of a trading pair specified upon listing, and
``--from alice`` represents the account that initiates the proposal. For
further details of parameter descriptions, please refer to [`dexList
proposal
commands <./command/gov.md###dexList%20proposal%20commands>`__\ ].

OKChain will generate a ``proposal-id`` for the successfully submitted
proposal to uniquely label the proposal. The query results are as
follows:

.. code:: sh

    $ okchaincli query tx D78534FBA22688F482CCE36F368A99DB77F9886CA4016C7A3325DEA940C34B83
    {
      "height": "137",
      "txhash": "D78534FBA22688F482CCE36F368A99DB77F9886CA4016C7A3325DEA940C34B83",
      "raw_log": "[{\"msg_index\":\"0\",\"success\":true,\"log\":\"\"}]",
      "tags": [
        {
          "key": "fee",
          "value": "0.01250000 okt"
        },
        {
          "key": "proposal-id",
          "value": "1"
        },
      ],
      ...
    }

We know from the query results that ``proposal-id`` of the proposal
generated in the example is 1. Query proposal information:

.. code:: sh

    $ okchaincli query gov proposal 1
    #example
    {
     "type": "gov/DexListProposal",
     "value": {
      "proposal_id": "1",
      "list_asset": "mycoin",
      "quote_asset": "okt",
      "init_price": "40.250000000000000000",
      "proposal_status": "DepositPeriod",

       ...
    }

The current proposal status is ``DepositPeriod``, which represents the
deposit phase. On OKChain’s system, the deposit amount is set to be
``1000okt`` for listing. In the above application, only\ ``500okt`` is
deposited, so it is necessary to deposit ``500okt`` again.

3. deposit for DexList proposal
-------------------------------

The remaining ``500okt`` can also be deposited by alice or other okt
holders

.. code:: sh

    $ okchaincli tx gov deposit 1 500okt --from alice

    confirm transaction before signing and broadcasting [Y/n]: y
    {
     "height": "143",
     "txhash": "E117DD7F03D5EF47C62D38E764B0849B85329BDDECE8108A1CFE6D8395B9D4C4",

      ...
    }

The proposal falls within the ``VotingPeriod`` state when query is made
through the above commands again after the deposit.

4. Vote on DexList proposal
---------------------------

During the voting phase, the **validator** on OKChain’s network needs to
review the fully deposited **dexList proposal** and vote on the proposal
as follows

.. code:: sh

    $ okchaincli tx gov vote 1 yes --from alice

    confirm transaction before signing and broadcasting [Y/n]: y
    {
     "height": "146",
     "txhash": "35AF42AEF0D9D8BB1F0A1509D7514D09CBD04ADB2912BD05E58997F6F8C1D36A",

      ...
    }

Query the proposal at the end of the voting period. The proposal status
is ``Passed``, which means the proposal has been approved.

5. Listing activation
---------------------

After the listing proposal is passed, the **token issuer** (here is
alice) can take the initiative to activate the token listing:

.. code:: sh

    $ okchaincli tx gov dexlist --proposal=1 --from alice

    confirm transaction before signing and broadcasting [Y/n]: y
    {
     "height": "339",
     "txhash": "E558097F2190176B4B9731A6F2A8214C23C58D7AEE556A69C01CD80FF74F750E",
     
      ...
    }

Users can also use `automatic activation <../governance/dexlist.md>`__
to activate token listing.

Finally, users can check whether the listing is activated by querying
the trading pair:

.. code:: sh

    $ okchaincli query token  tokenpair
    #example
    [
      {
        "baseAssetSymbol": "mycoin",
        "quoteAssetSymbol": "okt",
        "price": "10.00000000",
        "maxPriceDigit": "1",
        "maxSizeDigit": "2",
        "minTradeSize": "0.10000000",
        "tokenPairId": "0"
      }
    ]

The above result shows that the trading pair mycoin/okt exists,
indicating that the listing is successful. ``mycoin`` can be freely
traded on\ ``DEX``.
