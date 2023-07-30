# Create-and-Mint-Token
A smart contract to create your own token and deploy it using Remix.
# ERC20 Token Contract

This is a simple ERC20 token contract written in Solidity. The contract allows you to create your own custom token with the ability to mint, transfer, and burn tokens. The contract owner has the privilege to mint new tokens, while any user can transfer and burn tokens.

### Prerequisites

- An Ethereum development environment like Remix IDE.

## Code : 
     // SPDX-License-Identifier: MIT
     pragma solidity ^0.8.0;

    contract MyToken {
    string public name;
    string public symbol;
    uint256 public totalSupply;

    mapping(address => uint256) public balanceOf;

    address public owner;

    event Transfer(address indexed from, address indexed to, uint256 value);
    event Burn(address indexed from, uint256 value);
    event Mint(address indexed to, uint256 value);

    constructor(
        string memory tokenName,
        string memory tokenSymbol,
        uint256 initialSupply
    ) {
        name = tokenName;
        symbol = tokenSymbol;
        totalSupply = initialSupply;
        balanceOf[msg.sender] = totalSupply;
        owner = msg.sender;
    }

    modifier onlyOwner() {
        require(msg.sender == owner, "Only the contract owner can perform this action");
        _;
    }

    function transfer(address to, uint256 amount) public returns (bool) {
        require(to != address(0), "Invalid address");
        require(amount > 0, "Amount should be greater than zero");
        require(balanceOf[msg.sender] >= amount, "Insufficient balance");

        balanceOf[msg.sender] -= amount;
        balanceOf[to] += amount;

        emit Transfer(msg.sender, to, amount);
        return true;
    }

    function burn(uint256 amount) public returns (bool) {
        require(amount > 0, "Amount should be greater than zero");
        require(balanceOf[msg.sender] >= amount, "Insufficient balance");

        balanceOf[msg.sender] -= amount;
        totalSupply -= amount;

        emit Burn(msg.sender, amount);
        emit Transfer(msg.sender, address(0), amount);
        return true;
    }

    function mint(address to, uint256 amount) public onlyOwner {
        require(to != address(0), "Invalid address");
        require(amount > 0, "Amount should be greater than zero");

        balanceOf[to] += amount;
        totalSupply += amount;

        emit Mint(to, amount);
        emit Transfer(address(0), to, amount);
    }
    }

## Walkover Video: 
https://www.loom.com/share/997fc0b388734e7bb13f89422c24e3e5?sid=62c1c725-f5e0-4c5c-8c58-371045195eb1

## Getting Started

To deploy and interact with this ERC20 token contract, follow the steps below:


Apologies for the confusion. Here are the steps to deploy and interact with the ERC20 token contract named "Create_and_Mint_Token.sol" on Remix IDE:

1. **Open Remix IDE:**
   - Go to the Remix IDE website: https://remix.ethereum.org/.

2. **Create a New File:**
   - Click on the "+" icon in the file explorer to create a new file.
   - Name the file "Create_and_Mint_Token.sol" and press Enter.

3. **Copy and Paste the Solidity Code:**
   - Copy the ERC20 token contract code provided in the previous responses.
   - Paste the code into the "Create_and_Mint_Token.sol" file.

4. **Compile the Contract:**
   - In Remix, go to the "Solidity Compiler" tab on the left-hand side.
   - Select the appropriate compiler version (e.g., 0.8.0).
   - Click on "Compile Create_and_Mint_Token.sol" to compile the contract.

5. **Deploy the Contract:**
   - Go to the "Deploy & Run Transactions" tab on the left-hand side.

6. **Select the Environment:**
   - Under the "Environment" dropdown, choose "Injected Web3" to connect Remix Provided wallets.

7. **Deploy the Contract:**
   - Choose an Ethereum account to deploy the contract (this will be the contract owner).
   - In the "Deploy" section, click on the "Deploy" button.
   - Confirm the transaction in your Ethereum wallet when prompted.

8. **Interact with the Contract:**
   - After the contract is successfully deployed, you will see the contract interface on the right-hand side.

9. **Mint Tokens (Only for Contract Owner):**
   - In the contract interface, locate the "mint" function.
   - Enter the address of the recipient in the "to" field.
   - Enter the number of tokens to mint in the "amount" field.
   - Click on "transact" to mint tokens and assign them to the specified address.

10. **Transfer Tokens (Any User):**
    - In the contract interface, locate the "transfer" function.
    - Enter the recipient's address in the "to" field.
    - Enter the number of tokens to transfer in the "amount" field.
    - Click on "transact" to transfer tokens to the specified address.

11. **Burn Tokens (Any User):**
    - In the contract interface, locate the "burn" function.
    - Enter the number of tokens to burn in the "amount" field.
    - Click on "transact" to burn the specified number of tokens.

## Contract Details

- **Name:** The name of the token.
- **Symbol:** The symbol of the token (e.g., XYZ).
- **Total Supply:** The total supply of tokens initially available.
- **Balance Of:** A mapping that tracks the token balance of each address.

## Owner Privileges

The contract owner has the following privileges:

- Minting new tokens and assigning them to a specific address.

## Security Considerations

- Before deploying the contract to a production environment, conduct thorough testing and security audits to avoid potential vulnerabilities.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.
