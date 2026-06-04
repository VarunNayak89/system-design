# What is API Design?

API design defines how clients interact with backend services.  
Two popular approaches are:

- **REST** (Representational State Transfer)  
- **GraphQL** (Query Language for APIs)

---

## 🧠 REST Overview

### ✅ Characteristics
- Resource-based: Each endpoint represents a resource.  
- Uses HTTP methods: `GET`, `POST`, `PUT`, `DELETE`.  
- Stateless: Each request is independent.  
- Responses are typically in JSON.

### 🧪 Example
```http
GET /users/1
```

```json
{
  "id": 1,
  "name": "Varun",
  "email": "varunbe09@gmail.com",
  "age": 28
}
```

---

## 🧠 GraphQL Overview

### ✅ Characteristics
- Single endpoint: `/graphql`  
- Clients define the shape of the response.  
- Strongly typed schema.  
- Supports queries, mutations, and subscriptions.

### 🧪 Example
```graphql
query {
  user(id: 1) {
    name
    email
  }
}
```

```json
{
  "data": {
    "user": {
      "name": "Varun",
      "email": "varunbe09@gmail.com"
    }
  }
}
```

---

## 🆚 REST vs GraphQL Endpoint Example

| REST | GraphQL |
|------|----------|
| `/users/1` | `/graphql` |
| `/orders/1` | `/graphql` |
| `/products/5` | `/graphql` |
| Multiple endpoints | Single endpoint |
| Fixed response | Client chooses fields |

### REST

```http
GET /users/1
GET /orders/1
GET /products/5
```

### GraphQL

```graphql
POST /graphql

query {
  user(id: 1) {
    name
  }

  order(id: 1) {
    total
  }

  product(id: 5) {
    title
  }
}
```

## 📊 REST vs GraphQL Comparison

| Feature | REST | GraphQL |
|----------|------|----------|
| Data Fetching | Fixed structure per endpoint | Client specifies exact fields |
| Over/Under-fetching | Common | Avoided |
| Endpoints | Multiple | Single (`/graphql`) |
| Versioning | URI versioning (`/v1/`) | Schema evolution via types |
| Error Handling | HTTP status codes | Custom error objects |
| Caching | Easy with HTTP | More complex |
| Tooling | Postman, Swagger | GraphiQL, Banana Cake Pop |
| Learning Curve | Easier | Requires schema/query knowledge |

---

## 🧠 System Design Relevance

GraphQL is primarily an API implementation choice, not a system design strategy.  
However, it influences design in areas such as:

- Data fetching efficiency  
- Backend orchestration  
- Caching strategies  
- Security and access control  

---

## 🔧 GraphQL Implementation in C# with HotChocolate

### ✅ Steps
1. Create a New Project  
2. Install **HotChocolate**  
3. Define a Data Model  
4. Create a Query Resolver  
5. Configure GraphQL in `Program.cs`  
6. Run and Test  

- Navigate to: [http://localhost:5000/graphql](http://localhost:5000/graphql)  
- Use **Banana Cake Pop** to test queries.  

✅ **Response:** *(Add example response here)*

---

## 🧠 Summary

| Aspect | REST | GraphQL |
|---------|------|----------|
| System Design Impact | Minimal | Moderate (depends on usage) |
| Implementation | HTTP endpoints, controllers | Schema, resolvers, query engine |
| C# Support | ASP.NET Core Web API | HotChocolate, GraphQL.NET |
