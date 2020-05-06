# Etherplex

Ethers.js + Maker's Multicall

Batch your calls together using Etherplex.

# Setup

```bash
$ yarn add @pooltogether/etherplex
```

# Usage

```javascript
import { ethers } from 'ethers'
import { batch, contract } from '@pooltogether/etherplex'

// Assuming PoolAbi is an ABI
// Assume the DAI_ADDRESS and USDC_ADDRESS constants are Ethereum addresses

let daiContract = contract('DaiPool', PoolAbi, DAI_ADDRESS)

// Alternatively, you can just pass in an ethers.Contract instance
let ethersContract = new ethers.Contract(USDC_ADDRESS, PoolAbi, provider)

let usdcContract = contract('UsdcPool', ethersContract)

batch(
  ethers.getDefaultProvider(),
  daiContract
    .totalBalanceOf(address),
  usdcContract
    .totalBalanceOf(address)
).then(results => {
  console.log('Your data', results)
}).catch(e => {
  console.error('Uh-or read error', e)
})
/*
Will yield:

{
  DaiPool: {
    'totalBalanceOf(address)': [BigNumber],
    totalBalanceOf: [BigNumber],
  },
  UsdcPool: {
    'totalBalanceOf(address)': [BigNumber],
    totalBalanceOf: [BigNumber],
  }
}

*/
```
