# Serverless Architecture

- "Focus on your applicatoin, not the infrastructure"
- Serverless is a cloud computing execution model where the cloud provider dynamically manages the allocation and provisioning of servers.
- A serverless app runs in stateless compute containers that are event-triggered, ephemeral(may last for one invocation), and full managed by the cloud provider.
- pricing is based on the number of executions rather than pre-purchased cmopute capacity.
- Serverless appications are event-driven cloud-based systems where application development rely solely on a combination of third-party services, client-side ligic and cloud-hosted remote procedure cals (Functions as a Service)

## Cloud providers

- AWS Lambda
- Google Could Functions
- Azure Functions
- IBM OpenWhisk
- Alibaba Function Compute
- Iron Functions
- Auth0 Webtask
- Oracle Fn Project
- Kubeless

## Traditional vs Serverless Architecture

- application used to run on servers which you had to patch, update and continuously look after due to all the unimaginable errors that broke your production.
- with serverless, you no longer need ot worry about the underlying servers as they are not managed by you anymore and with management out of the picture the responsibility falls on the Cloud vendors.

## Pricing

- recuded coast since its execution based: charged for the number of executions.
- alloted a certain number of seconds of use that varies with the amount of memory you require.

## Networking

- downside is taht serverless functions are accessed only as private APIs and you must set up an API Gateway.
- you cannot directly access them through the usual IP.

## 3rd Party Dependencies

- most project have external dependencies (libraries that are not built into the language or framework you use)
- without system-level access, you must package these depends into the application itself.

## Environments

- setting up different env for Serverless is as eas as setting up a single evn.
- no longer need to set up dev, staging and production machines.

## Timeout

- hard 300-second timeout limit: long-running functiosn are not good for Serverless, but having a hard timeout makes it impossible to perform certain tasks.
- this makes Serverless unusable for applications that have variable execution times, and for certain services which require information from an external source.

## Scale

- automatic and seamless for Serverless, but there's a lack of control or entire absence of control.
- auto scaling is great, it's difficult nto to be able to address and mitigate errors related to new Serverless instance.

## Stateless

- with Serverless, everything is stateless, you can't save a file to disk on one execution of your function and expect it to be there at the next.


# AWS Amplify

- AWS Amplify is a set of purpose-built tools and features that lets frontend web and mobile developer quickly and easily build full-stack applications on AWS, whith the flexibility to leverage the breadth of AWS services as your use cases evolve.
- configure a web or mobile app backend, connnect your app in mintues, visually build a web front UI, and easily manage app content outside of AWS console.

## Tools

- Amplify Studio: visually build a full-stack app, both front-end UI and a backend.
- Amplify Libraries: connect an app to new or existing AWS services.
- Amplify CLI: configure an app backend with a guide CLI workflow.
- Amplify Hosting: host secure, reliable, fast web apps or webiste via the AWS content delivery network.

## API (Graphql)

- the GraphQL Transform provides a simpel to use abstraction that help you quickly creaaet backendc for your urweb and mobile application on AWS.
- define your application's data model using the GraphQL Schema Definition language (SDL) and the library handles converting your SDL definition into a set of fully descriptive AWS CloudFormation templates that implement your data model.

## Creat a GraphQL API

- navigate into the root of a JavaScript, IOS or Android project and run:
- `amplify init`
- follow the wizard to create a new app. After finishing run:
- `amplify add api`
- Select the following options:
  - Select GraphQL
  - When asked if you have a schema, say No
  - Select one of the default samples; you can change this later
  - Choose to edit the schema and it will open the new `schema.graphql` in your editor

```
type Blog @model {
  id: ID!
  name: String!
  posts: [Post] @connection(name: "BlogPosts")
}
type Post @model {
  id: ID!
  title: String!
  blog: Blog @connection(name: "BlogPosts")
  comments: [Comment] @connection(name: "PostComments")
}
type Comment @model {
  id: ID!
  content: String
  post: Post @connection(name: "PostComments")
}
```

- save the file and hit enter in your terminal window- if no error messages are thrown the transformation was successful and you can deploy your new API. Run: `amplify push`

## Test the API

- Once the API is finsihed deploying, go to the AWS AppSync console or run `amplify mock api` to try some o fthese queires in your new API's query page.

```
# Create a blog. Remember the returned id.
# Provide the returned id as the "blogId" variable.
mutation CreateBlog {
  createBlog(input: {
    name: "My New Blog!"
  }) {
    id
    name
  }
}

# Create a post and associate it with the blog via the "postBlogId" input field.
# Provide the returned id as the "postId" variable.
mutation CreatePost($blogId:ID!) {
  createPost(input:{title:"My Post!", postBlogId: $blogId}) {
    id
    title
    blog {
      id
      name
    }
  }
}

# Provide the returned id from the CreateBlog mutation as the "blogId" variable
# in the "variables" pane (bottom left pane) of the query editor:
{
  "blogId": "returned-id-goes-here"
}

# Create a comment and associate it with the post via the "commentPostId" input field.
mutation CreateComment($postId:ID!) {
  createComment(input:{content:"A comment!", commentPostId:$postId}) {
    id
    content
    post {
      id
      title
      blog {
        id
        name
      }
    }
  }
}

# Provide the returned id from the CreatePost mutation as the "postId" variable
# in the "variables" pane (bottom left pane) of the query editor:
{
  "postId": "returned-id-goes-here"
}

# Get a blog, its posts, and its posts' comments.
query GetBlog($blogId:ID!) {
  getBlog(id:$blogId) {
    id
    name
    posts(filter: {
      title: {
        eq: "My Post!"
      }
    }) {
      items {
        id
        title
        comments {
          items {
            id
            content
          }
        }
      }
    }
  }
}

# List all blogs, their posts, and their posts' comments.
query ListBlogs {
  listBlogs { # Try adding: listBlog(filter: { name: { eq: "My New Blog!" } })
    items {
      id
      name
      posts { # or try adding: posts(filter: { title: { eq: "My Post!" } })
        items {
          id
          title
          comments { # and so on ...
            items {
              id
              content
            }
          }
        }
      }
    }
  }
}
```

## Update Schema

- If you want to update your API, open your projeft's `backend/api/~apiname~/schema.graphql` (not the one in the /build folder) and edit in code editor.
- compile by running: `amplify api gql-compile`
- push updated changes with: `amplify push`

- The following schema updates require replacement of the uderlying DynamoDB table:
  1. Removing or renaming a model
  2. Modifying the primary key of a model
  3. Modifying a Local Secondary Index of a model.
- When trying to push a schema change with one or morre of these updates, you will see an error message explaining that you will lose ALL DATA in any table that requires replacment. To confirm, run: `amplify push --allow-destructive-graphql-schema-updates`
  - this command should NEVER be use din a production environment as you will not be able to recover data from replaced tables.

## Rebuild GraphQL API

- rebuild should NEVER be used in a production environment.
- when in development, test data gets in a bad state or you want to make many changes to your schema all at once, run: `amplify rebuild api`
- this will recreate ALL of the tables backing models in your schema. ALL DATA in ALL TABLES will be deleted.

## API Category Project Structure

- transform libraries taek a schema defined in the GraphQL Schema Definition Language (SDL) and converts it into a set of AWS CloudFormation templates and toehr assets that are deployed as part of `amplify push`
- when creating APIs, you will make changes to the other files and directories in the `amplify/backend/api/YOUR-API-NAME/directory` but you should not manually change anything in the build directory.
- the build direcotry will be overwritten the next time you run `amplify push` or `amplify api gql-compile`

### API directory

```
-build/
- resolvers/
| # Store any resolver templates written in vtl here. E.G.
|-- Query.ping.req.vtl
|-- Query.ping.res.vtl
|
- stacks/
| # Create custom resources with CloudFormation stacks that will be deployed as part of `amplify push`.
|-- CustomResources.json
|
- parameters.json
| # Tweak certain behaviors with custom CloudFormation parameters.
|
- schema.graphql
| # Write your GraphQL schema in SDL
- schema/
| # Optionally break up your schema into many files. You must remove schema.graphql to use this.
|-- Query.graphql
|-- Post.graphql
- transform.conf.json
```

### Sources

[Hackernoon](https://hackernoon.com/what-is-serverless-architecture-what-are-its-pros-and-cons-cc4b804022e9)  
[AWS Amplify](https://aws.amazon.com/amplify/)  
[AWS Amplify](https://docs.amplify.aws/cli-legacy/graphql-transformer/overview/#test-the-api)  
