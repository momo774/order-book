# Order Book System
This is an implementation of an order book system in C++. An order book is a critical component in electronic trading platforms, where buy and sell orders for financial instruments are collected, matched, and executed.

## Features

- Support for different order types: Good-Till-Canceled (GTC), Fill-and-Kill (FAK), Fill-or-Kill (FOK), Good-for-Day (GFD), and Market orders.
- Matching engine that matches buy and sell orders based on price-time priority.
- Order modification and cancellation capabilities.
- Thread-safe implementation using mutexes and condition variables.
- Separate thread for pruning Good-for-Day orders after the market closes.
- Comprehensive test suite using Google Test framework.

## Project Structure

- `main.cpp`: Entry point of the application (minimal implementation provided).
- `Orderbook.h`, `Orderbook.cpp`: Implementation of the core `Orderbook` class.
- `Order.h`: Definition of the `Order` class, representing an individual order.
- `OrderModify.h`: Definition of the `OrderModify` class, representing a modification to an existing order.
- `Trade.h`, `TradeInfo.h`: Definitions of the `Trade` and `TradeInfo` classes/structs, representing trades and trade information.
- `OrderbookLevelInfos.h`, `LevelInfo.h`: Definitions of classes/structs for representing order book level information.
- `OrderType.h`, `Side.h`: Definitions of enumerations for order types and order sides.
- `Usings.h`, `Constants.h`: Type aliases and constant definitions.
- `test.cpp`, `pch.h`, `pch.cpp`: Test suite implementation using Google Test framework.

## Build and Run

1. Install a C++ compiler and build tools (e.g., Visual Studio, GCC, Clang).
2. Install the Google Test package if you want to run the test suite.
3. Configure your build system (e.g., Makefile, Visual Studio Code tasks, Visual Studio project) to compile the source files and link against the required libraries.
4. Build the project.
5. Run the compiled executable or test runner.

## Usage

The `Orderbook` class is the main entry point for interacting with the order book system. Here's a basic example of how to use it:

```cpp
#include "Orderbook.h"

int main() {
    Orderbook orderbook;

    // Add a buy order
    auto order1 = std::make_shared<Order>(OrderType::GoodTillCancel, 1, Side::Buy, 100, 10);
    orderbook.AddOrder(order1);

    // Add a sell order
    auto order2 = std::make_shared<Order>(OrderType::FillAndKill, 2, Side::Sell, 100, 5);
    auto trades = orderbook.AddOrder(order2);

    // Cancel an order
    orderbook.CancelOrder(1);

    // Modify an order
    OrderModify modifiedOrder(2, Side::Sell, 101, 3);
    trades = orderbook.ModifyOrder(modifiedOrder);

    // Get the current order book state
    auto orderInfos = orderbook.GetOrderInfos();
    // ... (Process the order book state)

    return 0;
}

```
## License
This project is licensed under the MIT License.
