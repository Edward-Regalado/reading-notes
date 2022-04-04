# API (GraphQL)

## Directives

- Amplify CLI provides GraphQL directvies to enhance your schema with additional capabilities such as custon indexes, authorization rules, function triggers and much more.

## Amplify-provided directives

### Model

- `@model`: [Defines top level object types in your API that are backed by Amazon DynamoDB](https://docs.amplify.aws/cli/graphql-transformer/model/)
  - object types that are annotated with `@model` are top-level entities in the generated API
  - stored in Amazon DynamoDB and are capable of being protected via `@auth`, related to other objects via `@connection`, and streamed into Amazon OpenSearch via `@searchable`
  - The following SDL define the `@model` directive that allows you to easliy define top level obejcts types in your API.
  
```
  directive @model(
  queries: ModelQueryMap
  mutations: ModelMutationMap
  subscriptions: ModelSubscriptionMap
  timestamps: TimestampConfiguration
) on OBJECT
input ModelMutationMap {
  create: String
  update: String
  delete: String
}
input ModelQueryMap {
  get: String
  list: String
}
input ModelSubscriptionMap {
  onCreate: [String]
  onUpdate: [String]
  onDelete: [String]
  level: ModelSubscriptionLevel
}
enum ModelSubscriptionLevel {
  off
  public
  on
}
input TimestampConfiguration {
  createdAt: String
  updatedAt: String
}

```

### Usage

- define a GraphQL object type and annotate it with the `@model` to store in DynamoDB and auto config CRUDL queries and mutations.

```
type Post @model {
  id: ID! # id: ID! is a required attribute.
  title: String!
  tags: [String!]!
}
```

- override the names of any generated queries, mutations and subscriptions or remove operations entirely.

```
type Post @model(queries: { get: "post" }, mutations: null, subscriptions: null) {
  id: ID!
  title: String!
  tags: [String!]!
}
```

### Key

- `@key`: [Configures custom index structures for @model types](https://docs.amplify.aws/cli/graphql-transformer/key/)
- Amazon dynamoDB is a key-value and document database.
- may use at most two attributes to query data. The first query argument passed ot a query (hash key) must use strict equality and the second attribute (sort key) may use gt, ge, lt, le, eq, beginsWith, and between.

#### Arguments

- fields: a list of keys that should compise the `@key`, used in conjunction with an `@model`type. The first field in the list will always be the HASH key. If two fields are provided, the second argument will be the SORT key.
- name: when provided, specifies the name of the secondary index. When not included, specifies that the `@key` is defining the primary index. You may have at most one primary key per table and may have at most one `@key` that does not specify a name per `@model` type. 
- queryField: when defining a secondary index (by name or argument), this specifies that a new top level query field that queries the secondary index should be generated wiht the given name.

### Auth

- `@auth`: [Defines authorization rules for your @model types and fields](https://docs.amplify.aws/cli/graphql-transformer/auth/)
- is required for applications to interact with your GraphQL API.
- API keys are best used for public APIs (or whichever part of your schema you want to make public) or prototyping - must specify the expiration time before deploying.
- IAM auth uses Signature Version 4 to make request with policies attached to Roles.
- `@auth` object types that are annotated are protected by a set of authorization rules giving you additional controls than the top level authorization on an API.
- when using `@auth` on `@model`, all resolvers that return objects of that type will be protected.
- Definition

```
# When applied to a type, augments the application with
# owner and group-based authorization rules.
directive @auth(rules: [AuthRule!]!) on OBJECT | FIELD_DEFINITION
input AuthRule {
  allow: AuthStrategy!
  provider: AuthProvider
  ownerField: String # defaults to "owner" when using owner auth
  identityClaim: String # defaults to "username" when using owner auth
  groupClaim: String # defaults to "cognito:groups" when using Group auth
  groups: [String]  # Required when using Static Group auth
  groupsField: String # defaults to "groups" when using Dynamic Group auth
  operations: [ModelOperation] # Required for finer control

  # The following arguments are deprecated. It is encouraged to use the 'operations' argument.
  queries: [ModelQuery]
  mutations: [ModelMutation]
}
enum AuthStrategy { owner groups private public }
enum AuthProvider { apiKey iam oidc userPools }
enum ModelOperation { create update delete read }

# The following objects are deprecated. It is encouraged to use ModelOperations.
enum ModelQuery { get list }
enum ModelMutation { create update delete }
```

### Connection

- `@connection`: [Defines 1:1, 1:M, and N:M relationships between @model types](https://docs.amplify.aws/cli/graphql-transformer/connection/)

### Function

- `@function`: [Configures a Lambda function resolvers for a field](https://docs.amplify.aws/cli/graphql-transformer/function/)


### Http

- `@http`: [Configures an HTTP resolver for a field](https://docs.amplify.aws/cli/graphql-transformer/http/)


### Predictions

- `@predictions`: [Queries an orchestration of AI/ML services such as Amazon Rekognition, Amazon Translate, and/or Amazon Polly](https://docs.amplify.aws/cli/graphql-transformer/predictions/)
- `@searchable`: [Makes your data searchable by streaming it to Amazon OpenSearch](https://docs.amplify.aws/cli/graphql-transformer/searchable/)
- `@versioned`: [Defines the versioning and conflict resolution strategy for an @model type]https://docs.amplify.aws/cli/graphql-transformer/versioned/)

## AWS AppSync-provided directives

- The following directives are supported by the AppSync service and can be used within the Amplify GraphQL schemas. 
- These will not be processed by Amplify CLI but passed through to the service as is and will be present in the output schema.
- Amplify's @auth directive will add these directives under the hood to the output schema.

- `@aws_api_key`
- `@aws_iam`
- `@aws_oidc`
- `@aws_cognito_user_pools`
- `@aws_auth`
- `@aws_subscribe`

Learn more about these directives in the [AWS AppSync Developer Guide](https://docs.aws.amazon.com/appsync/latest/devguide/security-authz.html).

## 3rd party directives

- `@algolia`: [Add serverless search to your Amplify API with Algolia](https://github.com/thefinnomenon/graphql-algolia-transformer)
  - 
- `@ttl`: [Enable DynamoDB's time-to-live feature to auto-delete old entries in your AWS Amplify API](https://github.com/flogy/graphql-ttl-transformer)
- `@firehose`: [Add a simple interceptor to all of your Amplify API mutations and queries](https://github.com/LaugnaHealth/graphql-firehose-transformer)
- `@retain`: [Enable the "Retain" deletion policy for your Amplify-generated DynamoDB tables](https://github.com/flogy/graphql-retain-transformer)