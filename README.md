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

## Fetch

Make a `fetch` request to `https://rickandmortyapi.com/graphql`:

```javascript
// fetch-api/src/index.js

fetch('https://rickandmortyapi.com/graphql', {})
```

The request is a `POST` request with `Content-Type` of `application/json`:

```javascript
// fetch-api/src/index.js

fetch('https://rickandmortyapi.com/graphql', {
  method: 'POST',

  headers: {
    "Content-Type": "application/json"
  },
})
```

The `characters` query we wrote above asking for their `name` included in the `body` and [stringified](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON/stringify):

```javascript
// fetch-api/src/index.js

fetch('https://rickandmortyapi.com/graphql', {
  method: 'POST',

  headers: {
    "Content-Type": "application/json"
  },

  body: JSON.stringify({
    query: `
      query getCharacters {
        characters {
          results {
            name
          }
        }
      }
    `
  })
})
```

The `results` displayed with `console.log()`:

```javascript
// fetch-api/src/index.js

fetch('https://rickandmortyapi.com/graphql', {
  method: 'POST',

  headers: {
    "Content-Type": "application/json"
  },

  body: JSON.stringify({
    query: `
      query getCharacters {
        characters {
          results {
            name
          }
        }
      }
    `
  })
})
.then(res => res.json())
.then(data => console.log(data.data))
```

![04-fetch-request](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/5yjlc6d38y9yaj5rn2jr.png)

## graphql-request

[graphql-request](https://github.com/prisma-labs/graphql-request) is a minimal GraphQL client that supports Node and browsers.

### Initialize project and install dependencies

```
yarn init -y
yarn add graphql graphql-request react react-dom react-scripts
```

### Add scripts and browsers list

```json
{
  "name": "intro-to-graphql",
  "version": "1.0.0",
  "main": "index.js",
  "repository": "https://github.com/stepzen-samples/intro-to-graphql.git",
  "author": "ajcwebdev <anthony@stepzen.com>",
  "license": "MIT",
  "dependencies": {
    "graphql": "^15.5.0",
    "graphql-request": "^3.4.0",
    "react": "^17.0.2",
    "react-dom": "^17.0.2",
    "react-scripts": "^4.0.3"
  },
  "scripts": {
    "start": "react-scripts start",
    "build": "react-scripts build",
    "test": "react-scripts test",
    "eject": "react-scripts eject"
  },
  "browserslist": {
    "production": [
      ">0.2%",
      "not dead",
      "not op_mini all"
    ],
    "development": [
      "last 1 chrome version",
      "last 1 firefox version",
      "last 1 safari version"
    ]
  }
}
```

### index.html

```html
<!-- graphql-request/public/index.html -->

<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8">
    <meta
      name="viewport"
      content="width=device-width, initial-scale=1.0"
    >
    <meta
      http-equiv="X-UA-Compatible"
      content="ie=edge"
    >

    <title>How to Query the Rick and Morty GraphQL API</title>
  </head>

  <body>
    <noscript>
      You need to enable JavaScript to run this app.
    </noscript>

    <div id="root"></div>
  </body>
</html>
```

### index.js

```jsx
// graphql-request/src/index.js

import React from "react"
import { render } from "react-dom"
import { GraphQLClient, gql } from 'graphql-request'

async function main() {
  const endpoint = 'https://rickandmortyapi.com/graphql'
  const graphQLClient = new GraphQLClient(endpoint)

  const GET_CHARACTERS_QUERY = gql`
    query getCharacters {
      characters {
        results {
          name
        }
      }
    }
  `

  const data = await graphQLClient.request(GET_CHARACTERS_QUERY)
  console.log(JSON.stringify(data, undefined, 2))
}

main()

render(
  <React.StrictMode>
    <h1>graphql-request</h1>
  </React.StrictMode>,
  document.getElementById("root")
)
```

![05-graphql-request](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/b6aaw38auy01erw74or6.png)