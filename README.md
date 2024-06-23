# Mall Smart Contract

This Solidity smart contract simulates a simple mall system with functionalities to set product prices, update stock, and ensure minimum stock availability. The contract includes mechanisms to restrict access to certain functions to the contract owner and emits events on state changes.

## Features

- Set prices for different categories of products: electronics, clothing, and groceries.
- Ensure minimum stock availability using assertions.
- Update stock with checks to ensure stock does not fall below a minimum threshold.
- Emit events when product prices or stock levels change.

## Contract Details

### State Variables

- uint256 public productPrice: Stores the current product price.
- uint256 public stock: Stores the current stock level.
- address public owner: Stores the owner's address.

### Events

- event PriceChanged(uint256 newPrice): Emitted when the product price is updated.
- event StockChanged(uint256 newStock): Emitted when the stock level is updated.

### Modifiers

- modifier onlyOwner(): Restricts access to certain functions to the contract owner.

### Functions

#### Constructor

- constructor(): Initializes the contract by setting the deployer as the owner.

#### Price Setting Functions

- function setElectronicsPrice(uint256 newPrice) external onlyOwner: Sets the price for electronics, ensuring it is above 500.
- function setClothingPrice(uint256 newPrice) external onlyOwner: Sets the price for clothing, ensuring it is above 100.
- function setGroceryPrice(uint256 newPrice) external onlyOwner: Sets the price for groceries, ensuring it is above 50.

#### Stock Functions

- function checkMinimumStock() external view: Ensures that the stock level is always above a minimum threshold of 10.
- function updateStock(uint256 newStock) external onlyOwner: Updates the stock level, reverting the transaction if the new stock is below 5.

## Usage

### Deployment

To deploy the contract, ensure you have a Solidity development environment set up (such as Remix or Truffle) and deploy the Mall contract.

### Interacting with the Contract

1. *Setting Prices*: Use the setElectronicsPrice, setClothingPrice, and setGroceryPrice functions to set the prices for different categories. Only the owner can call these functions.
2. *Updating Stock*: Use the updateStock function to update the stock level. Only the owner can call this function.
3. *Checking Minimum Stock*: Use the checkMinimumStock function to verify that the stock level is above the minimum threshold. This function can be called by anyone.

### Usage of require, revert, and assert

#### require

The require statement is used to validate conditions and inputs. If the condition is not met, the function execution is stopped, and the remaining gas is refunded. The contract state is also reverted to its previous state.

Examples in the contract:

- require(newPrice > 500, "Price for electronics must be above 500"); in the setElectronicsPrice function.
- require(newPrice > 100, "Price for clothing must be above 100"); in the setClothingPrice function.
- require(newPrice > 50, "Price for groceries must be above 50"); in the setGroceryPrice function.
- require(msg.sender == owner, "Caller is not the owner"); in the onlyOwner modifier.

#### revert

The revert statement is used to flag an error and revert the transaction. It is typically used for complex conditions that cannot be handled by require.

Example in the contract:

- if (newStock < 5) { revert("Stock cannot be less than 5 units."); } in the updateStock function.

#### assert

The assert statement is used to check for conditions that should never be false. If the condition is false, it indicates a bug in the contract, and the transaction is reverted. The remaining gas is not refunded.

Example in the contract:

- assert(stock >= 10); in the checkMinimumStock function. This ensures that the stock level is always above 10, which should be a guaranteed condition.
