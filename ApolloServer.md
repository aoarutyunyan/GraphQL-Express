# GraphQL Express vs. Apollo Server

## Types

### User/Company Type

#### GraphQL Express
* GraphQL Express combines types with resolvers, i.e. they are defined together.

```
const UserType = new GraphQLObjectType({
    name: 'User',
    fields: () => ({
        id: { type: GraphQLString },
        firstName: { type: GraphQLString },
        age: { type: GraphQLInt },
        company: { 
            type: CompanyType,
            resolve(parentValue, args) {
               return axios.get(`http://localhost:3000/companies/${parentValue.companyId}`)
                 .then(res => res.data);
            }
        }
    })
});

const CompanyType = new GraphQLObjectType({
    name: 'Company',
    fields: () => ({
        id: { type: GraphQLString },
        name: { type: GraphQLString },
        description: { type: GraphQLString },
        users: {
            type: new GraphQLList(UserType),
            resolve(parentValue, args) {
                return axios.get(`http://localhost:3000/companies/${parentValue.id}/users`)
                  .then(res => res.data);
            }
        }
    })
});
```


#### Apollo Server
* Apollo Server requires two separate files: a schema file containing the types, as well as, a file containing the resolvers:
##### Useful links for structuring files:
* [Modularizing your GraphQL Schema Code](https://blog.apollographql.com/modularizing-your-graphql-schema-code-d7f71d5ed5f2)
* [GraphQL Module for Next Framework](https://github.com/nestjs/graphql)
* [Apollo GraphQL Docs](https://www.apollographql.com/docs/)

```
type User {
    id: !String,
    firstName: String,
    age: Integer,
    companyId: Integer
}

type Company {
    id: !String,
    name: String,
    description: String,
    employees: [User]
}
```
