# GraphQL with Spring Boot

A beginner-friendly project demonstrating how to integrate **GraphQL** with **Spring Boot** using the official `spring-boot-starter-graphql` library. It exposes a simple Books API with query and mutation support, backed by an in-memory H2 database.

---

## Tech Stack

| Technology | Version |
|---|---|
| Java | 16 |
| Spring Boot | 2.7.2 |
| Spring GraphQL | (via starter) |
| Spring Data JPA | (via starter) |
| H2 Database | In-memory |
| Lombok | Latest |
| Maven | Wrapper included |

---

## Project Structure

```
src/
└── main/
    ├── java/com/graphql/learn/
    │   ├── GraphqlProjectApplication.java   # Entry point
    │   ├── controllers/
    │   │   └── BookController.java          # GraphQL query & mutation handlers
    │   ├── entities/
    │   │   └── Book.java                    # JPA entity
    │   ├── repositories/
    │   │   └── BookRep.java                 # Spring Data repository
    │   └── services/
    │       ├── BookService.java             # Service interface
    │       └── impl/BookServiceImpl.java    # Service implementation
    └── resources/
        ├── application.properties           # App configuration
        └── graphql/
            └── schema.graphqls             # GraphQL schema definition
```

---

## GraphQL Schema

```graphql
type Query {
  allBooks: [Book]
  getBook(bookId: Int): Book
}

type Mutation {
  createBook(book: BookInput): Book
}

type Book {
  id: ID!
  title: String
  desc: String
  author: String
  price: Float
  pages: Int
}

input BookInput {
  title: String
  desc: String
  author: String
  price: Float
  pages: Int
}
```

---

## Getting Started

### Prerequisites

- Java 16+
- Maven (or use the included `mvnw` wrapper)

### Run the Application

```bash
./mvnw spring-boot:run
```

The server starts on **port 8009**.

---

## Testing the API

### GraphiQL Playground

Spring Boot's built-in GraphiQL interface is available at:

```
http://localhost:8009/graphiql
```

### Sample Queries

**Create a book:**
```graphql
mutation {
  createBook(book: {
    title: "Clean Code"
    desc: "A handbook of agile software craftsmanship"
    author: "Robert C. Martin"
    price: 499.99
    pages: 431
  }) {
    id
    title
    author
  }
}
```

**Get all books:**
```graphql
query {
  allBooks {
    id
    title
    author
    price
  }
}
```

**Get a single book:**
```graphql
query {
  getBook(bookId: 1) {
    id
    title
    desc
    author
    price
    pages
  }
}
```

---

## H2 Console

The in-memory H2 database console is accessible at:

```
http://localhost:8009/h2-console
```

| Field | Value |
|---|---|
| JDBC URL | `jdbc:h2:mem:testdb` |
| Username | `sa` |
| Password | `admin` |

---

## Key Concepts Demonstrated

- Defining a GraphQL schema with types, queries, and mutations
- Using `@QueryMapping` and `@MutationMapping` annotations
- Passing structured input with `@Argument` and GraphQL `input` types
- Persisting data with Spring Data JPA and H2

---

## License

This project is open-source and free to use for learning purposes.
