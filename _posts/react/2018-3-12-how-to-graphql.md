---
layout: post
categories: react
title: How to GraphQL
---

Gatsby's data layer is powered by GraphQL. If you're new to GraphQL, this section may feel a little overwhelming.

# Data in Gatsby

Store data outside components and then bring the data into the component as needed.

Data can also live in file types like Markdown, CSV, etc. as well as databases and APIs of all sorts.

__Gatsby's data layer let us pull data from these (and any other source) directly into our components -- in the shape and form we want.__


# How Gatsby's data layer uses GraphQL to pull data into components

Gatsby uses GraphQL to enable components to declare the data they need.

# Our first GraphQL query

To graphql in gatsby, we have to ensure data has been written in  `gatsby-config.js` :

```javascript
module.exports = {
    siteMetadata: {
        title: `Blah Blah Fake Title`,
    }
}
```

and in the file, that we graphql, like `src/pages/about.js`:

```
export default ({data}) =>(
    <div>About { data.site.siteMetadata.title }</div>
)

export const query = graphql`
    site {
        siteMetadata {
            title
        }
    }
`
```
make sure you write the code above, or error comes


# Where did the graphql tag com from?

The short answer is this:   
during the Gatsby build process, GraphQL queries are pulled out of the original source for parsing.

The longer answer is a little more involved:   
Gatsby borrows a technique from [Relay][relay] that converts our source code into an [abstract syntax tree (AST)][ast] during the build step. All graphql-tagged templates are found in `file-parser.js` and `query-compiler.js`, which effectively removes them from the original source code. This means that the `graphql` tag isn't executed the way that we might expect, which is why there's no error, despite the fact that we're technically using an undefined tag in our source.


[relay]:https://facebook.github.io/relay/
[ast]:https://en.wikipedia.org/wiki/Abstract_syntax_tree

# Introducing GraphQL

We can access GraphQL IDE at http://localhost:8000/___graphql.  

# Source plugins

Add `gatsby-source-filesystem` and explore how it works.

```
yarn add gatsby-source-filesystem
```

`gatsby-config.js`:  

```
plugins: [
    {
        resolve: `gatsby-source-filesystem`,
        options: {
            name: `src`,
            path: `${__dirname}/src/`,
        },
    },
]
```

# Build a page with a GraphQL query

Create a new file at `src/pages/my-files.js` with the `allFile` query we just created:  

```javascript
import React from "react"

export default ({ data }) => {
  console.log(data)
  return <div>Hello world</div>
}

export const query = graphql`
  query MyFilesQuery {
    allFile {
      edges {
        node {
          relativePath
          prettySize
          extension
          birthTime(fromNow: true)
        }
      }
    }
  }
`
```

If you visit the new page at `/my-files/` and open up your browser console you will see the data we've query.  

```jsx
import React from "react"

export default ({ data }) => {
  console.log(data)
  return (
    <div>
      <h1>My Site's Files</h1>
      <table>
        <thead>
          <tr>
            <th>relativePath</th>
            <th>prettySize</th>
            <th>extension</th>
            <th>birthTime</th>
          </tr>
        </thead>
        <tbody>
          {data.allFile.edges.map(({ node }, index) =>
            <tr key={index}>
              <td>
                {node.relativePath}
              </td>
              <td>
                {node.prettySize}
              </td>
              <td>
                {node.extension}
              </td>
              <td>
                {node.birthTime}
              </td>
            </tr>
          )}
        </tbody>
      </table>
    </div>
  )
}

export const query = graphql`
  query MyFilesQuery {
    allFile {
      edges {
        node {
          relativePath
          prettySize
          extension
          birthTime(fromNow: true)
        }
      }
    }
  }
`

```  

# Transformer plugins

Add a Markdown file to our site at `src/pages/sweet-pandas-eating-sweets.md`(This will become our first Markdown blog post) and learn how to transform it to HTML using transformer plugins and GraphQL.  

Once you save the file, look at `/my-files/` again -- the new Markdown is in the table. This is a very powerful feature of Gatsby. Like the earlier `siteMetadata` example, source plugins can live reload data. `gatsby-source-filesystem` is always scanning for new files to be added and when they are, re-runs your queries.  

```
---
title: "Sweet Pandas Eating Sweets"
date: "2018-3-11"
---

Pandas are really sweet.
Here's a video of a panda eating sweets.

```

Add a transformer plugin that can transform Markdown files:
```
yarn add gatsby-transformer-remark
```

Then add it to the `gatsby-config.js` like normal:

```js
plugins: [
    `gatsby-transformer-remark`
]

```

# Create a list of our site's Markdown files in `src/pages/index.js`

Like with the `src/pages/my-files.js` page, replace `src/pages/index.js`
with the following to add a query with some initial HTML and styling.

```jsx
import React from "react";
import g from "glamorous";

import { rhythm } from "../utils/typography";

export default ({ data }) => {
  console.log(data);
  return (
    <div>
      <g.H1 display={"inline-block"} borderBottom={"1px solid"}>
        Amazing Pandas Eating Things
      </g.H1>
      <h4>{data.allMarkdownRemark.totalCount} Posts</h4>
      {data.allMarkdownRemark.edges.map(({ node }) => (
        <div key={node.id}>
          <g.H3 marginBottom={rhythm(1 / 4)}>
            {node.frontmatter.title}{" "}
            <g.Span color="#BBB">— {node.frontmatter.date}</g.Span>
          </g.H3>
          <p>{node.excerpt}</p>
        </div>
      ))}
    </div>
  );
};

export const query = graphql`
  query IndexQuery {
    allMarkdownRemark {
      totalCount
      edges {
        node {
          id
          frontmatter {
            title
            date(formatString: "DD MMMM, YYYY")
          }
          excerpt
        }
      }
    }
  }
`;
```

# Programmatically creating pages from data

Create new pages has two steps:

+ Generate the "path" or "slug" for the page.
+ Create the page.

Two Gatsby APIs `onCreateMode` and `createPages`. These are two workhorse APIs you'll see used in many sites and plugins.  

We do our best to make Gatsby APIs simple to implement. To implement an API, you export a function with the name of the API from `gatsby-node.js`

So let's do that. In the root of our site, create a file named `gatsby-node.js`.

```javascript
exports.onCeateNode = ({ node }) => {
    console.log( node.internal.type )
}
```

Stop and restart the development server. As you do, you'll see quite a few newly created nodes get logged to the terminal console. Let's use this API to add the slugs for our Markdown pages to `MarkdownRemark` nodes.  

Change our function so it now is only looking at `MarkdownRemark` nodes.

```
exports.onCreateNode = ({ node }) => {
    if (node.internal.type === `MarkdownRemark` ) {
        console.log(node.internal.type)
    }
}
```
> the nodes show us plugin nodes of graphql, MarkdownRemark, we just added it

We want to use each Markdown file name to create the page slug. So `pandas-and-bananas.md` will become `/pandas-and-banans/`. traverse the "node graph" to its parent `File` nodes contain data we need about files on disk.

```js
exports.onCreateNode = ({ node, getNode }) => {
    if ( node.interal.type === `MarkdownRemark` ){
        const fileNode = getNode(node.parent)
        console.log(`\n`, fileNode.relativePath)
    }
}
```

> then, we can see the filenames in build time.
> while, `gatsby-node.js` init the environment during build time

The `gatsby-source-filesystem` plugin ships with a function Creating slugs?
It makes `pandas-and-bananas.md` to `/pandas-and-banans/`

```js
const { createFilePath } = require(`gatsby-source-filesystem`);
exports.onCreateNode = ({ node, getNode }) => {
    if (node.internal.type === `MarkdownRemark`){
        console.log(createFilePath({ node, getNode, basePath: `pages` }))
    }
}
```
> if you change the basePath to 'src', output will be `/pages/pandas-to-bananas`

The func handles finding the parent `File` node along with creating the slug.
Now, add new slugs directly onto the `MarkdownRemark` nodes.
we'll use a function passed to our API implementation called `createNodeField`. This function allows us to create additional fields on nodes created by other plugins.
Only the original creator of a node can directly modify the node -- all other plugins (including our gatsby-node.js), must use this function to create additional fields.

```js
const { createFilePath } = require(`gatsby-source-filesystem`);
exports.onCreateNode = ({ node, getNode, boundActionCreators }) => {
    const { createNodeField } = boundActionCreators
    if (node.internal.type === `MarkdownRemark`) {
        //change markdown file
        const slug = createFilePath({ node, getNode, basePath: `pages` })
        createNodeField({
            node, 
            name: `slug`,
            value: slug
        })
    }
}
```
> We just add new field slug to the MarkdownRemark !

Restart the development server and open or refresh GraphiQL. Then run this query to see our new slugs

```javascript
{
    allMarkdownRemark {
        edges {
            node {
                field {
                    slug
                }
            }
        }
    }
}

```

Now that the slugs are created, we can create the pages.

In the same `gatsby-node.js` file.
Here we tell Gatsby about our pages -- what are their paths, what template component do they use, etc.

```javascript
const { createFilePath } = require(`gatsby-source-filesystem`);

exports.onCreateNode = ({ node, getNode, boundActionCreators }) => {
  const { createNodeField } = boundActionCreators
  if (node.internal.type === `MarkdownRemark`) {
    const slug = createFilePath({ node, getNode, basePath: `pages` })
    createNodeField({
      node,
      name: `slug`,
      value: slug,
    })
  }
};
exports.createPages = ({ graphql, boundActionCreators }) => {
    return new Promise(( resolve, reject ) => {
        graqhql(`
            {
                allMarkdownRemark {
                    edges {
                        node {
                            fields {
                                slug
                            }
                        }
                    }
                }
            }
        `).then( result => {
            console.log(JSON.stringify( result, null, 4))
            resolve()
        })
    })
}
```
> Take a look at the value `slug`, we set the filepath to the query named `slug`
> So, after this long query, we inject a slug to the page! lol~

Now that the slugs are created, we can create the pages.
createNode and createPage just like the state of react
