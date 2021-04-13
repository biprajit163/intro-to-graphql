# An Introduction to GraphQL with the Rick and Morty API

This repo demonstrates how to query the Rick and Morty API through various methods.

## What is GraphQL? 

First, let's back up to what GraphQL actually is. If you're familiar with REST APIs, you're familiar with having to filter data that comes back from the API to get the data that you actually want.

But if you use GraphQL as your query language, you start by querying for the data that you want-- and that's all you get in return! Goodbye, annoying filtering logic!

It's important to understand that GraphQL is organized in terms of types and fields.

To take an example from the docs, if we have:

```graphql
type Character {
  name: String!
  appearsIn: [Episode!]!
}
``` 

You can see that we define a `name` and a `appearsIn` field on the type Character, which is an Object type. The defined fields are the only fields that can appear on a query on the Character type. 
What are the exclamation points there for? They mean that the fields are non-nullable, or that you have to include them in a request. 
The brackets on `Episode` indicate that it is an array of objects.

Now that you've seen what GraphQL looks like, let's look at an example.


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

Note that there are a couple of really helpful tabs to the right of the screen:

<img width="800" alt="Screen Shot 2021-04-13 at 9 18 10 AM" src="https://user-images.githubusercontent.com/54046179/114586910-fefd1580-9c39-11eb-91bc-635b26614d9d.png">

The schema tab shows you the Rick and Morty GraphQL schema, which you can also download:

<img width="955" alt="Screen Shot 2021-04-13 at 9 27 13 AM" src="https://user-images.githubusercontent.com/54046179/114587491-93677800-9c3a-11eb-8d37-d07ccd96079a.png">


And the docs tab helpfully maps out the queries and types for you:

<img width="967" alt="Screen Shot 2021-04-13 at 9 27 36 AM" src="https://user-images.githubusercontent.com/54046179/114587525-9bbfb300-9c3a-11eb-8edd-28c1161790d9.png">


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
