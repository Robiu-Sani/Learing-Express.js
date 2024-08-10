# MyApp

Welcome to MyApp! This guide will help you set up your Node.js project with Express.js, deploy it using Vercel, and provide an overview of the demo functions.

## Installation Instructions

Follow these steps to set up your project:

1. **Create a new directory for your project and navigate into it:**

    ```bash
    $ mkdir myapp
    $ cd myapp
    ```

2. **Initialize a new Node.js project:**

    ```bash
    $ npm init
    ```

3. **Install Express.js:**

    ```bash
    $ npm install express
    ```

4. **Install Vercel globally to deploy your project:**

    ```bash
    $ npm install -g vercel
    ```

5. **Install the following packages:**

    ```bash
    $ npm install cookie-parser cors dotenv jsonwebtoken mongodb bcrypt
    ```

    - **cookie-parser**: Middleware for parsing cookies attached to client request objects.
    - **cors**: Configures Cross-Origin Resource Sharing (CORS) to enable access from different domains.
    - **dotenv**: Loads environment variables from a `.env` file into `process.env`, keeping sensitive data secure.
    - **jsonwebtoken**: Creates and verifies JSON Web Tokens (JWT) for secure data transmission and authentication.
    - **mongodb**: Official MongoDB driver for Node.js, enabling connection to and interaction with MongoDB databases.
    - **bcrypt**: Hashes passwords to securely store them in your database.

6. **Create a Vercel configuration file (`vercel.json`):**

    ```json
    {
      "version": 2,
      "builds": [
        {
          "src": "index.js",
          "use": "@vercel/node"
        }
      ],
      "routes": [
        {
          "src": "/(.*)",
          "dest": "index.js",
          "methods": ["GET", "POST", "PUT", "PATCH", "DELETE", "OPTIONS"]
        }
      ]
    }
    ```

    - **vercel.json**: This configuration file specifies how Vercel should build and deploy your project. It uses the `@vercel/node` builder for Node.js applications and routes all HTTP methods to your `index.js` file.

    > **Note:** Replace `"index.js"` with the actual entry point file of your project if it has a different name.

## Deployment

To deploy your project, run:

```bash
$ vercel
$ vercel --prod

```
//default route
app.get("/", (req, res) => {
  res.send("single building website api");
});

//listing port
app.listen(port, () => {
  console.log(`server port is ${port}`);
});
```

### Get function
``` Get function
    app.get("/payments", async (req, res) => {
      const result = await payment_collection.find().toArray();
      res.send(result);
    });
```
### pasition Get
``` pasition get
    app.get("/appartmantsPasition", async (req, res) => {
      const page = parseInt(req.query.page);
      const size = parseInt(req.query.size);
      const result = await appartmants_collection
        .find()
        .skip(page * size)
        .limit(size)
        .toArray();
      res.send(result);
    });
```
### Post function
``` Post function
    app.post("/payments", async (req, res) => {
      const payments = req.body;
      const result = await payment_collection.insertOne(payments);
      res.send(result);
    });
```
### Delete function
``` delete function
    app.delete("/contact_message/:id", async (req, res) => {
      const id = req.params.id;
      const query = { _id: new ObjectId(id) };
      const result = await contact_collection.deleteOne(query);
      res.send(result);
    });
```
### Patch function 
``` patch function
    app.patch("/agreements/:id", async (req, res) => {
      const id = req.params.id;
      const query = { _id: new ObjectId(id) };
      const Status = req.body;
      const updateData = {
        $set: {
          Status: Status.Status,
        },
      };
      const result = await agreements_collection.updateOne(query, updateData);
      res.send(result);
    });
```
### Put function
``` put function
app.put("/coupons/:id", async (req, res) => {
      const id = req.params.id;
      const query = { _id: new ObjectId(id) };
      const coupon = req.body;

      const updatedservices = {
        $set: {
          offerDigit: coupon.offerDigit,
          offerType: coupon.offerType,
          code: coupon.code,
          description: coupon.description,
        },
      };

      const result = await coupons_collection.updateOne(query, updatedservices);
      res.send(result);
    });

```










