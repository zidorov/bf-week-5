# Blockchain Founder. Week 5.
## DApp "Casino Ethereum"
Based on https://medium.com/@merunasgrincalaitis/the-ultimate-end-to-end-tutorial-to-create-and-deploy-a-fully-descentralized-dapp-in-ethereum-18f0cf6d7e0e

To get access just go to https://gateway.ipfs.io/ipns/QmX2JsU84kRtb1rttrYuyTsLKh3g9d8dZZQjxwXgHeZ22n/ when my ipfs daemon is running )

How to repeat:

truffle init

npm init
npm i --save webpack react react-dom babel-core babel-loader babel-preset-react babel-preset-env css-loader style-loader json-loader web3@0.20.0 babel-polyfill babel-register
npm i -g http-server webpack webpack-cli json-loader

nano webpack.config.js

mkdir src
mkdir src/js
mkdir src/css
mkdir dist

truffle compile
ganache-cli -l 8000000
nano 2_deploy_contract.js
truffle migrate

geth.exe --rpc --rpcport 8547 --verbosity 2 --fast --rinkeby console
personal.unlockAccount(eth.accounts[0],'12345678',1e9)

truffle migrate --reset --network rinkeby

write down Casino contract
0x78b45d4e5e5b1d9426b3eadd48dc13e157dc1fee

get ABI
solcjs --abi contracts/Casino.sol -o build/contracts/

install ipfs:
https://ipfs.io/docs/install/


http-server dist/
go to http://127.0.0.1:8081/ to check

now publish to ipfs:
ipfs add -r dist/

ipfs name publish QmdgEM47C7fYDJ8f3VwgKbiFSGz9fXFFdZFcSaaaSBJmhv

go to:
gateway.ipfs.io/ipfs/QmdgEM47C7fYDJ8f3VwgKbiFSGz9fXFFdZFcSaaaSBJmhv
