# Trade Quest - Cloud-Native Trading Simulator

A serverless trading simulator built on AWS that simulates real market dynamics using Finnhub API data, AI-generated news, and cloud-native architecture.

## Architecture Overview

```
┌─────────────┐
│   Finnhub   │
│     API     │
└──────┬──────┘
       │
       v
┌─────────────────────────────────────────────────────────┐
│                    AWS CLOUD                            │
│                                                         │
│  ┌─────────────┐    ┌──────────────┐                  │
│  │ EventBridge │───>│Step Functions│                  │
│  │  (Hourly)   │    │  Workflow    │                  │
│  └─────────────┘    └──────┬───────┘                  │
│                             │                           │
│                     ┌───────┴───────┐                  │
│                     │                │                  │
│              ┌──────v──────┐ ┌──────v────────┐        │
│              │  Finnhub    │ │    Price      │        │
│              │   Fetcher   │ │  Simulator    │        │
│              │   Lambda    │ │   Lambda      │        │
│              └──────┬──────┘ └───────┬───────┘        │
│                     │                 │                 │
│                     v                 v                 │
│              ┌─────────────────────────┐               │
│              │      S3 Buckets         │               │
│              │ (Market Data & News)    │               │
│              └──────────┬──────────────┘               │
│                         │                               │
│                         v                               │
│              ┌──────────────────┐                      │
│              │   News Generator │                      │
│              │  Lambda (AI)     │                      │
│              └──────────────────┘                      │
│                                                         │
│  ┌──────────────────────────────────────────────┐     │
│  │           API Gateway (HTTP)                 │     │
│  └──────────┬───────────────────────────────────┘     │
│             │                                           │
│      ┌──────┴──────────┬────────┬──────────┐          │
│      v                  v        v          v          │
│  ┌────────┐      ┌──────────┐ ┌──────┐ ┌─────────┐   │
│  │Get     │      │Execute   │ │Get   │ │Get      │   │
│  │Prices  │      │Trade     │ │News  │ │Portfolio│   │
│  │Lambda  │      │Lambda    │ │Lambda│ │Lambda   │   │
│  └────────┘      └──────────┘ └──────┘ └─────────┘   │
│      │                 │          │          │         │
│      └────────┬────────┴──────────┴──────────┘         │
│               v                                         │
│      ┌────────────────┐      ┌─────────────┐          │
│      │   DynamoDB     │      │   Cognito   │          │
│      │   Tables       │      │   (Auth)    │          │
│      └────────────────┘      └─────────────┘          │
└─────────────────────────────────────────────────────────┘
                          │
                          v
                 ┌─────────────────┐
                 │  Frontend HTML  │
                 │   (Browser)     │
                 └─────────────────┘
```

## Features

- **Real-Time Market Data**: Fetches live prices from Finnhub API every hour
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
5. **Finnhub API Key** (free tier available)
6. **Hugging Face API Key** (optional, falls back to templates)

## Project Structure

```
trade-quest/
├── terraform/
│   ├── main.tf              # Main infrastructure
│   ├── variables.tf         # Variable definitions
│   ├── outputs.tf          # Output values
│   ├── providers.tf        # Provider configuration
│   ├── versions.tf         # Version constraints
│   └── terraform.tfvars    # Your configuration values
├── lambda_functions/
│   ├── finnhub_fetcher/    # Fetches real market data
│   ├── price_simulator/    # Simulates price movements
│   ├── news_generator/     # Generates AI news
│   ├── api_get_prices/     # API: Get current prices
│   ├── api_get_news/       # API: Get latest news
│   ├── api_execute_trade/  # API: Execute trades
│   ├── api_get_portfolio/  # API: Get user portfolio
│   ├── api_get_leaderboard/# API: Get leaderboard
│   └── session_checker/    # Check active sessions
├── frontend/
│   ├── index.html          # Main webpage
│   ├── style.css           # Styling
│   └── app.js              # JavaScript logic              
├── deploy.yml              # Deployment script
└── README.md               # This file
```


