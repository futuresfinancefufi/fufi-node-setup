sudo apt-get install software-properties-common
  sudo add-apt-repository -y ppa:ethereum/ethereum
  sudo apt-get update
  sudo apt-get install ethereum
  sudo curl -sL https://deb.nodesource.com/setup_14.x | sudo -E bash -
  sudo apt-get install -y nodejs
  sudo npm i -g pm2 


- Create Node Account

  
bash
  # create new account
  /fufi_blockchain/node$ geth --datadir "./data" account new
  
  # password : enter your password
  Your new key was generated
  
  output :
  Public address of the key:   0x1B741E7043fa4FE5c78e5e7A53ACaeF453Df7bE5 
  Path of the secret key file: data/keystore/UTC--2021-09-06T15-09-50.582316582Z--1b741e7043fa4fe5c78e5e7a53acaef453df7be5
  
  
  # save password in to password.txt 
  /fufi_blockchain/node/data$ vim password.txt
  
  # put genesis.json into directory
  /fufi_blockchain/$ genesis.json
  
  
  

#  Node2 (Creating node2 using genesis file)
 /fufi_blockchain/node$ geth --datadir ./data init ../futurefinance.json

 output : 
 INFO [09-06|16:08:24.597] Maximum peer count                       ETH=50 LES=0 total=50
 INFO [09-06|16:08:24.597] Smartcard socket not found, disabling    err="stat /run/pcscd/pcscd.comm: no such file or directory"
 INFO [09-06|16:08:24.598] Set global gas cap                       cap=50,000,000
 INFO [09-06|16:08:24.598] Allocated cache and file handles         database=/var/www/app/fufi_blockchain/node2/data/geth/chaindata cache=16.00MiB handles=16
 INFO [09-06|16:08:24.608] Writing custom genesis block
 INFO [09-06|16:08:24.615] Persisted trie from memory database      nodes=356 size=50.63KiB time=1.54065ms gcnodes=0 gcsize=0.00B gctime=0s livenodes=1 livesize=0.00B
 INFO [09-06|16:08:24.615] Successfully wrote genesis state         database=chaindata hash=63b7c6..a2d2b0
 INFO [09-06|16:08:24.616] Allocated cache and file handles         database=/var/www/app/fufi_blockchain/node2/data/geth/lightchaindata cache=16.00MiB handles=16
 INFO [09-06|16:08:24.623] Writing custom genesis block
 INFO [09-06|16:08:24.633] Persisted trie from memory database      nodes=356 size=50.63KiB time=2.575635ms gcnodes=0 gcsize=0.00B gctime=0s livenodes=1 livesize=0.00B
 INFO [09-06|16:08:24.634] Successfully wrote genesis state         database=lightchaindata hash=63b7c6..a2d2b0


# create Node script.sh file 
/fufi_blockchain/node$ vim pm2.node.sh

geth --networkid 60457 --datadir "./data" --bootnodes enode://b4627a88f618ad66944c5c250ef04046b71ee79d6d134a3d138fcc761653fd37eaf3f686f562463f3806b0298812986a2b83f0d5e014f5179de514df516b8bf1@159.89.161.128:0?discport=30301 --port 30311 --ipcdisable --syncmode full --http.api 'eth,web3,personal' --http --allow-insecure-unlock --http.corsdomain "*" --http.port 8546 --unlock 0x1da73173273b4AaF99952964FE7474deE2C30345 --password ./data/password.txt  console



# Run Node script.sh file
/fufi_blockchain/node$ pm2 start pm2.node.sh

# Show Logs Node script.sh file
/fufi_blockchain/node$ pm2 logs pm2.node.sh

