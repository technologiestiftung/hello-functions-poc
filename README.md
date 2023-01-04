# netlify functions proof of concept

Using netlify functions

## Setup

Actually relatively straightforward.

In the file `netlify/functions/hello.ts`. 

you have the following code

```ts
import { Handler, HandlerEvent, HandlerContext } from `netlify/functions`;

const handler: Handler = async (event: HandlerEvent, context: HandlerContext) => {
  return {
    statusCode: 200,
    body: JSON.stringify({ message: "Hello World" }),
  };
};

export { handler };
```

You need the following packages

```bash
npm install --save-dev typescript && npm install @netlify/functions
# set up typescript
npx tsc --init
# maybe use netlify cli for development
npm install --save-dev netlify-cli
```

The following configuration is necessary for typescript. 


```json
{
...
Compiler options:{
...
 esModuleInterop :true,
 isolatedModules :true,
...
}
}
```

## Development

With the netlify cli you can start a local development server
```bash
npx netlify dev
```

## Deployment

Deployed just like a frontend via git push from repo.

The usual things are needed:

- create a repo
- push your code
- connect to netlify site to github repo

The url of the function should then be `<something>.netlify.app/.netlify/functions/hello`. 

## From the docs

> By default, all functions are provided with:
> 
> - us-east-1 AWS Lambda region.
> - 1024 MB memory
> - 10 seconds execution limit for synchronous functions, including scheduled functions.
> 6 MB for request and response payload for synchronous functions.
> 256 KB for the size of the payload of request and response for background functions


If that's too little, then there are [background Functions](https://docs.netlify.com/functions/background-functions/) and in beta [Edge Functions](https://docs.netlify.com/edge-functions/overview/) (which run in Deno instead of Nodejs and are deployed globally)


