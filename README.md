# Proof of Authority Development Chain¶

### In this proeject I will set up a testnet blockchain. To do this, I will create the following deliverables:
1.  Set up my custom testnet blockchain
2.  Send a test transaction 

## 1. Create accounts and setup the out-of-the-box blockchain:
To setup my custom testnet blockchain, I will go through the following steps:

 1.  Create node accounts
 2. Setup a new genesis block (./puppeth)
 3.  Initiate the nodes
 4.  Start mining
### Create Node Accounts:
- First, I navigated into the blockchain_tools directory
- Second, I created two accounts for two nodes for the network with a separate datadir for each using geth .

          ./geth account new --datadir node1

          ./geth account new --datadir node2
- I stored the public address for both nodes to a local text file so I can use it later
- the datadir flag is corresponding for the node directory where the node information are stored
![createaccount](screenshots/create_account_1.png)
### Setup New Genesis Block:
- To setup a new genesis, run the following command:  

           ./puppeth
- I chose the name 'crypto_project' for my network, and saved it in the current directory
- I selected proof-of-authority consensus, and entered (555) as a chainID 
- Next, I entered both node1 and node2 account addresses into the list of accounts to seal and into the list of accounts to pre-fund
- To keep genesis cleaner, I selected 'no' for pre-funding the pre-compiled accounts

![genesissetup](screenshots/1_genesis_setup.png)
![genesissetup](screenshots/2_setup_genesis_block.png)
- Next, I exported genesis configurations and saved the genesis 'crypto_project.json' in the current directory
    ![genesissetup](screenshots/3_setup_genesis_block.png)
### Initiate the Nodes:
- I initiated the nodes by running the following commands:

    
         ./geth init crypto_project.json --datadir node1
         ./geth init crypto_project.json --datadir node2
    ![genesissetup](screenshots/4_setup_genesis_block.png)
### Start Mining:
- Started mining by running the the following commands:
    - Node1 command:


             ./geth --datadir node1 --unlock"{node1 key}" --mine --rpc --allow-insecure-unlock
- As we can see in the above command, we unlocked the first node by entering its address (using --unlock flag) that we stored on a local text file (each node has a unique address, which is the public key)
- I copied the full enode address here in order to run node2 
- the --mine flag enables mining for this node 
- the --rpc enables other nodes to communicate with this node and run commands using rpc (remote procedure call)
- the --allow-insecure-unlock enables unlocking the private key for this node through http (not only https)
![createaccount](screenshots/node1_1.png)
![createaccount](screenshots/node1_2.png)
![createaccount](screenshots/node1_3.png)
![createaccount](screenshots/node1_4.png)
    - Node2 command:

             ./geth --datadir node_2 --mine --port 30304 --bootnodes "{enode of node1}" --unlock "{node2 key}" --allow-insecure-unlock.
    - I unlocked  node2 (using --unlock flag) by first entering the node2 address (public key)
    - I then entered the public key of node1 (enode address) that I copied from node1, that will allow the two nodes to communicate (using the --bootnodes flag)
    - the --mine flag enables mining for this node 
    - the --rpc enables other nodes to communicate with this node and run commands using rpc (remote procedure call)
    - the --allow-insecure-unlock enables unlocking the private key for this node through http (not only https)
 ![createaccount](screenshots/node2_1.png)
 ![createaccount](screenshots/node2_2.png)
 ![createaccount](screenshots/node2_3.png)
 ![createaccount](screenshots/node2_4.png)

    - the --port flag to specify what port will node2 be using. We used node1 port + 1
## 2. Send Transactions
To send a transaction, I have done the following:

 1. run MyCrypto and use the private network using the  custom network option
 2. Use Keystore file for Node1
 3. Check whether you have a sufficient balance in your account
4. Enter address to send a transaction

### Setup a Custom Network:
- First, I setup a custom network using MYCrypto  
    - I first clicked on 'Change Network', then 'Add Custom Node'
    - entered crypto_project as Node Name
    - changed network to custom
    - entered ChainID as 555, which is the same chainID number I chose when I first created the genesis block)


### Node1 Account 
- Here, I opened MYCrypto to use the node1 account by importing the keystore file that was generated when node1 account was first created
![login](screenshots/login_.png)

### Sufficient Balance
- Here, I have enough balance to send a transaction  
![login](screenshots/account_balance.png)

### Send Transaction
- I sent a 500 ETH from my node1 account to my node2 account 

![login](screenshots/send_transaction.png)

- Check transaction status

![login](screenshots/transaction_confirmation.png)


- Check transaction on terminal
![login](screenshots/terminal_transaction.png)


### Dependencies:
- MyCrypto tool 
- Go Ethereum
