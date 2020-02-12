Join the OKChain Testnet
========================

The `launce repo <http://gitlab.okcoin-inc.com/dex/launch>`__ collects
the genesis and configuration files for the OKChain testnet.

::

    Note: You need to install okchain and configure okchaind before you go further

For further details, please refer to `install
OKChain <install.md##%20install%20OKChain>`__

1. Setting up a new node
------------------------

Initialize the node and create the necessary config files:

.. code:: bash

    okchaind init --chain-id okchain 

You can edit ``moniker`` in the ``$HOME/.okchaind/config/config.toml``

::

    # A custom human readable name for this node
    moniker = "<your_custom_moniker>"

Note: Monikers can only contain ASCII characters. Unicode characters may
render nodes invisible on the network!

2. Genesis
----------

For further details, please refer to `What is the
Genesis <genesis.md>`__ ### 2.1 Download the genesis file: download
genesis.json via
`genesis <http://gitlab.okcoin-inc.com/dex/launch/blob/testnet01/genesis.json>`__

Verify the completeness of genesis.json to ensure that the same genesis
file is used on the testnet

::

    $ shasum -a 256 genesis.json
    5b96c28ca7352ea83304e3d41fc5c24bb373a0cbf269f6e65504cb8128aae5fa

Copy the genesis.json of the testnet to okchaind's configuration
directory, which is ``$HOME/.okchaind/config``

3. Seed nodes
-------------

After the nodes are initialized, they need to join OKChain's testnet
through the seed nodes.

The details of the configuration of seed nodes on OKChain's testnet are
as follows:

::

    b7c6bdfe0c3a6c1c68d6d6849f1b60f566e189dd@3.13.150.20:26656
    d7eec05e6449945c8e0fd080d58977d671eae588@35.176.111.229:26656
    223b5b41d1dba9057401def49b456630e1ab2599@18.162.106.25:26656

Configure seed nodes in ``~/.okchaind/config/config.toml``\ 。

::

    # Comma separated list of seed nodes to connect to
    seeds = "b7c6bdfe0c3a6c1c68d6d6849f1b60f566e189dd@3.13.150.20:26656,d7eec05e6449945c8e0fd080d58977d671eae588@35.176.111.229:26656,223b5b41d1dba9057401def49b456630e1ab2599@18.162.106.25:26656"

4. Start nodes
--------------

4.1 okchaind start
~~~~~~~~~~~~~~~~~~

Connect seed nodes configured in ``config.toml`` to OKChain

.. code:: bash

    okchaind start 

4.2 Use docker to activate
~~~~~~~~~~~~~~~~~~~~~~~~~~

4.2.1 Use docker commands to activate
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

okchaind can also be enabled by a docker container. We have officially
released a number of docker images.
:math:`TAG represents the version number of okchaind. The version of the testnet is ``\ TAG=v0.1.0\ ``. ```bash $ docker run \     -e OKDEX_P2P_SEEDS=b7c6bdfe0c3a6c1c68d6d6849f1b60f566e189dd@3.13.150.20:26656,d7eec05e6449945c8e0fd080d58977d671eae588@35.176.111.229:26656,223b5b41d1dba9057401def49b456630e1ab2599@18.162.106.25:26656 \     -e OKDEX_P2P_ADDR_BOOK_STRICT=false \     -e OKDEX_LOG_STDOUT=false \     -e OKDEX_LOG_FILE=/root/.okchaind/okchaind.log \     -p 26656:26656 \     -p 26657:26657 \     -p 26659:26659 \     okchain/testnet:v0.1.0 \     okchaind start ``` #### 4.2.2 Use docker-compose commands to activate First, save the below in``\ okchain\_full\_node.yml\`.

.. code:: yml

    version: '2'

    services:
      mynode:
        container_name: mynode
        image: "okchain/testnet:v0.1.0"
        environment:
          - OKDEX_P2P_ADDR_BOOK_STRICT=false
          - OKDEX_LOG_LEVEL=*:info
          - OKDEX_LOG_STDOUT=false
          - OKDEX_LOG_FILE=/root/.okchaind/okchaind.log
          - OKDEX_PROF_LADDR=0.0.0.0:6060
          - OKDEX_P2P_LADDR=tcp://0.0.0.0:26656
          - OKDEX_P2P_SEEDS=b7c6bdfe0c3a6c1c68d6d6849f1b60f566e189dd@3.13.150.20:26656,d7eec05e6449945c8e0fd080d58977d671eae588@35.176.111.229:26656,223b5b41d1dba9057401def49b456630e1ab2599@18.162.106.25:26656
          - OKDEX_MONIKER=mynode
        volumes:
          - /var/run/docker.sock:/var/run/docker.sock
          - ./okchain_data/mynode:/root/.okchaind
        ports:
          - "26656:26656"
          - "26657:26657"
          - "26659:26659"

Then, execute the command
``docker-compose -f okchain_full_node.yml up -d``. okchaind container
will be locally enabled and connected to the testnet after successfully
executing the command.

4.3 Enable backend module
~~~~~~~~~~~~~~~~~~~~~~~~~

If you want to get extra info from your full node (eg. candlestick data,
market data, order books and transaction lists, you should enable
backend module when activating nodes.

.. code:: bash

    okchaind start --backend.enable_backend=1 --backend.orm_engine.engine_type=sqlite3 --backend.orm_engine.connect_str=$db_filepath

5. Close nodes
--------------

When you need to close the nodes, you need to exit okchaind as follows,
otherwise block data will be damaged:

5.1 Close nodes enabled by okchaind start
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code:: bash

    # grep "okchaind" | grep -v grep |awk '{print "kill -2 "$1""}' |  bash
    okchaind stop

5.2 Close nodes enabled by docker
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code:: bash

    # docker exec -i <container_id> ps -ef| grep "okchaind" | grep -v grep |awk '{print "kill -2 "$1""}' | docker exec -i <container_id> /bin/bash
    docker exec -i <container_id> okchaind stop

5.3 Close nodes enabled by docker-compose
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code:: bash

    # docker-compose exec -i <container_id> ps -ef| grep "okchaind" | grep -v grep |awk '{print "kill -2 "$1""}' | docker-compose exec -i <container_id> /bin/bash
    docker-compose exec -i <container_id> okchaind stop

