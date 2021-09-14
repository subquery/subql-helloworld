# What is SubQuery?

SubQuery powers the next generation of Polkadot dApps by allowing developers to extract, transform and query blockchain data in real time using GraphQL. In addition to this, SubQuery provides production quality hosting infrastructure to run these projects in.

# SubQuery Example - Hello World

This subquery example indexes the timestamp of each finalized block and it is an example of a CallHandler. By processing the `timestamp.set` extrinsic, and extracting the first arguments of it, we can retrieve the timestamp.

# Getting Started

### 1. Clone the entire subql-example repository

```shell
git clone https://github.com/subquery/subql-helloworld.git

```

### 2. Install dependencies

```shell
cd subql-helloworld
yarn
```

### 3. Generate types

```shell
yarn codegen
```

### 4. Build the project

```shell
yarn build
```

### 5. Start Docker

```shell
docker-compose pull & docker-compose up
```

### 6. Run locally

Open http://localhost:3000/ on your browser

### 7. Example query to run

```shell
query{
  starterEntities(last:5, orderBy:BLOCK_HEIGHT_ASC){
    nodes{
      blockHeight
    }
  }
}
```

# Understanding this project

As mentioned above, this project has a function called handleBlock. It uses a [BlockHandler](https://doc.subquery.network/create/mapping.html#block-handler) which is defined in the [manifest file](https://doc.subquery.network/create/manifest.html) (project.yaml) as "kind: substrate/BlockHandler"

The [schema.graphql](https://doc.subquery.network/create/graphql.html) file defines the variables blockHeight which is mandatory and of type Int.

If we examine the function handleBlock in more detail, you can see that this function takes one argument of type SubstrateBlock. It then creates a new instance of StarterEntity passing in the block.block.header.hash argument as a string and assigning this to the variable record.

Next, the blocknumber is converted to a number via toNumber() and assigned to record.blockHeight which is a StarterEntity meaning that the fields within are accessed with a dot.