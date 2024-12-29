# [TABLE OF CONTENTS](#table-of-contents)

- [Setup Notes from Tutorial](#setup-notes-from-tutorial)
- [Architecture Using Controllers and Routes](#architecture-using-controllers-and-routes)
- [Working with Express Router in TypeScript](#working-with-express-router-in-typescript)
- [Handling GET-POST-PUT-DELETE requests with Express Typescript](#handling-get-post-put-delete-requests-with-express-typescript)
- [package.json](#packagejson)
- [(`src`) / `index.ts`](#src--indexts)
- [(`src`) / (`routes`) / `index.ts`](#src--routes--indexts)
- [(`src`) / (`routes`) / `home.routes.ts`](#src--routes--homeroutests)
- [(`src`) / (`routes`) / `tutorial.routes.ts`](#src--routes--tutorialroutests)
- [(`src`) / (`controllers`) / `home.controller.ts`](#src--controllers--homecontrollerts)
- [(`src`) / (`controllers`) / `tutorial.controller.ts`](#src--controllers--tutorialcontrollerts)

# Setup Notes from Tutorial

These are the setup notes I took from the tutorial located here: https://www.bezkoder.com/express-typescript-example/.

The original github repository is located here: https://github.com/bezkoder/express-typescript-examp which has more links to articles and examples.

The notes below are organized by File Name and contain AI generated explanations that go deeper than the tutorial's notes.

**key takeaways or "gotchas"**

- In TypeScript when you create a class the class itself can be used as a `type`.
- In backend development **Controllers** handle the business logic for each endpoint. They process incoming requests, interact with the database or other services, and send responses back to the client whereas **Routes** define endpoints and map them to controller functions.

## Architecture Using Controllers and Routes

The architecture using "controllers" is a common pattern in backend development, especially in frameworks like Express. The main purpose of this architecture is to separate concerns, making the code more modular, maintainable, and scalable. Here's how it works:

1. Routes: Define the endpoints and map them to controller functions.
2. Controllers: Handle the business logic for each endpoint. They process incoming requests, interact with the database or other services, and send responses back to the client.

This separation allows you to manage your codebase more effectively, especially as it grows. It also makes it easier to test individual components.

## Working with Express Router in TypeScript

### High-Level Overview of the Code Excerpts

The code excerpts in this repository demonstrate a structured approach to setting up an Express server using TypeScript. This architecture leverages the concepts of Express Router, controllers, and a server setup class to create a modular, maintainable, and scalable application. By separating concerns into distinct components, the codebase becomes easier to manage and extend. Below is an expanded explanation of how these components work together.

### Express Router

The Express Router is a crucial component in organizing the routes of an application. In the provided code, the `home.routes.ts` file defines a router for the home endpoint. The `Router class` from Express is used to create a new router instance, which is then configured with specific routes. For example, the `intializeRoutes` method sets up a route for the root path (`"/"`) and maps it to the `welcome` controller function. This modular approach allows you to define routes in separate files, making the codebase more organized and easier to navigate. By exporting the router instance, it can be easily integrated into the main application.

### Controllers

Controllers handle the business logic for each endpoint, processing incoming requests and sending appropriate responses. In the `home.controller.ts` file, the `welcome` function is defined to handle requests to the root path. This function takes in a request (`req`) and a response (`res`) object, and sends a JSON response with a welcome message. By separating the logic into controllers, the code becomes more modular and easier to test. Each controller function can be independently tested and maintained, ensuring that the business logic is encapsulated and reusable.

### Server Setup

The server setup is managed by the `Server class` defined in the `src/index.ts` file. This class is responsible for configuring the Express application and setting up middleware. The constructor of the `Server` class takes an `app` parameter of type `Application` and calls the `config` method to configure the application. The `config` method sets up CORS options, JSON parsing, and URL-encoded data parsing. Additionally, the `Routes class` is instantiated to set up the main routes for the application. This centralized setup ensures that all configurations and routes are defined in one place, making the application easier to manage and extend.

### Conclusion

By using Express Router, controllers, and a server setup class, the provided code excerpts demonstrate a well-structured approach to building an Express server with TypeScript. This architecture separates concerns into distinct components, making the codebase more modular, maintainable, and scalable. The Express Router organizes routes, controllers handle business logic, and the server setup class configures the application and integrates routes. Together, these components create a robust foundation for building and managing a web application.

## Handling GET-POST-PUT-DELETE requests with Express Typescript

This project demonstrates how to handle HTTP requests using Express and TypeScript. The architecture separates concerns into routes and controllers, making the code modular and maintainable. The `Routes class` sets up the main application routes, while the `TutorialRoutes` class defines specific routes for tutorial-related operations. The `TutorialController` class handles the business logic for each route, processing incoming requests and sending appropriate responses.

### src/routes/index.ts
The `Routes class` in `src/routes/index.ts` is responsible for setting up the main application routes. It imports the `homeRoutes` and `tutorialRoutes` modules and registers them with the Express application. The constructor takes an `app` parameter of type `Application` and uses the `app.use` method to define the base paths for the routes. The `homeRoutes` are registered under the `/api` path, while the `tutorialRoutes` are registered under the `/api/tutorials` path. This setup ensures that the application can handle requests to these endpoints and delegate them to the appropriate route handlers.

### src/routes/tutorial.routes.ts
The `TutorialRoutes` class in `src/routes/tutorial.routes.ts` defines the specific routes for tutorial-related operations. It imports the `Router class` from Express and the `TutorialController` class. The class initializes a new router instance and a new controller instance. The `intializeRoutes` method sets up the routes for creating, retrieving, updating, and deleting tutorials. Each route is mapped to a corresponding method in the `TutorialController` class. For example, the `POST /` route is mapped to the `create` method, the `GET /` route is mapped to the `findAll` method, and so on. This modular approach allows for easy management and extension of the routes.

### src/controllers/tutorial.controller.ts
The `TutorialController` class in `src/controllers/tutorial.controller.ts` handles the business logic for each tutorial-related operation. It defines asynchronous methods for creating, retrieving, updating, and deleting tutorials. Each method takes a request (`req`) and a response (`res`) object as parameters. The methods use try-catch blocks to handle potential errors and send appropriate responses. For example, the `create` method sends a `201 Created` status with a JSON response containing the request body, while the `findAll` method sends a `200 OK` status with a JSON response containing a success message. If an error occurs, the methods send a `500 Internal Server Error` status with an error message.

### Conclusion
By separating concerns into routes and controllers, this project demonstrates a structured approach to handling HTTP requests with Express and TypeScript. The `Routes class` sets up the main application routes, the `TutorialRoutes` class defines specific routes for tutorial-related operations, and the `TutorialController` class handles the business logic for each route. This architecture makes the code modular, maintainable, and scalable, allowing for easy management and extension of the application.



## `package.json`

To work with TypeScript, we need TypeScript compiler (`tsc`), which converts TypeScript code into JavaScript (inside `./build` folder). TypeScript files have the `.ts` extension. Once compiled to JavaScript, we can run the resulting JavaScript files using a JavaScript runtime environment or include them in web applications.

So we modify "scripts" property of `package.json` file by adding `build`, `dev` and `start` like this:

```json
{
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "build": "tsc",
    "dev": "node ./build/server.js",
    "start": "tsc && npm run dev"
  }
}
```

[Back to TOC](#table-of-contents)

## (`src`) / `index.ts`

This creates the Typescript server.

### Code

```ts
import express, { Application } from "express";
import cors, { CorsOptions } from "cors";

export default class Server {
  constructor(app: Application) {
    this.config(app);
  }

  private config(app: Application): void {
    const corsOptions: CorsOptions = {
      origin: "http://localhost:8081",
    };

    app.use(cors(corsOptions));
    app.use(express.json());
    app.use(express.urlencoded({ extended: true }));
  }
}
```

[Back to TOC](#table-of-contents)

### Code Explanation

#### 1. Imports

```ts
import express, { Application } from "express";
import cors, { CorsOptions } from "cors";
import Routes from "./routes";
```

##### `express`

Imports the Express framework.

##### `{ Application }`

Imports the Application type from Express. This type is provided by the `express` library. It represents an Express application instance. Using this type helps ensure that the app parameter in your code is correctly typed as an Express application.

##### `cors`

Imports the CORS middleware.

##### `{ CorsOptions }`

Imports the CorsOptions type from CORS. This type is provided by the `cors` library. It represents the options that can be passed to the CORS middleware. Using this type helps ensure that the `corsOptions` object in your code is correctly typed according to the options supported by the `cors` middleware.

##### `Routes`

Imports the Routes class from the ./routes module.

[Back to TOC](#table-of-contents)

#### 2. Class Definition

```ts
export default class Server {
```

Defines and exports a `Server` class as the default export.

#### 3. Constructor

```ts
constructor(app: Application) {
  this.config(app);
  new Routes(app);
}
```

[Back to TOC](#table-of-contents)

##### `constructor(app: Application) {`

The constructor takes an `app` parameter of type `Application`. This is a special method called a constructor. It is automatically called when a new instance of the `Server` class is created. The `app` parameter is of type `Application`, which is imported from Express.

- NB: `this`: Refers to the current instance of the class. It allows you to access properties and methods of the class.

##### `this.config(app)`

Calls the `config` method to configure the Express application. Calls the `config` method on the current instance of the `Server` class, passing the `app` parameter. This method configures the Express application.

##### `new Routes(app);`

Instantiates the `Routes` class, passing the `app` to set up routes. Creates a new instance of the `Routes` class, passing the `app` parameter. This sets up the routes for the Express application [see explanation of the `Routes` Class below](#src--routes--indexts).

The `constructor` method in the `Server` class initializes the server by calling the `config` method and setting up routes using the `Routes` class. The `this` keyword refers to the current instance of the class, allowing access to its properties and methods. The `Routes` class sets up the routes for the Express application by registering middleware for specific endpoints.

[Back to TOC](#table-of-contents)

#### 4. Config Method

```ts
private config(app: Application): void {
  const corsOptions: CorsOptions = {
    origin: "http://localhost:8081"
  };

  app.use(cors(corsOptions));
  app.use(express.json());
  app.use(express.urlencoded({ extended: true }));
}
```

##### `private`

The method is private and can only be called within the class. The `private` keyword is an access modifier in TypeScript. It restricts access to the method or property it is applied to, making it accessible only within the class it is defined in. For example, the `config` method is marked as `private`, meaning it can only be called from within the `Server` class. It cannot be accessed from outside the class or by instances of the class.

[Back to TOC](#table-of-contents)

##### `config(app: Application): void`

Defines a method that takes an `app` parameter of type `Application` and returns `void`. The `void` return type indicates that the method does not return any value. For example, the `config` method is used to configure the Express application. It performs its tasks (setting up middleware) without returning any value, hence the `void` return type.

[Back to TOC](#table-of-contents)

##### `corsOptions`

Defines CORS options to allow requests from `http://localhost:8081`. The `CorsOptions` type is used to define the configuration options for the CORS (Cross-Origin Resource Sharing) middleware. For example, `corsOptions` is an object of type `CorsOptions` that specifies the configuration for the CORS middleware. The `origin` property is set to `"http://localhost:8081"`, allowing requests from this origin.

Other examples of properties that can be set within the `corsOptions` variable are:

- `methods`: Specifies the HTTP methods that are allowed.
- `allowedHeaders`: Specifies the headers that are allowed in the request.
- `exposedHeaders`: Specifies the headers that are exposed to the browser.
- `credentials`: Indicates whether or not the response to the request can be exposed when the credentials flag is true.
- `maxAge`: Indicates how long (in seconds) the results of a preflight request can be cached.
- `preflightContinue`: Pass the CORS preflight response to the next handler.
- `optionsSuccessStatus`: Provides a status code to use for successful OPTIONS requests.

[Back to TOC](#table-of-contents)

##### `app.use(cors(corsOptions))`

Applies the CORS middleware with the specified options.

##### `app.use(express.json())`

Parses incoming JSON requests.

##### `app.use(express.urlencoded({ extended: true }))`

Parses URL-encoded data.

[Back to TOC](#table-of-contents)

### TypeScript Syntax Explanation

#### 1. Imports

```ts
import express, { Application } from "express";
import cors, { CorsOptions } from "cors";
import Routes from "./routes";
```

##### `import ... from "module"`

Imports modules or specific exports from a module.

##### `{ Application }`

Destructures and imports specific types or functions.

[Back to TOC](#table-of-contents)

#### 2. Class Definition

```ts
export default class Server {
```

#### 3. Constructor

```ts
constructor(app: Application) {
```

##### `constructor`

A special method for creating and initializing an object created with a class.

##### `app: Application`

Type annotation indicating that `app` is of type `Application`.

[Back to TOC](#table-of-contents)

#### 4. Method Definition

```ts
private config(app: Application): void {
```

##### `private`

Access modifier indicating that the method is private.

##### `config(app: Application): void`

Method signature with type annotations.

##### `app: Application`

Parameter `app` is of type `Application`.

##### `: void`

Return type annotation indicating the method returns nothing.

[Back to TOC](#table-of-contents)

#### 5. Type Annotations

```ts
const corsOptions: CorsOptions = {
  origin: "http://localhost:8081",
};
```

##### `const corsOptions: CorsOptions`

Declares a constant `corsOptions` with type `CorsOptions`.

[Back to TOC](#table-of-contents)

## `server.ts`

### Code

```ts
import express, { Application } from "express";
import Server from "./src/index";

const app: Application = express();
const server: Server = new Server(app);
const PORT: number = process.env.PORT ? parseInt(process.env.PORT, 10) : 8080;

app
  .listen(PORT, "localhost", function () {
    console.log(`Server is running on port ${PORT}.`);
  })
  .on("error", (err: any) => {
    if (err.code === "EADDRINUSE") {
      console.log("Error: address already in use");
    } else {
      console.log(err);
    }
  });
```

### Code Explanation

1. Imports

```ts
import express, { Application } from "express";
import Server from "./src/index";
```

- `express`: Imports the Express framework.
- `{ Application }`: Imports the `Application` type from Express.
- `Server`: Imports the `Server` class from the `./src/index` module.

2. Creating Express Application

```ts
const app: Application = express();
```

- `const app: Application = express();`: Creates an instance of an Express application and assigns it to the `app` constant. The `app` is typed as `Application`.

3. Initializing Server Object

```ts
const server: Server = new Server(app);
```

- `const server: Server = new Server(app);`: Creates a new instance of the `Server` class, passing the `app` instance to its constructor. The `server` is typed as `Server`.

4. Setting Port

```ts
const PORT: number = process.env.PORT ? parseInt(process.env.PORT, 10) : 8080;
```

- `const PORT: number = process.env.PORT ? parseInt(process.env.PORT, 10) : 8080;`: Sets the `PORT` constant to the value of the `PORT` environment variable (if it exists) or defaults to `8080`. The PORT is typed as `number`.

5. Listening for Incoming Requests

```ts
app
  .listen(PORT, "localhost", function () {
    console.log(`Server is running on port ${PORT}.`);
  })
  .on("error", (err: any) => {
    if (err.code === "EADDRINUSE") {
      console.log("Error: address already in use");
    } else {
      console.log(err);
    }
  });
```

- `app.listen(PORT, "localhost", function () { ... })`: Starts the Express application listening on the specified `PORT` and `localhost`. The callback function logs a message when the server starts.
- `.on("error", (err: any) => { ... })`: Attaches an error handler to log errors. If the error code is `EADDRINUSE`, it logs a specific message; otherwise, it logs the error.

### TypeScript Syntax Explanation

1. Imports

```ts
import express, { Application } from "express";
import Server from "./src/index";
```

- `import ... from "module"`: Imports modules or specific exports from a module.
- `{ Application }`: Destructures and imports specific types or functions.

2. Variable Declaration and Type Annotation

```ts
const app: Application = express();
const server: Server = new Server(app);
const PORT: number = process.env.PORT ? parseInt(process.env.PORT, 10) : 8080;
```

- `const`: Declares a constant variable.
- `app: Application`: Type annotation indicating that `app` is of type `Application`.
- `server: Server`: Type annotation indicating that `server` is of type `Server`.
- `PORT: number`: Type annotation indicating that `PORT` is of type `number`.

3. Conditional Assignment

```ts
const PORT: number = process.env.PORT ? parseInt(process.env.PORT, 10) : 8080;
```

- `process.env.PORT ? parseInt(process.env.PORT, 10) : 8080`: Uses a ternary operator to assign the value of `PORT`. If `process.env.PORT` is `defined`, it parses it as an integer; otherwise, it defaults to `8080`.

4. Method Chaining

```ts
app
  .listen(PORT, "localhost", function () {
    console.log(`Server is running on port ${PORT}.`);
  })
  .on("error", (err: any) => {
    if (err.code === "EADDRINUSE") {
      console.log("Error: address already in use");
    } else {
      console.log(err);
    }
  });
```

- `app.listen(...).on(...)`: Chains method calls on the `app` object.
- `function () { ... }`: Defines an anonymous function.
- `(err: any) => { ... }`: Defines an arrow function with a parameter `err` of type `any`.

## (`src`) / (`routes`) / `index.ts`

### Code

```ts
import { Application } from "express";
import homeRoutes from "./home.routes";
import tutorialRoutes from "./tutorial.routes";

export default class Routes {
  constructor(app: Application) {
    app.use("/api", homeRoutes);
    app.use("/api/tutorials", tutorialRoutes);
  }
}
```

[Back to TOC](#table-of-contents)

### Code Explanation

#### 1. Imports

```ts
import { Application } from "express";
import homeRoutes from "./home.routes";
```

- Imports the `Application` type from Express.
- Imports the `homeRoutes` router.

#### 2. Class Definition

```ts
export default class Routes {
```

- `export default`: Exports the `Routes` class as the default export of the module.
- `class Routes`: Defines a class named `Routes`.

[Back to TOC](#table-of-contents)

#### 3. Constructor

```ts
constructor(app: Application) {
  app.use("/api", homeRoutes);
  app.use("/api/tutorials", tutorialRoutes);
}
```

- `constructor(app: Application)`: This is the constructor method for the `Routes` class. It takes an `app` parameter of type `Application`.
- Sets up the `homeRoutes` and `tutorialRoutes` routers to handle requests to the `/api` and `/api/tutorials` endpoints.
- `app.use("/api", homeRoutes)`: Registers the `homeRoutes` middleware to handle requests to the `/api` endpoint.
- `app.use("/api/tutorials", tutorialRoutes)`: Registers the `tutorialRoutes` middleware to handle requests to the `/api/tutorials` endpoint.

[Back to TOC](#table-of-contents)

### TypeScript Syntax Explanation

## (`src`) / (`routes`) / `home.routes.ts`

### Code

```ts
import { Router } from "express";
import { welcome } from "../controllers/home.controller";

class HomeRoutes {
  router = Router();

  constructor() {
    this.intializeRoutes();
  }

  intializeRoutes() {
    this.router.get("/", welcome);
  }
}

export default new HomeRoutes().router;
```

[Back to TOC](#table-of-contents)

### Code Explanation

#### Imports

```ts
import { Router } from "express";
import { welcome } from "../controllers/home.controller";
```

- Imports the `Router` class from Express.
- Imports the `welcome` function from the `home.controller` module.

#### Class Definition

```ts
class HomeRoutes {
  router = Router();
```

- Defines the `HomeRoutes` class.
- Initializes a new `Router` instance and assigns it to the `router` property.

#### Constructor

```ts
constructor() {
    this.intializeRoutes();
  }
```

- Calls the `initializeRoutes` method when a new instance of `HomeRoutes` is created.

#### Method

```ts
intializeRoutes() {
    this.router.get("/", welcome);
  }
```

- Defines a method that sets up a route for the root path (`"/"`) and maps it to the `welcome` controller function.

#### Export

```ts
export default new HomeRoutes().router;
```

- Creates a new instance of `HomeRoutes` and exports its `router` property.

[Back to TOC](#table-of-contents)

### TypeScript Syntax Explanation

[Back to TOC](#table-of-contents)

## (`src`) / (`routes`) / `tutorial.routes.ts`

### Code

```ts
import { Router } from "express";
import TutorialController from "../controllers/tutorial.controller";

class TutorialRoutes {
  router = Router();
  controller = new TutorialController();

  constructor() {
    this.intializeRoutes();
  }

  intializeRoutes() {
    // Create a new Tutorial
    this.router.post("/", this.controller.create);

    // Retrieve all Tutorials
    this.router.get("/", this.controller.findAll);

    // Retrieve a single Tutorial with id
    this.router.get("/:id", this.controller.findOne);

    // Update a Tutorial with id
    this.router.put("/:id", this.controller.update);

    // Delete a Tutorial with id
    this.router.delete("/:id", this.controller.delete);
  }
}

export default new TutorialRoutes().router;
```

[Back to TOC](#table-of-contents)

### Code Explanation

[Back to TOC](#table-of-contents)

### TypeScript Syntax Explanation

[Back to TOC](#table-of-contents)

## (`src`) / (`controllers`) / `home.controller.ts`

### Code

```ts
import { Request, Response } from "express";

export function welcome(req: Request, res: Response): Response {
  return res.json({ message: "Welcome to bezkoder application." });
}
```

[Back to TOC](#table-of-contents)

### Code Explanation

#### Imports

```ts
import { Request, Response } from "express";
```

- Imports the `Request` and `Response` **_types_** from Express.

#### Function

```ts
export function welcome(req: Request, res: Response): Response {
  return res.json({ message: "Welcome to bezkoder application." });
}
```

- Defines and exports the `welcome` function.
- Sends a JSON response with a welcome message.

[Back to TOC](#table-of-contents)

### TypeScript Syntax Explanation

[Back to TOC](#table-of-contents)

## (`src`) / (`controllers`) / `tutorial.controller.ts`

### Code

```ts
import { Request, Response } from "express";

export default class TutorialController {
  async create(req: Request, res: Response) {
    try {
      res.status(201).json({
        message: "create OK",
        reqBody: req.body,
      });
    } catch (err) {
      res.status(500).json({
        message: "Internal Server Error!",
      });
    }
  }

  async findAll(req: Request, res: Response) {
    try {
      res.status(200).json({
        message: "findAll OK",
      });
    } catch (err) {
      res.status(500).json({
        message: "Internal Server Error!",
      });
    }
  }

  async findOne(req: Request, res: Response) {
    try {
      res.status(200).json({
        message: "findOne OK",
        reqParamId: req.params.id,
      });
    } catch (err) {
      res.status(500).json({
        message: "Internal Server Error!",
      });
    }
  }

  async update(req: Request, res: Response) {
    try {
      res.status(200).json({
        message: "update OK",
        reqParamId: req.params.id,
        reqBody: req.body,
      });
    } catch (err) {
      res.status(500).json({
        message: "Internal Server Error!",
      });
    }
  }

  async delete(req: Request, res: Response) {
    try {
      res.status(200).json({
        message: "delete OK",
        reqParamId: req.params.id,
      });
    } catch (err) {
      res.status(500).json({
        message: "Internal Server Error!",
      });
    }
  }
}
```

[Back to TOC](#table-of-contents)

### Code Explanation

[Back to TOC](#table-of-contents)

### TypeScript Syntax Explanation

[Back to TOC](#table-of-contents)
