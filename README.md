# An Introduction to GraphQL with the Rick and Morty API

This repo demonstrates how to query the Rick and Morty API through various methods.

So if we wanted to take it to the total basics, you'd want to start with actually making a GraphQL query. For example, if you were to go to the following [link](https://rickandmortyapi.com/graphql) you'll see this:

![01-rick-and-morty-graphiql](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/p71t3vphq4c9vt1r3suo.png)

We want to make a query, so we'll enter the following `query` for `characters`, specifically their `name` (the `results` array is a quirk of this specific GraphQL schema).

```graphql
query {
  characters {
    results {
      name
    }
  }
}
```

This returns an array of names.

![02-character-names](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/sdvapzwb74l4bw38p73w.png)

## Clone this repo

```bash
git clone https://github.com/stepzen-samples/intro-to-graphql.git
cd intro-to-graphql
```

Open `index.html` with a development server. If you don't have one install the [Live Server](https://ritwickdey.github.io/vscode-live-server/) VS Code extension at the [following link](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer). Open your Dev Tools and go to the console.

![03-hello-mintbean](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/nurmlwvhq4wn976xz7vh.png)
