# **Assignment: User Management CRUD Application with TypeScript**

This assignment will help you practice and demonstrate your understanding of **TypeScript** fundamentals, including **enums**, **interfaces**, **type aliases**, **generic functions**, and **API interactions**. You will build a **User Management CRUD** application by implementing a **generic fetch function** and performing **Create**, **Read**, **Update**, and **Delete** operations on user data.

Additionally, you will simulate a backend using **JSON Server** to store and retrieve user data.

### **Assignment Structure:**

1. **Part 1:** Implement a generic `handleRequest` function to simulate HTTP requests.
2. **Part 2:** Implement the CRUD operations for user management.
3. **Part 3:** Test the CRUD functions with mock data.

---

### **Part 1: Implementing the `handleRequest` Function**

The first step is to implement a generic function called `handleRequest`. This function should handle HTTP requests for different methods like `GET`, `POST`, `PUT`, and `DELETE`. It will simulate interacting with a backend API (using the mock data stored in `db.json`).

#### **Requirements:**

1. Define a generic function `handleRequest` that:

   - Accepts a URL, HTTP method, and an optional request body.
   - Returns a `Response` object containing:
     - `success` (boolean): Indicates whether the request was successful.
     - `data` (of type `T`): Contains the response data.
     - `message` (optional): Contains an error message if the request failed.

2. The `handleRequest` function should be flexible to handle different HTTP methods (GET, POST, PUT, DELETE).

#### **Function Signature:**

```typescript
async function handleRequest<T>(
  url: string,
  method: "GET" | "POST" | "PUT" | "DELETE",
  body?: T
): Promise<Response<T>>;
```

---

### **Part 2: Implementing CRUD Operations for User Management**

Once you've implemented the `handleRequest` function, you need to implement the CRUD operations for managing user data. You will use the mock backend (simulated by **JSON Server** with a `db.json` file).

#### **Requirements:**

1. Define the `Role` enum with the following values:

   - `Admin`
   - `User`

2. Define the `User` interface with the following properties:

   - `id`: number
   - `name`: string
   - `email`: string
   - `role`: `Role`

3. Implement the following CRUD operations:

   - **Create a new user**:

     ```typescript
     async function createUser(user: User): Promise<User>;
     ```

   - **Get all users**:

     ```typescript
     async function getUsers(): Promise<User[]>;
     ```

   - **Update an existing user**:

     ```typescript
     async function updateUser(
       id: number,
       updatedUser: Partial<User>
     ): Promise<User | null>;
     ```

   - **Delete a user by ID**:

     ```typescript
     async function deleteUser(id: number): Promise<boolean>;
     ```

4. Each of these functions should interact with the simulated backend through the `handleRequest` function.

---

### **Part 3: Testing the CRUD Functions**

Once you’ve implemented the `handleRequest` function and CRUD operations, test their functionality by calling the functions in sequence.

#### **Sample Tests:**

- **Create a new user**:

  ```typescript
  const newUser = await createUser({
    id: 1,
    name: "John Doe",
    email: "john@example.com",
    role: Role.Admin,
  });
  console.log(newUser);
  ```

- **Get all users**:

  ```typescript
  const users = await getUsers();
  console.log(users);
  ```

- **Update a user**:

  ```typescript
  const updatedUser = await updateUser(1, {
    name: "Johnathan Doe",
    role: Role.User,
  });
  console.log(updatedUser);
  ```

- **Delete a user**:

  ```typescript
  const deleteSuccess = await deleteUser(1);
  console.log(deleteSuccess);
  ```

---

### **Simulating the Backend with JSON Server**

As you don't have a backend, you will simulate one using **JSON Server**. It will allow you to mock API requests by interacting with a local JSON file (`db.json`), which will act as your mock database.

#### **Step 1: Install Dependencies**

In order to simulate the backend, you need to install **JSON Server** and **TypeScript**.

```bash
npm install json-server typescript
```

#### **Step 2: Set Up `db.json`**

Create a `db.json` file at the root of your project to simulate a user database. This file will store and serve user data.

```json
// db.json
{
  "users": [
    {
      "id": 1,
      "name": "John Doe",
      "email": "john.doe@example.com",
      "role": "admin"
    }
  ]
}
```

#### **Step 3: Create `package.json`**

In your `package.json`, add the following scripts to start **JSON Server** and run your TypeScript code:

```json
// package.json
{
  "name": "user-management-crud",
  "version": "1.0.0",
  "scripts": {
    "dev": "json-server --watch db.json --port 5000",
    "start": "tsc && node dist/index.js"
  },
  "dependencies": {
    "json-server": "^0.16.3"
  },
  "devDependencies": {
    "typescript": "^4.5.4"
  }
}
```

- **`npm run dev`** will start **JSON Server** and watch changes to `db.json` (on `localhost:5000`).
- **`npm start`** will compile your TypeScript code and run the application.

#### **Step 4: Test the Application**

1. First, start **JSON Server** by running:

   ```bash
   npm run dev
   ```

2. Then, compile and run your TypeScript code:

   ```bash
   npm start
   ```

This will simulate API requests for CRUD operations, and you can test your functions as if they were interacting with a real backend.

---

### **Folder Structure:**

```
/user-management-crud
├── /src
│   ├── /models
│   │   └── user.ts       # Define Role enum, User interface, and Response interface
│   ├── /utils
│   │   └── api.ts        # Implement the handleRequest function
│   └── index.ts          # Main file to test the CRUD operations
├── db.json               # Simulated data for JSON Server (mock backend)
├── package.json          # Project dependencies and scripts
└── README.md             # Documentation
```

---

### **Submission Instructions:**

1. Implement the handleRequest function and the specified CRUD operations.
2. Test the functionality of your application using the provided test cases.
3. Submit your GitHub repository with all the code.

---
