# mocha-chai-node-testing
Mocha &amp; Chai Testing Setup with Node.js and ESM Modules

This method resolved the error
```js
import * as chai from "chai";
import chaiHttp from "chai-http";
const request = use(chaiHttp).request.execute;
...
request(app).post ....

```

- NOTE: import chai from "chai" does not seem to work
- github [issues note](https://github.com/chaijs/chai/issues/1561)

  
🔧 Configuration

Ensure package.json has:
```js
"type": "module",
"scripts": {
  "test": "mocha"
}
```

🏗️ Testing Setup

 ```js

 process.env.NODE_ENV = "test";

import chaiHttp from "chai-http";
import * as chai from "chai";

const should = chai.should();
const expect = chai.expect();

const use = chai.use;
const request = use(chaiHttp).request.execute;

import app from "../app.js";
import User from "../models/User.js";

describe(" API Testing ", () => {
  beforeEach(async () => {
   await User.deleteMany({});

 after(async () => {
    await mongoose.connection.close();
    console.log("Disconnected from mongodb after tests");
  });

describe("Register ", () => {
const newUser = {
        username: "newuser",
        password: "password123",
      };

      request(app)
        .post("/api/users/register")
        .send(newUser)
        .end((err, res) => {
          console.log(res.body);
          res.should.have.status(201);
          res.body.should.have
            .property("message")
            .equal("User registered successfully");
          done();
        });
    });
});

```

🧪 Running Tests

Execute tests using Mocha:
npm test
