| Descriptions: 1. Issue (`issue </getting-start/command/token/#1>`__)
tokens before initiating a dexList proposal
| 2. The types of dexList proposals include `dexList proposal for
automatic activation of token listing </getting-start/ico/#242>`__ and
`dexList proposal for initiating listing
activation </getting-start/ico/#241>`__:
|   a. DexList proposals for automatic activation of token listing are
the proposals that do not specify ``--blockHeight`` and complete listing
activation through a `listing activation
command </getting-start/command/gov/#4>`__ upon approval
|   b. DexList proposals for initiating listing activation are the
proposals that specify ``--blockHeight`` upon initiation and complete
listing activation when the block height reaches a specified level upon
approval
| 3. DexList proposals for initiating listing activation can be
initiated by any okt holders, but after they are approved, they ``must``
be activated by token owners. DexList proposals for automatic activation
of token listing ``must`` be initiated by token owners
| 4. DexList proposals for automatic activation should be completed
within the expiration period of activation (DexListExpireTime) upon
approval, otherwise they will become invalid and cannot be activated.
You can only initiate the proposals again to activate token listing.
