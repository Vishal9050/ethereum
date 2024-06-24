# Smart Contract for MyToken

This Solidity smart contract is responsible for creating a standard fungible token that includes features such as minting, burning, and access control.

## Description

This agreement establishes the fundamental framework for developing a custom token on a blockchain network. It enables the specification of a token's name, abbreviation, and initial total supply. Token holders can maintain token balances, while the contract includes capabilities for creating new tokens (limited to the owner) and eliminating existing tokens (subject to a balance verification).

## Getting Started

### Executing program

To run this program, you can use Remix, an online Solidity IDE. To get started, go to the Remix website at https://remix.ethereum.org/.

Once you are on the Remix website, create a new file by clicking on the "+" icon in the left-hand sidebar. Save the file with a .sol extension (e.g., MyToken.sol). Copy and paste the following code into the file:

```javascript

Solidity
// SPDX-License-Identifier: MIT
 pragma solidity 0.8.18;

contract MyToken {

  // Public variables here
  string public tokenName = 'Meta';
  string public tokenAbbrv ='MTA';
  uint public totalSupply = 0;

  // Mapping variable here
  mapping(address => uint) public balances;

  // Owner address for access control
  address public owner;

  // Event to emit when tokens are minted
  event Minted(address indexed to, uint256 amount);

  // Event to emit when tokens are burned
  event Burned(address indexed from, uint256 amount);

  // constructor to set the owner
  constructor() {
    owner = msg.sender;
  }

  // mint function with access control
  function mint(address _address, uint _value) public onlyOwner {
    totalSupply += _value;
    balances[_address] += _value;
    emit Minted(_address, _value);
  }

  // burn function with access control and safety check
  function burn(address _address, uint _value) public {
    require(balances[_address] >= _value, "Insufficient balance");
    totalSupply -= _value;
    balances[_address] -= _value;
    emit Burned(_address, _value);
  }

  // modifier to restrict functions to owner only
  modifier onlyOwner() {
    require(msg.sender == owner, "Only owner can call this function");
    _;
  }
}

```

To compile the code, click on the "Solidity Compiler" tab in the left-hand sidebar. Make sure the "Compiler" option is set to "0.8.18" (or another compatible version), and then click on the "Compile MyToken.sol" button.

Once the code is compiled, you can deploy the contract by clicking on the "Deploy & Run Transactions" tab in the left-hand sidebar. 




## Usage

**Functions:**

- `mint(address _address, uint _value)` (onlyOwner): This mints a given amount of `tokens(_value)` to an account(`_address`).

- burn(address _address, uint _value) : Burns an amount of tokens (_value) of the address_sufficient determination(_address), allowing to check on every transaction if the balance is enough

## Help

**Common Issues:**

Insufficient Balance: Make sure the address, which is attempting to burn tokens have enough balance as the function `burn` has no way of failing when trying to reduce an amount greater than its balance.

Unauthorized Minting: Minion can not mint with out calling the function: Only the contract owner is able to `mint` this is set by our access control modifier.

## Authors

Contributors names and contact info.

Name:Vishal Mittal

Gmail:Vishalmittal262003@gmail.com
