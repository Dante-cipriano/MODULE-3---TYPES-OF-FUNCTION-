# MyModule3 Solidity Contract Types of functions

# Overview
MyModule3 is a Solidity smart contract that extends the ERC20 token standard provided by OpenZeppelin's library. It introduces additional functionalities such as custom transfer events, burning tokens, and minting tokens.

# Function
Transfer: Extends the default transfer function of ERC20 to emit a custom transfer event.

Burn: Allows the owner to burn a specific amount of tokens from their own balance.

Mint: Allows the owner to mint a specific amount of tokens and assign them to a specified address.

# Owner
The owner of this contract is Dante Cipriano.

# Usage
This contract can be used in the Remix IDE or any other Ethereum development environment that supports Solidity smart contracts.

# License
This contract is licensed under the MIT License.

// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

import "@openzeppelin/contracts/token/ERC20/ERC20.sol";

contract MyModule3 is ERC20 {
    event TransferCustom(address indexed from, address indexed to, uint256 value);
    event Burn(address indexed burner, uint256 value);
    event Mint(address indexed to, uint256 value);

    constructor() ERC20("dantee", "DRCTOKEN") {
        _mint(msg.sender, 200 * (2 * uint256(decimals())));
    }

    function transfer(address recipient, uint256 amount) public virtual override returns (bool) {
        bool success = super.transfer(recipient, amount);
        if (success) {
            emit TransferCustom(msg.sender, recipient, amount);
        }
        return success;
    }

    function burn(uint256 amount) public {
        _burn(msg.sender, amount);
        emit Burn(msg.sender, amount);
    }

    function mint(address to, uint256 amount) public {
        _mint(to, amount);
        emit Mint(to, amount);
    }
}
