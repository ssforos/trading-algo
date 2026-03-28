# Repository Analysis

This repository contains a Python-based framework for algorithmic trading. Here's a breakdown of what's inside and the key strategies:

### What's in the Repository?

*   **Core Functionality:** The project is designed to run automated trading strategies, connecting to brokerage accounts to execute trades.
*   **Strategies:** It comes with two pre-built trading strategies:
    1.  **Survivor Strategy (`strategy/survivor.py`):** An options-selling strategy that reacts to price movements in the NIFTY index. It sells PUT options when the index rises and CALL options when it falls, based on configurable price "gaps."
    2.  **Wave Strategy (`strategy/wave.py`):** A strategy that continuously places buy and sell orders around the current market price, creating a "wave." It includes risk management based on the overall portfolio's delta.
*   **Broker Integrations (`brokers/`):** The code is designed to be modular and supports different brokers. It currently has integrations for:
    *   Fyers
    *   Zerodha
*   **Order and Data Management:**
    *   `dispatcher.py`: Handles routing of real-time market data to the strategies.
    *   `orders.py`: Manages order tracking and status.

### Key Strategies Explained

1.  **The Survivor Strategy:**
    *   **Goal:** To systematically sell options and collect premiums.
    *   **Method:** It establishes a reference price for the NIFTY index. When the index moves up by a predefined amount (the "gap"), it sells a PUT option. When it moves down by the gap, it sells a CALL option.
    *   **Risk Management:** The strategy adjusts its reference price after each trade to avoid accumulating too many positions on one side. It also has a "reset" mechanism to adapt to larger market trends.

2.  **The Wave Strategy:**
    *   **Goal:** To capture profits from small price fluctuations (scalping).
    *   **Method:** It places both a buy order below the current market price and a sell order above it. When one order is filled, the other is typically cancelled, and a new "wave" of orders is placed.
    *   **Risk Management:** This strategy includes a sophisticated risk management layer that calculates the portfolio's overall "delta" (a measure of directional risk). If the delta exceeds certain thresholds, it will restrict new buy or sell orders to prevent taking on too much risk in one direction.

In short, this repository provides a foundation for building and running automated trading strategies, with two distinct examples already implemented. You can configure it with your broker credentials and run the strategies from the command line.
