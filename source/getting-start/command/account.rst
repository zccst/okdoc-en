Account
=======

1. Key：
--------

1.1 Add an account:
~~~~~~~~~~~~~~~~~~~

Parameter description:
^^^^^^^^^^^^^^^^^^^^^^

+-------------+---------------------------------+
| Parameter   | Mark                            |
+=============+=================================+
| name        | Add an account name (eg. bob)   |
+-------------+---------------------------------+

Example:
^^^^^^^^

The system will randomly gerenate information including mnemonic
phrases, public keys and addresses

.. code:: bash

    okchaincli keys add <name> [flags]

Successful response:
^^^^^^^^^^^^^^^^^^^^

::

    okchaincli keys add wind
      
    # Example output
    {
      "name": "wind",
      "type": "local",
      "address": "okchain1ltxwpg2f2frsnq3et3qp7sfz2u44qsaj5ytlcf",
      "pubkey": "okchainpub1addwnpepqg8g82chdrf4ra4fn39e0lhzmds6qgs75emlzp2kqw5n69xt0fz3cewvx06",
      "mnemonic": "alpha enroll regret dizzy bid reunion company divorce layer narrow ceiling state"
      }
      
    # Recover keys by mnemonic phrases
    okchaincli keys add --recover admin   -y -m "keen border system oil inject hotel hood potato shed pumpkin legend actor"

1.2 Display all local key information:
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Parameter description:
^^^^^^^^^^^^^^^^^^^^^^

Null

Example:
^^^^^^^^

Display all local key information

.. code:: bash

    okchaincli keys list [flags]

Successful response:
^^^^^^^^^^^^^^^^^^^^

::

      okchaincli keys list
      
      # Example output
      [
        {
          "name": "admin16",
          "type": "local",
          "address": "okchain1v853tq96n9ghvyxlvqyxyj97589clccr33yr7a",
          "pubkey": "okchainpub1addwnpepq2nfj9lqmqrwjyrqnp574tll493svxdltwlnqq3vn5ptmf2ceraesgyfegg"
        },
        {
          "name": "alice",
          "type": "local",
          "address": "okchain1vr9u0u829g68vcy6y362efm3tky4mhfxf28tth",
          "pubkey": "okchainpub1addwnpepq2nkjj2tv9yyvfaevc45n3tszsl9l7t642rh5j2udvwn5uee26gqv7vwhun"
        },
      ]

1.3 Display the information on the key of a specific user:
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Parameter description:
^^^^^^^^^^^^^^^^^^^^^^

+-------------+------------------------------------------+
| Parameter   | Mark                                     |
+=============+==========================================+
| name        | Account name to be displayed (eg. bob)   |
+-------------+------------------------------------------+

Example:
^^^^^^^^

Display the information on the key of a specific user

.. code:: bash

    okchaincli keys show [name [name...]] [flags]

Successful response:
^^^^^^^^^^^^^^^^^^^^

::

      okchaincli keys show bob
      
      # Example output
      {
        "name": "bob",
        "type": "local",
        "address": "okchain10487f9wxss2g2ctvpewkmjk543vg65x9rzv09n",
        "pubkey":     "okchainpub1addwnpepq2gaqy8nk0z0plexzusvs4g97wsvjtqftnpjkmw25lfh2hjz3wk0svf030h"
      }

1.4 Delete the information on the key of a specific user:
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Parameter description:
^^^^^^^^^^^^^^^^^^^^^^

+-------------+----------------------------------------+
| Parameter   | Mark                                   |
+=============+========================================+
| name        | Account name to be deleted (eg. bob)   |
+-------------+----------------------------------------+

Example:
^^^^^^^^

Delete the information on the key of a specific user

.. code:: bash

    okchaincli keys delete <name> [flags]

Successful response:
^^^^^^^^^^^^^^^^^^^^

::

      okchaincli keys delete bob
      
      #Example output
      DANGER - enter password to permanently delete key:
      Key deleted forever (uh oh!)

1.5 Update the information on the key of a specific user:
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Parameter description:
^^^^^^^^^^^^^^^^^^^^^^

+-------------+----------------------------------------+
| Parameter   | Mark                                   |
+=============+========================================+
| name        | Account name to be updated (eg. bob)   |
+-------------+----------------------------------------+

Example:
^^^^^^^^

Update the information on the key of a specific user:

.. code:: bash

    okchaincli keys update <name> [flags]

Successful response:
^^^^^^^^^^^^^^^^^^^^

::

      okchaincli keys update bob
      
      # Example output
      Enter the current passphrase:
      Enter the new passphrase:
      Repeat the new passphrase:
      Password successfully updated!

1.6 Generate a bip39 mnemonic phrase:
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Parameter description:
^^^^^^^^^^^^^^^^^^^^^^

Null

Example:
^^^^^^^^

Generate a bip39 mnemonic phrase

.. code:: bash

    okchaincli keys mnemonic [flags]

Successful response:
^^^^^^^^^^^^^^^^^^^^

::

    okchaincli keys mnemonic

    # Example output
    board zone elevator lesson welcome meadow love card obey cruise unlock double

2. Account：
------------

Query account balance:
~~~~~~~~~~~~~~~~~~~~~~

Parameter description:
^^^^^^^^^^^^^^^^^^^^^^

+-------------+---------------------------------------------------------------------+
| Parameter   | Mark                                                                |
+=============+=====================================================================+
| Address     | User address (eg. okchain10q0rk5qnyag7wfvvt7rtphlw589m7frsmyq4ya)   |
+-------------+---------------------------------------------------------------------+

Example:
^^^^^^^^

Query user information, including serial numbers, public keys and token
balances

.. code:: bash

    okchaincli query account <address>

Successful response:
^^^^^^^^^^^^^^^^^^^^

::

      okchaincli query account okchain10q0rk5qnyag7wfvvt7rtphlw589m7frsmyq4ya
      
      # Example output
      {
        "type": "auth/Account",
        "value": {
          "address": "okchain10q0rk5qnyag7wfvvt7rtphlw589m7frsmyq4ya",
          "coins": [
            {
              "denom": "acoin",
              "amount": "10000000.00000000"
            },
            {
              "denom": "bcoin",
              "amount": "10000000.00000000"
            },
            {
              "denom": "bcoin-805",
              "amount": "200000.00000000"
            },
            {
              "denom": "okt",
              "amount": "9920000.00000000"
            },
          ],
          "public_key": {
            "type": "tendermint/PubKeySecp256k1",
            "value": "AgYaL1tZ7ekqvweQhKojG8sDHUfN23qJWviAsTDIWvYU"
          },
          "account_number": "3",
          "sequence": "4"
        }
       }  

