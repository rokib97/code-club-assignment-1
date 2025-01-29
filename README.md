# **Assignment: User Management CRUD Application with TypeScript**

This assignment will help you practice and demonstrate your understanding of **TypeScript** fundamentals, including **enums**, **interfaces**, **type aliases**, **generic functions**, and **API interactions**. You will build a **User Management CRUD** application by implementing a **generic fetch function** and performing **Create**, **Read**, **Update**, and **Delete** operations on user data.

Additionally, you will simulate a backend using **JSON Server** to store and retrieve user data.

## **Assignment Structure**

1. **Part 1:** Implement a generic `handleRequest` function to simulate HTTP requests.
2. **Part 2:** Implement the CRUD operations for user management.
3. **Part 3:** Test the CRUD functions with mock data.
4. **Part 4:** Set up a simulated backend using JSON Server.

---

## **Part 1: Implementing the `handleRequest` Function**

### **Requirements**

1. Define a generic function `handleRequest` that:

   - Accepts a URL, HTTP method, and an optional request body.
   - Returns a `Response` object containing:
     - `success` (boolean): Indicates whether the request was successful.
     - `data` (of type `T`): Contains the response data.
     - `message` (optional): Contains an error message if the request failed.

2. The `handleRequest` function should handle different HTTP methods (`GET`, `POST`, `PUT`, `DELETE`).

### **Function Signature**

```typescript
async function handleRequest<T>(
  url: string,
  method: "GET" | "POST" | "PUT" | "DELETE",
  body?: T
): Promise<Response<T>>;
```

---

## **Part 2: Implementing CRUD Operations for User Management**

### **Requirements**

1. Define the `Role` enum:

   ```typescript
   enum Role {
     Admin = "admin",
     User = "user",
   }
   ```

2. Define the `User` interface:

   ```typescript
   interface User {
     id: number;
     name: string;
     email: string;
     role: Role;
   }
   ```

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

4. Each function should use `handleRequest` for API interactions.

---

## **Part 3: Testing the CRUD Functions**

### **Sample Tests**

```typescript
const newUser = await createUser({
  id: 1,
  name: "John Doe",
  email: "john@example.com",
  role: Role.Admin,
});
console.log(newUser);

const users = await getUsers();
console.log(users);

const updatedUser = await updateUser(1, {
  name: "Johnathan Doe",
  role: Role.User,
});
console.log(updatedUser);

const deleteSuccess = await deleteUser(1);
console.log(deleteSuccess);
```

---

## **Part 4: Simulating the Backend with JSON Server**

### **Setup Steps**

#### **Step 1: Install Dependencies**

```bash
npm install json-server typescript
```

#### **Step 2: Set Up `db.json`**

Create a `db.json` file to simulate a user database:

```json
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

#### **Step 3: Configure `package.json`**

```json
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

#### **Step 4: Run the Application**

1. Start **JSON Server**:
   ```bash
   npm run dev
   ```
2. Compile and run the TypeScript code:
   ```bash
   npm start
   ```

---

## **Folder Structure**

```
/user-management-crud
├── tsconfig.json
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

## **Submission Instructions**

1. Implement the `handleRequest` function and the CRUD operations.
2. Test your application using the provided test cases.
3. Submit your GitHub repository with all the code.

---
