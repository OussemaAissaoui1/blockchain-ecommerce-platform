# Blockchain E-Commerce Platform

A full-stack e-commerce platform with integrated Ethereum blockchain payments, built with Node.js, Express, MongoDB, and Solidity smart contracts.

## Overview

**EnsiB E-commerce** is a multi-vendor marketplace where customers can browse products, place orders, and pay using Ethereum (via a local Ganache blockchain). Transactions are recorded on-chain through Solidity smart contracts, ensuring transparency and immutability. The platform supports three user roles: **Client**, **Vendor**, and **Admin**.

## Features

- **Blockchain Payments** — Orders are paid in ETH via smart contracts deployed on Ganache, with on-chain transaction recording
- **Multi-Vendor Marketplace** — Vendors register, list products, and manage their orders independently
- **Platform Fee System** — Configurable platform fee (default 2.5%) automatically deducted from each transaction
- **Order Lifecycle** — Full status tracking: Placed → Processing → Shipped → Delivered (with Cancel/Refund support)
- **Vendor Wallet** — Vendors accumulate balances on-chain and can withdraw ETH earnings
- **JWT Authentication** — Secure login and route protection via JSON Web Tokens
- **File Uploads** — Product images and profile photos via Multer

## Tech Stack

| Layer | Technology |
|-------|------------|
| **Backend** | Node.js, Express.js |
| **Database** | MongoDB Atlas (Mongoose) |
| **Blockchain** | Solidity ^0.8.17, Ganache, Web3.js |
| **Frontend** | HTML, CSS, SCSS, JavaScript |
| **Auth** | JWT, bcrypt |
| **Other** | Multer, Axios, node-cron |

## Project Structure

```
├── api/                    # REST API routes
│   ├── user.js             # User registration, login, profile
│   ├── products.js         # Product CRUD operations
│   └── orders.js           # Order management
├── contracts/              # Solidity smart contracts
│   ├── contract.sol        # Main EnsiBEcommerce contract (vendors, clients, orders, fees)
│   ├── Transaction.sol     # Purchase recording contract
│   ├── deploy.js           # Contract deployment script
│   └── artifacts/          # Compiled contract ABIs
├── middleware/
│   └── auth.js             # JWT authentication middleware
├── services/
│   ├── ganachePayment.js   # Web3 payment service (sign & send transactions)
│   └── blockchainSync.js   # Blockchain synchronization service
├── public/                 # Frontend static files
│   ├── index.html          # Homepage
│   ├── cart.html           # Shopping cart
│   ├── checkout.html       # Checkout & payment
│   ├── category.html       # Product categories
│   ├── single-product.html # Product detail page
│   ├── tracking.html       # Order tracking (client)
│   ├── vendortracking.html # Order tracking (vendor)
│   ├── vendor product.html # Vendor product management
│   ├── css/ js/ scss/ img/ fonts/ vendors/
│   └── ...
├── uploads/                # Uploaded images
├── server.js               # Express app entry point
├── register-vendor.js      # Vendor registration utility
├── setup-ganache-payment.js # Ganache payment setup
├── compiler_config.json    # Solidity compiler configuration
└── package.json
```

## Smart Contracts

### EnsiBEcommerce (`contract.sol`)
The main platform contract handling:
- Vendor & client registration with role-based access
- Order placement with automatic ETH payment splitting (vendor payout + platform fee)
- Order status updates and refund processing
- Vendor balance tracking and fund withdrawal

### Transaction (`Transaction.sol`)
A lightweight contract for recording purchase transactions on-chain with buyer, seller, amount, and timestamp.

## Getting Started

### Prerequisites
- Node.js
- MongoDB Atlas account (or local MongoDB)
- [Ganache](https://trufflesuite.com/ganache/) (local Ethereum blockchain)

### Installation

```bash
git clone https://github.com/OussemaAissaoui1/blockchain-ecommerce-platform.git
cd blockchain-ecommerce-platform
npm install
```

### Configuration

Create a `.env` file with:

```env
PORT=3001
MONGODB_URI=your_mongodb_connection_string
GANACHE_URL=http://localhost:7545
TRANSACTION_CONTRACT_ADDRESS=your_deployed_contract_address
JWT_SECRET=your_jwt_secret
```

### Run

```bash
# Start Ganache first, then:
npm start
# or for development:
npm run dev
```

The app will be available at `http://localhost:3001`.

## API Endpoints

| Method | Route | Description |
|--------|-------|-------------|
| `POST` | `/api/user/register` | Register a new user |
| `POST` | `/api/user/login` | Authenticate user |
| `GET` | `/api/products` | List products |
| `POST` | `/api/products` | Create a product (vendor) |
| `POST` | `/api/orders` | Place an order |
| `GET` | `/api/orders` | Get orders |
| `GET` | `/health` | Health check |
