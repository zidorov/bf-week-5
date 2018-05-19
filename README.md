# Blockchain Founder. Week 5.
## DApp "Casino Ethereum"
Based on https://medium.com/@merunasgrincalaitis/the-ultimate-end-to-end-tutorial-to-create-and-deploy-a-fully-descentralized-dapp-in-ethereum-18f0cf6d7e0e

To get access just go to
https://gateway.ipfs.io/ipns/QmawAyhL433WQDQDLPChzm989fW9sqnjp718rrPu9qFwq8
when and if my IPFS daemon is running )

How to build and deploy from scratch.
Nodejs and truffle should already be installed.
### Install dependencies
```console
mkdir ethereum-casino
cd ethereum casino
truffle init
npm init

npm i --save webpack react react-dom babel-core babel-loader babel-preset-react babel-preset-env css-loader style-loader json-loader web3@0.20.0 babel-polyfill babel-register babel-preset-stage-2 babel-preset-es2015

npm i -g http-server webpack webpack-cli json-loader 
```
### Update source code
Make dirs in project root:
```console
mkdir src
mkdir src/js
mkdir src/css
mkdir dist
```
Replace file in project root with one from https://github.com/zidorov/bf-week-5/tree/master/casino-ethereum-demo
```
truffle.js
```

Add files to project from https://github.com/zidorov/bf-week-5/tree/master/casino-ethereum-demo:
```
webpack.config.js
migrations/2_deploy_casino.js
contracts/Casino.sol
dist/index.html
src/css/index.css
src/js/index.js
```
### Test and deploy contracts
Compile contracts using truffle:
```console
truffle compile
```
Deploy contracts in ganache:
```
ganache-cli -l 8000000
truffle migrate
```
Test contracts:
```
truffle test
```
Deploy contracts in Rinkeby.
Start Geth:
```
geth.exe --rpc --rpcport 8547 --verbosity 2 --fast --rinkeby console
```
Unlock account in geth console:
```
personal.unlockAccount(eth.accounts[0],'<password>',1e9)
```
Deploy contracts to Rinkeby:
```
truffle migrate --reset --network rinkeby
```
Write down Casino contract number, e.g. 0x78b45d4e5e5b1d9426b3eadd48dc13e157dc1fee

Get Casino.sol contract ABI:
```
solcjs --abi contracts/Casino.sol -o build/contracts/
```
### Update code and build using webpack
Update ABI and contract address in file src/js/index.js
```js
const MyContract = web3.eth.contract(<put contract ABI here>);
this.state.ContractInstance = MyContract.at("<put contract address here>")
```
Build dist/build.js:
```
webpack
```
### Test locally
```
http-server dist/
```
Go to http://localhost:8080 to test.

### Deploy to IPFS
install IPFS https://ipfs.io/docs/install/

Init IPFS node:
```
ipfs init
```
Run IPFS daemon
```
ipfs daemon
```

Now publish ```dist/``` dir to ipfs:
```
ipfs add -r dist/
```
example output:
```
added QmWiLswt1STr1BhXsxtnAki3cp43gJsU4LbDXeZ2SKcz6c dist/build.js
added QmW1zu8pRP1Cb9yiRz5z2HqtYhmzZuGMyoopZKxvyGPuSG dist/index.html
added QmZJy7nbfx2EXfRfHuWcMyNft7afDNnsEo6JvB7vvYb34q dist
```
Publish in IPNS using ```dist/``` hash:
```
ipfs name publish QmZJy7nbfx2EXfRfHuWcMyNft7afDNnsEo6JvB7vvYb34q
```
example output:
```
Published to QmawAyhL433WQDQDLPChzm989fW9sqnjp718rrPu9qFwq8: /ipfs/QmZJy7nbfx2EXfRfHuWcMyNft7afDNnsEo6JvB7vvYb34q
```
#### Now DApp is accessible via IPFS
###### IPFS addresses (changes every time if file/dir is changed)
Public gateway:
```https://gateway.ipfs.io/ipfs/QmZJy7nbfx2EXfRfHuWcMyNft7afDNnsEo6JvB7vvYb34q```
Local gateway:
```https://localhost:8080/ipfs/QmZJy7nbfx2EXfRfHuWcMyNft7afDNnsEo6JvB7vvYb34q```
###### IPNS addresses (constant even if file/dir is changed)
Public gateway:
```https://gateway.ipfs.io/ipns/QmawAyhL433WQDQDLPChzm989fW9sqnjp718rrPu9qFwq8```
Local gateway:
```https://gateway.ipfs.io/ipns/QmawAyhL433WQDQDLPChzm989fW9sqnjp718rrPu9qFwq8```


