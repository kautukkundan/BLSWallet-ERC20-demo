# BLS Wallet Demo App
<img width="1728" alt="Screenshot 2022-04-18 at 5 21 11 AM" src="https://user-images.githubusercontent.com/23727056/163737751-ed3ff178-c72a-4a3c-9d41-d10d1626f1f4.png">


## How to setup

1. deploy Generic ERC20 contract with minting ability

eg -

```solidity
//SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

import "@openzeppelin/contracts/token/ERC20/ERC20.sol";

contract Token is ERC20 {
    constructor(string memory name_, string memory symbol_)
        ERC20(name_, symbol_)
    {}

    function mint(address _account, uint256 _amount) public {
        _mint(_account, _amount);
    }
}

```

2. deploy a spender contract (any contract which can pull tokens from user)

eg -

```solidity
//SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

import "@openzeppelin/contracts/token/ERC20/IERC20.sol";

contract Spender {
    function pullTokens(address _token, uint256 _amount) public {
        IERC20(_token).transferFrom(msg.sender, address(this), _amount);
    }
}
```
can clone this repo - https://github.com/kautukkundan/generic-ERC20-spender
and run `npx hardhat run scripts/deploy.ts --network localhost`
make sure to deploy on the same network as BLS contracts

3. note the addresses for the 2 contracts
4. update `.env` file with the 2 addresses
5. run `yarn install`
6. run `yarn start`
7. connect Quill Wallet
