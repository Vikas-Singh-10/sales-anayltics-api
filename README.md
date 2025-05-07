# Sales & Revenue Analytics API

A GraphQL API built with NestJS and MongoDB Atlas for analyzing e-commerce sales, customer spending, and product trends.

## Features
- **Customer Spending Analytics**: Track total, average, and last purchase for any customer.
- **Top-Selling Products**: Get the most popular products by quantity sold.
- **Sales Analytics**: Revenue, completed orders, and category breakdown for any date range.
- **MongoDB Aggregation**: Efficient, real-time analytics using MongoDB pipelines.

## Prerequisites
- Node.js (v14 or higher)
- npm
- MongoDB Atlas account (or local MongoDB for testing)

## Setup Instructions

1. **Clone the repository:**
   ```bash
   git clone <repository-url>
   cd sales-analytics-api
   ```

2. **Install dependencies:**
   ```bash
   npm install
   ```

3. **Configure MongoDB Atlas:**
   - Create a cluster and database in MongoDB Atlas.
   - Get your connection string.
   - In `src/app.module.ts`, replace `YOUR_MONGODB_ATLAS_URI` with your connection string.

4. **Import Seed Data:**
   - Download the seed data from the assignment link.
   - Import the CSV files into your MongoDB database using MongoDB Compass or the `mongoimport` CLI.
   - Ensure collections are named `customers`, `products`, and `orders` (all lowercase).
   - Make sure all `_id` and referenced `productId`/`customerId` fields are of type `ObjectId`.

5. **Start the server:**
   ```bash
   npm run start:dev
   ```
   The GraphQL Playground will be available at [http://localhost:3000/graphql](http://localhost:3000/graphql)

## Example GraphQL Queries

### 1. Get Customer Spending
```graphql
query {
  getCustomerSpending(customerId: "<customer_id>") {
    customerId
    totalSpent
    averageOrderValue
    lastOrderDate
  }
}
```

### 2. Get Top Selling Products
```graphql
query {
  getTopSellingProducts(limit: 3) {
    productId
    name
    totalSold
  }
}
```

### 3. Get Sales Analytics
```graphql
query {
  getSalesAnalytics(startDate: "2024-01-01", endDate: "2024-12-31") {
    totalRevenue
    completedOrders
    categoryBreakdown {
      category
      revenue
    }
  }
}
```

## Testing & Troubleshooting
- Use the GraphQL Playground for interactive testing.
- If a query returns an empty array, check:
  - Orders have `status: "completed"`.
  - Product and customer references are correct and of type `ObjectId`.
  - Collection names are all lowercase.
  - The server is connected to the correct database.
- To test with Postman, use a POST request with a JSON body:
  ```json
  {
    "query": "query { getTopSellingProducts(limit: 3) { productId name totalSold } }"
  }
  ```

## Project Structure
```
src/
├── models/       # Mongoose schemas
├── resolvers/    # GraphQL resolvers
├── types/        # GraphQL object types
├── schema/       # GraphQL schema (SDL)
└── app.module.ts # Main application module
```

## Notes
- For best results, ensure all IDs in your seed data are imported as `ObjectId`.
- The API is ready for extension (mutations, pagination, caching) as per bonus requirements.

## License
MIT
