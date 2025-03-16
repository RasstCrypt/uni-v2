# Uniswap SDK



In-depth documentation on this SDK is available at [uniswap.org](https://uniswap.org/docs/v2/SDK/getting-started/).

## Running tests

To run the tests, follow these steps. You must have at least node v10 and [yarn](https://yarnpkg.com/) installed.

First clone the repository:

```sh
git clone https://github.com/Uniswap/uniswap-sdk.git
```

Move into the uniswap-sdk working directory

```sh
cd uniswap-sdk/
```

Install dependencies

```sh
yarn install
```

Run tests

```sh
yarn test
```

You should see output like the following:

```sh
yarn run v1.22.4
$ tsdx test
 PASS  test/constants.test.ts
 PASS  test/pair.test.ts
 PASS  test/fraction.test.ts
 PASS  test/miscellaneous.test.ts
 PASS  test/entities.test.ts
 PASS  test/trade.test.ts

Test Suites: 1 skipped, 6 passed, 6 of 7 total
Tests:       3 skipped, 82 passed, 85 total
Snapshots:   0 total
Time:        5.091s
Ran all test suites.
✨  Done in 6.61s.
```
## Make changes to the constants.ts file
After installing all the SDK dependencies, let’s start modifying the files so that they will work with the smart contract we deployed earlier on the EVM chain of our choice. In our case, we will be using the Polygon Mumbai chain.

Go to src/constants.ts

Add the chain ID of the network where your smart contracts were deployed to the ChainId enum. The Polygon Mumbai chain id is 80001.

Change the value of the FACTORY_ADDRESS to the factory address of the factory smart contract you deployed on the Mumbai network.

Change the value of the INIT_CODE_HASH. The value is gotten from the Factory contract we had deployed in the previous article.

## Update the token.ts file
Go to src/entities/token.ts

From line 59 you will see a WETH constant. Add the ChainId and address of the Wrapped native token of the blockchain you are building for. In our case, we are building a swap for the Polygon Mumbai network. Remember that we had deployed WETH earlier in the previous article, that’s the contract address we will be using here.

## Update the currency.ts file
The only reason why we are modifying the currency.ts file is because the Polygon Mumbai network doesn’t use Ether (ETH) as its native currency. Otherwise, if the chain uses ETH as native currency, there will be no need to modify the currency.ts file.

Go to src/entities/currency.ts

## Build the SDK - to be used by the UniswapV2 Interface
The last step is to build the UniswapV2 SDK after making all the necessary modifications. The UniswapV2 Interface/Frontend will use the build to interact with the smart contracts we deployed earlier.

Run yarn build in your VSCode terminal

After a successful build, you will see a dist folder in the list of folders on your VSCode

At this point, you have successfully modified the UniswapV2 SDK to work on the Polygon Mumbai network.






## Uni Interswap Conf






## Point the v2-sdk dependency to the locally modified v2-sdk
Remember that the UniswapV2 frontend interface depends on the v2-sdk to interact with the deployed smart contracts. Now that we have modified our v2-sdk to work on the Polygon Mumbai network, we also need to point the UniswapV2 interface to work with the v2-sdk we modified. This will be done in the UniswapV2 interface package.json.

Open VSCode on the UniswapV2 interface

Open the package.json file

Find @uniswap/sdk under devDependencies

Change the value from 3.0.3-beta.1 to file:../v2-sdk

Ensure that you have the v2-sdk folder and the UniswapV2 interface folder in the same directory, just like in the image above.

In the VSCode terminal, run: yarn. This will install all the dependencies and will make use of the modified v2-sdk as the sdk dependency for the UniswapV2 interface.

## Update the src/constants/index.ts file
Go to src/constants/index.ts

Change the value of the ROUTER_ADDRESS constant to the address of the Router02.sol contract that was deployed earlier in the previous article.

Add MUMBAI ChainId to the WETH_ONLY constant.


## Update the src/connectors/index.ts file
Locate src/connectors/index.ts

Inside the file, find an array named supportedChainIds

Add the Polygon Mumbai network ID to the array. This specifies the chain IDs that the swap will support. So if you want it to work with only Polygon Mumbai, remove all the other values in the array and leave only the Polygon Mumbai ID.

You can also modify the appName to any preferred name you may want to name your swap. For this article, I will call mine Posiedonswap

The appLogoUrl is the URL of the logo for the swap.

## Update the src/constants/multicall/index.ts file
Locate: src/constants/multicall/index.ts

Add MUMBAI as ChainId and the contract address of the Multicall smart contract we deployed earlier.

## Update the src/components/Header/index.ts file
Go to src/components/Header/index.ts

Find NETWORK_LABELS constant, add MUMBAI to the list of network labels.

## Update the src/constants/v1/index.ts file
Locate src/constants/v1/index.ts

Inside the above file, find V1_FACTORY_ADDRESSES, add the MUMBAI chainID, and set the value to the address of the Factory contract we deployed earlier.

## Update the src/state/lists/hooks.ts file
Locate src/state/lists/hooks.ts

Find a constant named EMPTY_LIST, add ChainId.MUMBAI to the list

## Update the src/utils/index.ts file
Locate src/utils/index.ts

Find a constant inside the file named: ETHERSCAN_PREFIXES, add the Mumbai chainId and modify it to look like the image below:

## Run the UniswapV2 Frontend
After making the necessary changes to the UniswapV2 interface to make it work with our preferred blockchain (Polygon Mumbai), let’s now run the application.

To run the UniswapV2 frontend, run yarn start in your VSCode terminal.

NOTE: Make sure that you are using node version 14. You can switch between node versions using Node Version Manager (NVM)


## 
