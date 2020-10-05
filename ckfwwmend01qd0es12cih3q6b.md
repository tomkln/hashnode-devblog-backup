## How to get started with NodeJS & Express

Hi guys, this is a short tutorial for getting an ExpressJS web server up and running. Please note that this tutorial is made with simplicity in mind. For in-depth information, visit the respective [NodeJS](https://nodejs.org/api/) and [express](https://expressjs.com/) documentation.

This tutorial is based on newer Ubuntu versions. Instructions might differ depending on your operating system. Don't hesitate to ask in the comments.

<div data-theme-toc="true"> </div>

# Step 1 - Install NodeJS
If you don't have NodeJS installed already, you can do so by simply executing the following command as a root user (or with the `sudo ...` prefix):

```sh
apt install nodejs -y
```

# Step 2 - Setup your project
Next, we need to set up a basic NodeJS project. You can do so by using Node's Packet Manager (NPM):

```sh
npm init
```

You can modify the values in this setup to your likes.

# Step 3 - Install your dependencies
In this case, we just need express. There are different ways to install modules, we recommend using the `--save` flag to store the module inside your project.

```sh
npm install --save express
```

# Step 4 - Code & run your web server
Let's start by creating an index.js and importing the `express` module:

```nodejs
const express = require('express');
```

Then, create an app - that'll be your webserver instance:

```nodejs
const app = express();
```

Now, you can do all kinds of stuff with the `app` variable. You can create routes, modify settings, and more. Besides the obligatory hello world route, those configurations are out of scope of this tutorial. Feel free to leave feedback on what we should cover next.

Here's the hello world code:

```nodejs
app.get('/', (req, res) => {
  res.send("Hello World!");
});
```

So what does it do? First, we're specifying [a HTTP method](https://developer.mozilla.org/de/docs/Web/HTTP/Methods). GET is the default one used to open web pages, hence `app.get(...)`. The first argument is the path. We're specifying `/` as it is the home page opened. This could be anything like `/my-page` or more complicated paths. The second argument is a callback function. This function is executed once somebody requests this web page/route. There are two arguments for this callback function, `req` with request information from the visitor and `res` with the response information that you send back. In this case, we're sending back (`res.send(...);`) the text "Hello World!". This could contain all sorts of stuff - from images to HTML.

Now we just need to run the server on HTTP's default port:

```nodejs
app.listen(80, () => {
  console.log('Running the web server!');
});
```
... and tada! If you now run this script using `node index.js`, you should see the working web page on http://localhost/!

# Bonus - Setting up SSL/TLS (:https: https:)
In order to enable HTTPS, we have to add some lines of code to the end. In particular, we need to create an HTTPS instance of the `app`, configure our SSL/TLS certificates used for encrypting the traffic, and run the second instance on port 443 (https default).

In the case of the following code, you'd need to upload a certificate (server.crt) and a key (server.key) to your project's directory. You can get SSL certificates today for free, by either using a proxy service such as cloudflare.com's or gentlent.com's, or by getting one from a certification authority such as zerossl.com (easiest) or letsencrypt.org.

Start by importing the required Node modules at the top:

```nodejs
const https = require('https');
const fs = require('fs');
```

After that, add the following code at the bottom, to run an HTTPS server:

```nodejs
https.createServer({
    cert: fs.readFileSync(__dirname + '/server.crt'),
    key: fs.readFileSync(__dirname + '/server.key'),
}, app).listen(port);
```

Now, HTTPS should be up and running. Now start fiddling around with your code and start learning to build something awesome!

Let us know if that worked for you and what we should cover next.