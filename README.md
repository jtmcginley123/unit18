How to Start the Network:

Before you begin make sure that you have MyCrypto installed on your computer, as well as having downloaded geth + tools

Make sure that geth + tools is easy to find, maybe rename it 'block-chain-tools' or something obvious to you.

Open terminal

Navigate to 'block-chain-tools' in terminal.

I found it easiest to make my nodes first.

I used the following code to do so:
./geth --datadir node1 account new
./geth --datadir node2 account new

I made sure to write down their keys because they would be needed when configuring the genisis block.

From there, I followed these steps in the terminal:

./puppeth

name your network: alterra

I chose to configure a new genisis block (option 2)

I then chose to create new genisis block from scratch (option 1)

Next, I chose Clique - proof-of-authroity (option 2)

after that, I added both of keys from my nodes making sure to get the part after the 0x since that was already given.

I put both nodes keys in for list of accounts to seal and into list of accounts to pre-fund.

I chose no for the pre-funding the pre-compiled accounts.

I entered my chain/network ID and made sure that this was written down as well since it would be used for when we send our transaction later.

Once I made it back to the main menue, I chose "Manage existing genisis" (option 2) and then I chose to "Export genisis" (option 2)

This allowed for the .json files of the alterra network to be put in the same file as the geth + tools in the file folder titled 'block-chain-tools'

I then went on to initialize the nodes with the alterra.json file. This was done with the code:
./geth --datadir node1 init alterra.json
./geth --datadir node2 init alterra.json

When initializing node1, I made sure to write down the enode that was presented since this woud be used later when we started to mine. 

This next part was very confusing with me but I eventually figured it out. This next part requires two terminals to be opened, one for transactions and one for mining

I used the following code to do so:

For node1:

./geth --datadir node1 --unlock "SEALER_ONE_ADDRESS" --mine --rpc --allow-insecure-unlock

Where it says "SEALER_ONE_ADDRESS", I put in the public key of node1.

For node2:

./geth --datadir node2 --unlock "SEALER_TWO_ADDRESS" --mine --port 30304 --bootnodes "enode://SEALER_ONE_ENODE_ADDRESS@127.0.0.1:30303" --ipcdisable --allow-insecure-unlock

Where it says "SEALER_TWO_ADDRESS" I used the public key of node 2. Where it says 'enode://....." I put the enode address that showed up when I initialized node1.

From then both terminals were moving so I took this as a good sign.

I then proceeded to send a test transaction through MyCrypto.

I clicked 'Change Network'.

'Node Name': alterra
'Network': Custom
'Network Name': alterra
'Currency': ETH
'Chain ID': 369
'URL': http://127.0.0.1:8545

Then clicked 'Save & Use Custom Node'

I then proceeded to click 'Keystore File' since this would be how we woud send transactions from node1 to node2. 

I uploaded my keystore file that was located in my node1 folder with in my 'block-chain-tools'.

This allowed for me to be able to send a transaction from node1 to node2 with just inputting the node2 public address.

I clicked 'Send' and 'Send' again. The transaction went through. The status was 'Pending' but it did say that it may take 3+ hours to confirm. 