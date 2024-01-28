
# SellerSpace Project

SellerSpace is a Java-based application providing a GraphQL interface to manage sellers, producer states, and marketplace data.

## System Requirements

- Java 17

## Running the Application

Follow these steps to run the application:

1. Navigate to the project directory:
   ```bash
   cd sellerspace
   ```
2. Start the application using Maven:
   ```bash
   mvn spring-boot:run
   ```
3. Access the GraphQL interface at [http://localhost:8080/graphiql?path=/graphql](http://localhost:8080/graphiql?path=/graphql)

## Database Configuration

The application requires a PostgreSQL database. Configure the database connection in `application.properties` for both testing and running the application.

## GraphQL API

The application exposes a GraphQL API for querying and managing seller data.

### Queries

- `sellers`: Fetches a pageable response of sellers based on filters and sorting criteria.

#### SellerFilter

```graphql
input SellerFilter {
    searchByName: String
    producerIds: [ID]
    marketplaceIds: [String]
}
```

#### PageInput

```graphql
input PageInput {
    page: Int!
    size: Int!
}
```

#### SellerSortBy

```graphql
enum SellerSortBy {
    SELLER_INFO_EXTERNAL_ID_ASC,
    SELLER_INFO_EXTERNAL_ID_DESC,
    NAME_ASC,
    NAME_DESC,
    MARKETPLACE_ID_ASC,
    MARKETPLACE_ID_DESC,
}
```

#### SellerPageableResponse

```graphql
type SellerPageableResponse {
    meta: PageMeta!
    data: [Seller!]!
}
```

### Types

#### Seller

```graphql
type Seller {
    sellerName: String
    externalId: String!
    producerSellerStates: [ProducerSellerState]!
    marketplaceId: String
}
```

#### ProducerSellerState

```graphql
type ProducerSellerState {
    producerId: ID!
    producerName: String!
    sellerState: SellerState!
    sellerId: ID!
}
```

#### SellerState

```graphql
enum SellerState {
    REGULAR
    WHITELISTED
    GREYLISTED
    BLACKLISTED
}
```

