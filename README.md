# Handling Node.js Request Bodies with Vercel

### Parse Node.js request bodies for use inside Serverless Functions deployed with Vercel.

https://vercel.com/guides/handling-node-request-body

https://github.com/coding-to-music/vercel-node-req-body

To verify that the JSON is being parsed correctly, make a POST request to your new deployment using curl by executing the below code inside your terminal:

```java
curl -X POST "https://vercel-node-req-body-geqd03f1a-coding-to-music.vercel.app/api" \
  -H "Content-Type: application/json" \
  -d '{
  "name": "Reader"
}'
```

Response:

```java
Hello Reader, you just parsed the request body!
```

In this guide, we will show you how to parse a Node.js request body, for use inside a Serverless Function deployed to Vercel, without requiring a framework such as Express.

This guide assumes the request is sent with a

Content-Type
of
application/json
. However, many more content types can be parsed if required.

## Step 1: Creating the Function

To get started, create a project directory with an /api directory inside and cd into it:

```java
mkdir vercel-node-req-body && mkdir vercel-node-req-body/api
```

Creating an /api directory inside of a /vercel-node-req-body project.

```java
cd vercel-node-req-body
```

Moving into the /vercel-node-req-body project directory.

To illustrate the parsing of a request body, create an index.js file inside your /api directory with the following code:

```java
export default async function handler(req, res) {
const { body } = req;
return res.send(`Hello ${body.name}, you just parsed the request body!`);
}
```

An example of how to parse a request body using Node.js with a Helper property.

This function takes a POST request, parses the body, and uses data from the body in the response.

The key part here is line 2. Vercel adds a number of Express like helper properties to make wording with Node.js even easier.

Note: You can read more about helper properties either in the blog post or in the documentation.
With the req.body helper, the incoming request is parsed automatically, removing the need for third-party libraries or further code to handle the ReadableStream format the request normally arrives in.

## Step 2: Deploying the Function

Deploying your function to Vercel can be done with a single command:

```java
vercel
```

Deploying the app with the vercel command.

vercel

```java
Vercel CLI 23.1.2
? Set up and deploy “/mnt/volume_nyc1_01/vercel-node-req-body”? [Y/n] y
? Which scope do you want to deploy to? Tom Connors
? Found project “coding-to-music/vercel-node-req-body”. Link to it? [Y/n] y
🔗  Linked to coding-to-music/vercel-node-req-body (created .vercel and added it to .gitignore)
🔍  Inspect: https://vercel.com/coding-to-music/vercel-node-req-body/9qjWmVrveGk7j69wqw61Gituwhgg [2s]
✅  Preview: https://vercel-node-req-body-coding-to-music.vercel.app [11s]
📝  To deploy to production (vercel-node-req-body.vercel.app), run `vercel --prod`
```

vercel --prod

```java
Vercel CLI 23.1.2
🔍  Inspect: https://vercel.com/coding-to-music/vercel-node-req-body/CgXMCtMgE8wgFcRDgpF3SWv6NndZ [1s]
✅  Production: https://vercel-node-req-body.vercel.app [8s]
```

You have now created and deployed your project, all that's left to do is test that it works.

## Step 3: Sending the Request

To verify that the JSON is being parsed correctly, make a POST request to your new deployment using curl by executing the below code inside your terminal:

```java
curl -X POST "https://vercel-node-req-body-geqd03f1a-coding-to-music.vercel.app/api" \
  -H "Content-Type: application/json" \
  -d '{
  "name": "Reader"
}'
```

Response:

```java
Hello Reader, you just parsed the request body!
```

Making a POST request using curl.

Note: You should change the URL to match the one for your deployment given to you in the Vercel CLI.
You will receive a response similar to the following:

Hello Reader, you just parsed the request body!
An example response from making a POST request.

Congratulations, now you know how to parse request bodies with Vercel in Node.js!

Bonus: Understanding Why this Works
When Node.js receives a request, the body is in the format of a ReadableStream.

To get the data from the stream, you need to listen to its data and end events. To do this requires a few lines of code which you would much rather not have to repeat.

By using helper properties, the request is already parsed for you, allowing you to access the data immediately.
