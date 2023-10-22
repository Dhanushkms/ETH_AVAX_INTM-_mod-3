# ERC20 Token Contract

## Description
This is a simple ERC20 token contract written in Solidity. ERC20 is a standard interface for fungible tokens on the Ethereum blockchain. The contract contains the implementation of basic functionalities such as minting, burning, and transferring tokens. It also includes a constructor for initializing token metadata and an owner variable to manage permissions.

## Getting Started

To use this contract, you can deploy it on Remix, an online Solidity IDE.

1. Go to the Remix website at https://remix.ethereum.org/.
2. Create a new file by clicking on the "+" icon in the left-hand sidebar. Save the file with a .sol extension (e.g., myToken.sol).
3. Copy and paste the provided code into the file.
4. Make sure the Solidity compiler version is set to "0.8.0" or a compatible version
5. Compile the code by clicking on the "Solidity Compiler" tab and then clicking "Compile myToken.sol."
6. Deploy the contract by clicking on the "Deploy & Run Transactions" tab. Select the "myToken" contract from the dropdown menu and click "Deploy."

## ERC20 Token Functions

1. **Constructor:** Initializes the token metadata, including name, symbol, decimals, and initial supply. It also assigns the total supply to the owner's balance.

2. **Mint Function:** Allows the owner to create new tokens. Only the contract owner can call this function. It increases the balance of the recipient and the total supply by the specified amount.

3. **Burn Function:** Enables users to destroy tokens. It decreases the balance of the caller and the total supply by the specified amount. The function checks if the caller has a sufficient balance before performing the burn operation.

4. **Transfer Function:** Facilitates the transfer of tokens from the caller's address to the specified recipient's address. It checks whether the caller has a sufficient balance before executing the transfer operation.

```javascript
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

import "@openzeppelin/contracts/token/ERC20/ERC20.sol";

contract myToken is ERC20 {
    address public owner;

    constructor(
        string memory name,
        string memory symbol,
        uint8 decimals,
        uint256 initialSupply
    ) ERC20(name, symbol) {
        _mint(msg.sender, initialSupply * (10**decimals));
        owner = msg.sender;
    }

    function mint(address to, uint256 amount) public {
        require(msg.sender == owner, "Only the owner can mint tokens.");
        _mint(to, amount);
    }

    function burn(uint256 amount) public {
        _burn(msg.sender, amount);
    }

    function transfer(address to, uint256 amount) public override returns (bool) {
        _transfer(msg.sender, to, amount);
        return true;
    }
}

```

## Author

Dhanush km

dhamushkm@gmail.com

## License

This project is licensed under the MIT License - see the LICENSE.md file for details.
