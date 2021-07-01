# Proof of Authority Development Chain
For this assignment, you will take on the role of a new developer at a small bank.
Your mission, should you choose to accept it, will be to set up a testnet blockchain for your organization.
To do this, you will create and submit four deliverables:

- Set up your custom testnet blockchain.
- Send a test transaction.
- Create a repository.

Write instructions on how to use the chain for the rest of your team.

# Background
You have just landed a new job at ZBank, a small, innovative bank that is interested in exploring what
blockchain technology can do for them and their customers.
Your first project at the company is to set up a private testnet that you and your team of developers
can use to explore potentials for blockchain at ZBank.
You have decided on setting up a testnet because:
There is no real money involved, which will give your team of developers the freedom to experiment.
Testnets allows for offline development.
In order to set up a testnet, you will need to use the following skills/tools we learned in class:


- Puppeth, to generate your genesis block.
- Geth, a command-line tool, to create keys, initialize nodes, and connect the nodes together.
-The Clique Proof of Authority algorithm.


Tokens inherently have no value here, so we will provide pre-configured accounts and nodes for easy setup.
After creating the custom development chain, create documentation for others on how to start it using the pre-configured
nodes and accounts. You can name the network anything you want, have fun with it!
Be sure to include any preliminary setup information, such as installing dependencies and environment configuration.

# Instructions

## Node Setup
Assuming we've already downloaded geth, we want to copy those downloaded files to a new directory, in this case called 'Unit18'.
Next, open Git Bash and navigate to the 'Unit18' folder. From there we want to create folders for two nodes labelled 'node1' and 'node2'.
After this, we want to activate accounts for each node by passing: 
$ ./geth account new --datadir node1
$ ./geth account new --datadir node2

You will need to create a password for each node. Save the Public Address and Path of the Secret Key for each node. Copy these addresses (four in total) to a
notepad, we will need these later.

Run $ ./puppeth
Specify a network name, in this case we used 'unit18'
Choose 2, "Configure new genesis"
Choose 1, "Create new genesis from scratch"
Choose 2, "Clique - proof-of-authority"

Now we want to prefund our accounts that we will use to test the network.
Paste the public addresses of both nodes Where it asks "Which accounts are allowed to seal? (mandatory at least one)"
Repeat for "Which accounts should be pre-funded? (advisable at least one)"
Enter "no" for "Should the precompile-addresses (0x1 .. 0xff) be pre-funded with 1 wei? (advisable yes)"
Enter a chian network id. For this network we chose to use "456"

![2](https://user-images.githubusercontent.com/77086043/124188367-0501d600-da74-11eb-9984-9ca52c3e4e87.PNG)


You should recieve a message which says "Configured new genesis block"

Next, choose 2 to "Manage existing gensis"
Then, choose 2 to "Export genesis configuration"

It will ask what folder you want to save the gensis specs to. For this, we entered "puppernet".
Only wo specs are needed, the networkname.json and networkname-harmony.json.

After pressing 'enter', press Ctrl+C to navigate to the 'Unit18' directory.

Now we want to initialize the nodes. 
Enter: $ ./geth init puppernet/unit18.json --datadir node1
       $ ./geth init puppernet/unit18.json --datadir node2
You should see "Successfully wrote genesis state" for each command

![3](https://user-images.githubusercontent.com/77086043/124188411-164ae280-da74-11eb-9ffb-c73b175524c8.PNG)

After this is complete we want to start mining.
First enter $ ./geth --datadir node1 --unlock "SEALER_ONE_ADDRESS" --mine --rpc --allow-insecure-unlock
Enter your password when prompted
The "SEALER_ONE_ADDRESS" represents the public address from node1, replace it with such. 
Look for a message which says "Started P2P networking". 
Copy the message which starts with "enode://..." until "...30303"
Paste this whole entry to your notepad file and label it "node1 Enode"
We should see a message which says "Commit new mining work" to know it's working.

Open a new Git Bash window and navigate to the 'Unit18' folder.
Enter $ ./geth --datadir node2 --unlock "SEALER_TWO_ADDRESS" --mine --port 30304 --bootnodes "enode://SEALER_ONE_ENODE_ADDRESS@127.0.0.1:30303" --ipcdisable --allow-insecure-unlock
The "SEALER_TWO_ADDRESS" is the node2 public address, replace it with such. The "SEALER_ONE_ENODE_ADDRESS"
is the node1 Enode, replace it with such.
You should see the same "Commit new mining work" message as well as "Imported new chain segment" to 
confirm the two nodes are connected.

![4](https://user-images.githubusercontent.com/77086043/124188491-2d89d000-da74-11eb-93da-f24ccb7a7824.PNG)

![5](https://user-images.githubusercontent.com/77086043/124188499-2fec2a00-da74-11eb-916f-a3aeaae2744f.PNG)


## Custom Node on MyCrypto
Navigate to MyCrypto and click on "Add Custom Node" on the left side of the menu.
Label your node's name and select 'Custom' for the network.
Enter 'unt18' for the network name, currency as 'ETH', and chain ID as '456'
The URL should be 'http://127.0.0.1:8545'
Click 'Save & Use Custom Node'

Next, go to'View & Send' and click the 'Keystor File' tab.
Paste the file from your keystore folder in node1 and 'Unlock'
You should see a value of ETH opn the right side of the screen.
Paste the public address of node2 in the address tab, enter a random amount of ETH to send, and send the transaction.
Navigate to the 'TX Status' tab on the left side and look for your transaction.
We should see a "Successful" message after "Pending".

![6](https://user-images.githubusercontent.com/77086043/124188574-44c8bd80-da74-11eb-8d19-c934677cfae3.PNG)


![1](https://user-images.githubusercontent.com/77086043/124188534-3c708280-da74-11eb-86be-7d5ba01a2ad1.PNG)


