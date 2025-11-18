# Trade Quest - Cloud-Native Trading Simulator

A serverless trading simulator built on AWS that simulates real market dynamics using Yahoo Finance API data, AI-generated news, and cloud-native architecture.

## Architecture Overview
<img width="3034" height="1317" alt="image" src="https://github.com/user-attachments/assets/9308a0a7-b138-4051-b2ca-0d3c87527840" />


## Features

- **Real-Time Market Data**: Fetches live prices from Yahoo Finance API every hour
- **Price Simulation**: Uses Geometric Brownian Motion to generate realistic price movements
- **AI-Generated News**: Creates contextual market news using Hugging Face API
- **Trading Engine**: Buy/sell assets with portfolio tracking and P/L calculation
- **Leaderboard**: Compete with other users based on trading performance
- **Serverless Architecture**: Fully managed AWS services with auto-scaling
- **Event-Driven**: Automated workflows using EventBridge and Step Functions

## Prerequisites

Before deployment, ensure you have:

1. **AWS Account** with appropriate permissions
2. **AWS CLI** configured with credentials
3. **Terraform** (v1.6.0 or higher)
4. **Python 3.11** or higher
5. **Yahoo Finance API Key** 
6. **Hugging Face API Key** (optional, falls back to templates)




