# ✅ Top 50 Node.js + Express.js + Database Interview Questions (Expanded)

## 🔹 Node.js

### 1. What is Node.js and how does it work?
Node.js is a JavaScript runtime built on Chrome's V8 engine that uses an event-driven, non-blocking I/O model. It works by:
- **Executing JavaScript code server-side**: This allows developers to use JavaScript for backend development, enabling full-stack JavaScript applications.
- **Using a single-threaded event loop architecture**: This architecture allows Node.js to handle many connections simultaneously without creating a new thread for each connection, which is resource-intensive.
- **Handling multiple concurrent connections efficiently**: Node.js can manage thousands of connections at once, making it suitable for I/O-heavy applications like web servers.

### 2. What is the difference between Node.js and traditional backend technologies?

| Feature      | Node.js           | Traditional (PHP, Java) |
|--------------|-------------------|-------------------------|
| Architecture | Event-driven      | Thread-based            |
| Language     | JavaScript        | PHP/Java/etc.           |
| Performance  | Fast for I/O ops  | Better for CPU tasks    |
| Concurrency  | Non-blocking      | Blocking                |

- Event-driven: Node.js uses events to handle requests, while traditional technologies often rely on threads.
- JavaScript: Node.js allows developers to write server-side code in JavaScript, which is widely used for client-side scripting.
- Performance: Node.js excels in I/O operations, while traditional technologies may perform better in CPU-intensive tasks due to their multi-threaded nature.

### 3. What is the event loop in Node.js?
The event loop is what allows Node.js to perform non-blocking I/O operations by offloading operations to the system kernel when possible. It consists of:
- **Timers**: Functions like `setTimeout` and `setInterval` that schedule code execution after a specified delay.
- **Pending callbacks**: Callbacks that are waiting to be executed after their associated I/O operations complete.
- **Poll phase**: Retrieves new I/O events and executes their callbacks.
- **Check phase**: Executes callbacks scheduled by `setImmediate`.
- **Close callbacks**: Handles cleanup for closed connections.

### 4. What is the use of process object?
The process object provides:
- **Environment variables**: Access to environment variables through `process.env`, allowing configuration of applications based on the environment.
- **Command line arguments**: Access to command line arguments via `process.argv`, enabling dynamic input to applications.
- **Standard input/output streams**: Interfaces for reading from and writing to the console.
- **Process control methods**: Methods like `exit()` to terminate the process and `kill()` to send signals to other processes.
- **Memory usage information**: Access to memory usage statistics through `process.memoryUsage()`.

### 5. Explain the difference between require() and import

| require() (CommonJS)    | import (ES Modules)    |
|------------------------|-----------------------|
| Synchronous loading    | Asynchronous loading   |
| Can be called anywhere | Must be at top level   |
| `module.exports` for exports | `export`/`export default` |
| Dynamic imports with require() | Static imports only |

- **Synchronous vs Asynchronous**: `require()` loads modules synchronously, while `import` allows for asynchronous loading, improving performance in certain scenarios.
- **Scope**: `require()` can be used anywhere in the code, while `import` must be declared at the top level of the module.

### 6. What is callback hell and how can it be avoided?
Callback hell is the nesting of multiple callbacks leading to unreadable code. Solutions:
- Use **Promises**: Promises provide a cleaner way to handle asynchronous operations, allowing chaining of `.then()` and `.catch()`.
- Use **async/await**: This syntax allows writing asynchronous code that looks synchronous, improving readability.
- Modularize code: Break down complex functions into smaller, reusable functions to reduce nesting.
- Use control flow libraries: Libraries like `async.js` can help manage asynchronous flow without deep nesting.

### 7. What are Streams in Node.js?
Streams are collections of data that might not be available all at once. Types:
- **Readable**: Streams that allow reading data (e.g., `fs.createReadStream`).
- **Writable**: Streams that allow writing data (e.g., `fs.createWriteStream`).
- **Duplex**: Streams that can read and write data (e.g., TCP sockets).
- **Transform**: Streams that modify data as it is read or written (e.g., compression).

### 8. What is middleware in Node.js?
Middleware are functions that have access to:
- **Request object (`req`)**: Contains information about the HTTP request.
- **Response object (`res`)**: Used to send a response back to the client.
- **Next middleware function (`next`)**: A function to pass control to the next middleware in the stack.

Example:

```javascript
app.use((req, res, next) => {
  console.log('Middleware executed');
  next();
});
```

### 9. What is the role of package.json?
- Lists project dependencies: Specifies the libraries and packages required for the project.
- Contains project metadata: Information such as project name, version, and description.
- Defines scripts: Custom scripts for tasks like starting the server or running tests.
- Configures project settings: Settings for various tools and libraries used in the project.
- Specifies Node.js version compatibility: Ensures the project runs on the intended version of Node.js.

### 10. What is the difference between npm and npx?

| npm                  | npx                      |
|----------------------|--------------------------|
| Package manager      | Package runner           |
| Installs packages    | Runs packages temporarily |
| Requires global installation | No installation needed |

- Functionality: `npm` is used to install packages, while `npx` is used to execute packages without installing them globally.

## 🔹 Express.js

### 1. What is Express.js?
Express is a minimal and flexible Node.js web application framework that provides:
- Robust routing: Simplifies the process of defining routes for handling HTTP requests.
- Middleware support: Allows the use of middleware functions to handle requests and responses.
- HTTP helpers: Provides utility methods for common tasks like redirection and caching.
- View system integration: Supports various templating engines for rendering dynamic HTML.

### 2. What is middleware in Express?
Middleware functions that execute during the request-response cycle. They can:
- Execute any code: Custom logic can be implemented in middleware.
- Modify request/response objects: Middleware can alter the request or response before passing it along.
- End the request-response cycle: Middleware can send a response and terminate the cycle.
- Call the next middleware: Use `next()` to pass control to the next middleware function.

### 3. How to handle different HTTP methods in Express?

```javascript
app.get('/', (req, res) => { /* Handle GET */ });
app.post('/', (req, res) => { /* Handle POST */ });
```

- GET: Retrieve data from the server.
- POST: Send data to the server to create a resource.
- PUT: Update an existing resource.
- DELETE: Remove a resource from the server.

### 4. What is the difference between app.use() and app.get()?
- `app.use()`: Used for middleware that executes for all HTTP methods and routes.
- `app.get()`: Specifically handles GET requests for a defined route.

### 5. How does routing work in Express?

```javascript
const router = express.Router();
router.get('/users', (req, res) => { /* ... */ });
```

- Router: A modular way to define routes, allowing for better organization of code.
- Mounting: Routes can be mounted at specific paths, enabling nested routing.

### 6. What is next() in Express middleware?
- `next()`: Passes control to the next middleware function in the stack.
- Special cases:
  - `next('route')`: Skips remaining middleware for the current route and moves to the next route.
  - `next(err)`: Passes an error to the error handling middleware.

### 7. How do you handle errors in Express?

```javascript
app.use((err, req, res, next) => {
  console.error(err.stack);
  res.status(500).send('Something broke!');
});
```

- Error handling middleware: Defined after all other middleware and routes to catch errors and send appropriate responses.

### 8. What are route parameters and query parameters?
- Route params: Dynamic segments in the URL (e.g., `/users/:id` → `req.params.id`).
- Query params: Key-value pairs in the URL (e.g., `/users?name=John` → `req.query.name`).

### 9. How do you serve static files using Express?

```javascript
app.use(express.static('public'));
// Serves files from /public directory
```

- Static files: Files like images, CSS, and JavaScript that do not change and can be served directly.

### 10. What is the difference between global and route-level middleware?
- Global middleware: Applied to all routes using `app.use()`.
- Route-level middleware: Applied to specific routes using `router.use()`.

## 🔹 API & HTTP

### 1. What is RESTful API?
An API that follows REST architectural style:
- Stateless: Each request from the client contains all the information needed to process it.
- Cacheable: Responses can be cached to improve performance.
- Client-server: Separation of client and server concerns.
- Uniform interface: Standardized way of interacting with resources.
- Layered system: Architecture can be composed of multiple layers.

### 2. Difference between PUT and PATCH?
- PUT: Replaces the entire resource with the provided data.
- PATCH: Applies partial updates to a resource, allowing for more efficient updates.

### 3. Common HTTP status codes:
- 200 OK: Request succeeded.
- 201 Created: Resource successfully created.
- 400 Bad Request: Client sent an invalid request.
- 401 Unauthorized: Authentication required.
- 404 Not Found: Resource not found.
- 500 Internal Server Error: Server encountered an error.

### 4. What is CORS and how to handle it in Express?
Cross-Origin Resource Sharing (CORS) is a security feature that restricts web pages from making requests to a different domain than the one that served the web page. Enable CORS in Express with:

```javascript
const cors = require('cors');
app.use(cors());
```

- CORS middleware: Allows you to specify which domains are permitted to access resources.

### 5. How to secure APIs in Node.js?
- Use HTTPS: Encrypts data in transit to protect against eavesdropping.
- Input validation: Ensures that incoming data is valid and safe.
- Rate limiting: Prevents abuse by limiting the number of requests from a client.
- Authentication (JWT): Uses JSON Web Tokens for secure user authentication.
- Helmet middleware: Adds security headers to HTTP responses.
- CSRF protection: Prevents Cross-Site Request Forgery attacks.

## 🔹 Authentication

### 1. What is JWT and how does it work?
JSON Web Tokens (JWT) are a compact, URL-safe means of representing claims to be transferred between two parties. They consist of:
- **Header**: Contains metadata about the token, including the signing algorithm.
- **Payload**: Contains the claims, which are the statements about an entity (typically, the user) and additional data.
- **Signature**: Used to verify that the sender of the JWT is who it claims to be and to ensure that the message wasn't changed.

Flow:
- Server signs token: The server creates a token using a secret key.
- Client stores token: The client stores the token (usually in local storage).
- Token sent with requests: The client sends the token in the Authorization header with each request.
- Server verifies token: The server verifies the token's signature and extracts the claims.

### 2. How to implement authentication in Node.js?

```javascript
const jwt = require('jsonwebtoken');
const token = jwt.sign({ userId }, SECRET, { expiresIn: '1h' });
```

- Token generation: Use the `jsonwebtoken` library to create a token with user information and an expiration time.

### 3. Session vs Token-based auth:

| Sessions           | Tokens          |
|--------------------|-----------------|
| Server stores session | Stateless      |
| Cookie-based       | Often header-based |
| Harder to scale    | Easier to scale |

- Session management: Sessions require server-side storage, while tokens are self-contained and can be verified without server storage.

### 4. What is OAuth?
OAuth is an open standard for access delegation, commonly used for token-based authentication and authorization. It allows third-party applications to access user data without sharing credentials.

### 5. How to hash passwords securely?

```javascript
const bcrypt = require('bcrypt');
const saltRounds = 10;
bcrypt.hash(password, saltRounds, function(err, hash) {
  // Store hash in your password DB.
});
```

- Password hashing: Use the `bcrypt` library to hash passwords before storing them in the database, enhancing security.

## 🔹 Database - General

### 1. SQL vs NoSQL:

| SQL                 | NoSQL           |
|---------------------|-----------------|
| Tables with relations | Document/Key-Value |
| Schema required      | Schema-less     |
| Vertical scaling     | Horizontal scaling |

- Data structure: SQL databases use structured tables with defined schemas, while NoSQL databases offer flexible data models.

### 2. What is indexing in databases?
Indexing is a data structure technique that improves the speed of data retrieval operations at the cost of additional writes and storage space. Indexes allow the database to find data without scanning the entire table.

### 3. How to prevent SQL injection?
- Use parameterized queries: Ensure that user input is treated as data, not executable code.
- ORMs (Sequelize, TypeORM): Use Object-Relational Mapping libraries that automatically handle query parameterization.
- Input validation: Validate and sanitize user input to prevent malicious data.
- Least privilege principle: Limit database user permissions to only what is necessary.

## 🔹 MongoDB (NoSQL)

### 1. What is MongoDB?
MongoDB is a document-oriented NoSQL database that stores data in flexible JSON-like documents. It allows for dynamic schemas, making it easy to evolve data models over time.

### 2. Collection vs Document:

| Collection           | Document        |
|----------------------|-----------------|
| A grouping of MongoDB documents, similar to a table in SQL | A single record in a collection, represented as a JSON object |

### 3. Mongoose:
Mongoose is an Object Document Mapper (ODM) for MongoDB that provides:
- Schema validation: Enforces structure on documents in a collection.
- Middleware: Allows for pre and post hooks for document operations.
- Type casting: Automatically converts data types to match the schema.
- Query building: Simplifies the process of building complex queries.

### 4. CRUD with Mongoose:

```javascript
// Create
await Model.create(data);

// Read
const docs = await Model.find(query);

// Update
await Model.updateOne(filter, update);

// Delete
await Model.deleteOne(filter);
```

- CRUD operations: Mongoose provides methods for creating, reading, updating, and deleting documents in a MongoDB collection.

## 🔹 WebSocket & Socket.IO

### 1. What is WebSocket?
WebSocket is a protocol that provides full-duplex communication channels over a single TCP connection. It enables real-time data transfer between client and server with low latency and minimal overhead.

### 2. What is Socket.IO?
Socket.IO is a JavaScript library built on top of WebSocket that enables real-time, bidirectional communication between web clients and servers. It provides additional features like automatic reconnection, multiplexing, and fallback to other protocols when WebSocket is not supported.

### 3. Difference between WebSocket and Socket.IO

| Feature               | WebSocket                          | Socket.IO                          |
|-----------------------|----------------------------------|----------------------------------|
| Protocol              | WebSocket protocol                | Built on WebSocket + additional features |
| Fallback              | No fallback                      | Supports fallback to HTTP long-polling |
| Features              | Basic real-time communication    | Automatic reconnection, rooms, namespaces |
| Browser support       | Requires WebSocket support       | Works on all browsers with fallback |
| Ease of use           | Lower-level API                  | Higher-level API with more features |

## 🔹 PostgreSQL

### 1. What is PostgreSQL?
PostgreSQL is a powerful, open-source object-relational database system known for its robustness, extensibility, and standards compliance. It supports advanced data types, full ACID compliance, and complex queries.

### 2. Key features of PostgreSQL
- ACID compliant transactions.
- Support for JSON and JSONB data types.
- Advanced indexing techniques.
- Extensible with custom functions and data types.
- Strong support for concurrency and MVCC (Multi-Version Concurrency Control).

## 🔹 Prisma

### 1. What is Prisma?
Prisma is an open-source next-generation ORM (Object-Relational Mapping) tool for Node.js and TypeScript. It simplifies database access by providing a type-safe query builder and migration system.

### 2. Key features of Prisma
- Type-safe database client.
- Auto-generated queries based on schema.
- Migration system for database schema changes.
- Supports PostgreSQL, MySQL, SQLite, SQL Server, and MongoDB.
- Integration with TypeScript for better developer experience.

## 🧠 Top 20 Backend Concepts/Topics
- Event Loop & Non-blocking I/O: Understanding how Node.js handles asynchronous operations.
- Express Middleware System: The role of middleware in request handling.
- REST API Best Practices: Guidelines for designing RESTful APIs.
- Error Handling Strategies: Techniques for managing errors in applications.
- JWT Authentication Flow: The process of using JSON Web Tokens for authentication.
- Async/Await Patterns: Writing asynchronous code in a synchronous style.
- File System Operations: Interacting with the file system in Node.js.
- CORS Implementation: Configuring Cross-Origin Resource Sharing in applications.
- Rate Limiting Techniques: Preventing abuse by limiting request rates.
- Environment Configuration: Managing environment-specific settings.
- Database CRUD Operations: Performing Create, Read, Update, and Delete operations.
- SQL vs NoSQL Tradeoffs: Understanding the differences and use cases for SQL and NoSQL databases.
- Mongoose Schema Design: Best practices for designing schemas in Mongoose.
- MongoDB Aggregation: Techniques for processing and transforming data in MongoDB.
- SQL Query Optimization: Strategies for improving SQL query performance.
- Data Normalization: Organizing data to reduce redundancy.
- API Pagination: Techniques for handling large datasets in APIs.
- ACID Transactions: Ensuring data integrity in database transactions.
- Redis Caching: Using Redis for caching to improve performance.
