# Deploy your contracts using hardhat




## To setup a Hardhat project, Open up a terminal and execute these commands

```
$ mkdir NFT-Tutorial
$ cd  NFT-Tutorial
$ npm init --yes
$ npm install --save-dev hardhat
```

 In the same directory where you installed Hardhat run:

```
$ npx hardhat

```

If you are not on mac, please do this extra step and install these libraries as well :)


```
$  npm install --save-dev @nomiclabs/hardhat-waffle ethereum-waffle chai @nomiclabs/hardhat-ethers ethers
```
then
```
$ npm install @openzeppelin/contracts
```

don't forget to run this commandafter writing contract in /contracts 

```
$ npx hardhat compile
```
## Configuring Deployment
* Lets deploy the contract to rinkeby network. First, create a new file named deploy.js under scripts folder

* Now we would write some code to deploy the contract in deploy.js file.
  
```
// Import ethers from Hardhat package
const { ethers } = require("hardhat");

async function main() {
  /*
A ContractFactory in ethers.js is an abstraction used to deploy new smart contracts,
so nftContract here is a factory for instances of our GameItem contract.
*/
  const nftContract = await ethers.getContractFactory("GameItem");

  // here we deploy the contract
  const deployedNFTContract = await nftContract.deploy();

  // print the address of the deployed contract
  console.log("NFT Contract Address:", deployedNFTContract.address);
}

// Call the main function and catch if there is any error
main()
  .then(() => process.exit(0))
  .catch((error) => {
    console.error(error);
    process.exit(1);
  });
```
create .env file and add your Alchemy API Key & RINKEBY Private Key.

to install dotenv package
```
$ npm i dotenv
```
```
# Go to https://www.alchemyapi.io, sign up, create
# a new App in its dashboard and select the network as Rinkeby, and replace "add-the-alchemy-key-url-here" with its key url
ALCHEMY_API_KEY_URL="add-the-alchemy-key-url-here"

# Replace this private key with your RINKEBY account private key
# To export your private key from Metamask, open Metamask and
# go to Account Details > Export Private Key
# Be aware of NEVER putting real Ether into testing accounts
RINKEBY_PRIVATE_KEY="add-the-rinkeby-private-key-here"
```



Now open the hardhat.config.js file, we would add the rinkeby network here so that we can deploy our contract to rinkeby. Replace all the lines in the hardhat.config.js file with the given below lines

```
require("@nomiclabs/hardhat-waffle");
require("dotenv").config({ path: ".env" });

const ALCHEMY_API_KEY_URL = process.env.ALCHEMY_API_KEY_URL;

const RINKEBY_PRIVATE_KEY = process.env.RINKEBY_PRIVATE_KEY;

module.exports = {
  solidity: "0.8.4",
  networks: {
    rinkeby: {
      url: ALCHEMY_API_KEY_URL,
      accounts: [RINKEBY_PRIVATE_KEY],
    },
  },
};
```

To deploy in your terminal type:
```
$ npx hardhat run scripts/deploy.js --network rinkeby
```
Save the NFT Contract Address that was printed on your terminal in your notepad, you would need it.

Go to [Rinkeby Etherscan](https://rinkeby.etherscan.io/) and search for the address that was printed.

---
## try running following command to play with hardhat:

```shell
npx hardhat accounts
npx hardhat compile
npx hardhat clean
npx hardhat test
npx hardhat node
node scripts/sample-script.js
npx hardhat help
```
---

## To setup this project
```
$ git clone <repo-url>
$ cd <project-path>
$ npm install
OR
$ yarn install

```