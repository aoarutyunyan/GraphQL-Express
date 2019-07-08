# GraphQL

## Running

```
npm install
npm run json:server
npm run dev
```
* JSON Server running on localhost:3000
* GraphiQL running on localhost:4000

## Example Queries from GraphiQL

```
{
	google: company(id: "2") {
    ...companyDetails
    users {
      ...userDetails
    }
  }
  apple: company(id: "1") {
    ...companyDetails
    users {
      ...userDetails
    }
  }
}

fragment companyDetails on Company {
  id
  name
  description
}

fragment userDetails on User {
  id
  firstName
  age
}
```
### Mutation Example

```
// Adds user with default ID
mutation {
  addUser(firstName: "Arthur", age: 22) {
    id
    firstName
    age
  }
}

// should return null
mutation {
  deleteUser(id: "Q2-pqPx") {
    id
  }
}
```

### This is a playground application using GraphQL with express

