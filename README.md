# **Assignment: Advanced User Management CRUD Application with TypeScript**

This assignment is designed to challenge and enhance your **TypeScript** skills, including working with **enums**, **interfaces**, **type aliases**, **generic functions**, and **error handling**. You will build an advanced **User Management CRUD** application by implementing **complex data validation**, a **generic fetch function**, and performing **Create**, **Read**, **Update**, and **Delete** operations on user data. Additionally, you will integrate a **debounced search feature** and simulate a backend using **JSON Server**.

---

## **Assignment Structure**

1. **Part 1:** Implement a robust `handleRequest` function to simulate HTTP requests.
2. **Part 2:** Implement the CRUD operations for user management, including additional data validation.
3. **Part 3:** Add a **search feature** with debounced input.
4. **Part 4:** Set up a simulated backend using JSON Server.
5. **Part 5:** Implement error handling for edge cases and simulate failure scenarios.

---

## **Part 1: Implementing the `handleRequest` Function**

### **Requirements**

1. Define a generic function `handleRequest` that:

   - Accepts a `url`, HTTP `method`, optional `headers`, and an optional `request body`.
   - Returns a `Response` object containing:
     - `success` (boolean): Indicates if the request was successful.
     - `data` (of type `T` | `null`): Contains the response data or null if the request failed.
     - `message` (string): Contains an error message if the request failed.

2. Include **timeout handling** to simulate network delays (e.g., 2 seconds).
3. Throw an error if the request fails due to network or server issues.

### **Function Signature**

```typescript
async function handleRequest<T>(
  url: string,
  method: "GET" | "POST" | "PUT" | "DELETE",
  headers?: Record<string, string>,
  body?: T
): Promise<Response<T>>;
```

---

## **Part 2: Implementing CRUD Operations for User Management**

### **Requirements**

1. Define a `Role` enum and a `User` interface:

   ```typescript
   enum Role {
     Admin = "admin",
     User = "user",
     Guest = "guest",
   }

   interface User {
     id: number;
     name: string;
     email: string;
     role: Role;
     createdAt: string;
   }

   interface Response<T> {
     success: boolean;
     data: T | null;
     message: string;
   }
   ```

2. Implement the following CRUD operations:

   - **Create a new user**:

     - Validate that the `email` is unique and properly formatted using regex.
     - Validate that `role` is one of the allowed `Role` values.

     ```typescript
     async function createUser(
       user: Omit<User, "id" | "createdAt">
     ): Promise<User>;
     ```

   - **Get all users**:

     - Support filtering by `role` using query parameters.

     ```typescript
     async function getUsers(roleFilter?: Role): Promise<User[]>;
     ```

   - **Update an existing user**:

     - Allow updating only specific fields using a `Partial<User>` type.
     - Throw an error if the user ID does not exist.

     ```typescript
     async function updateUser(
       id: number,
       updatedUser: Partial<Omit<User, "id" | "createdAt">>
     ): Promise<User | null>;
     ```

   - **Delete a user by ID**:
     - Simulate a confirmation step before deletion.
     ```typescript
     async function deleteUser(id: number): Promise<boolean>;
     ```

3. Each function must use `handleRequest` and implement error handling for:
   - Network issues.
   - Invalid data input.
   - Nonexistent user IDs.

---

## **Part 3: Adding a Search Feature**

### **Requirements**

1. Implement a **debounced search** for filtering users by `name` or `email`.
2. Create a `searchUsers` function:
   ```typescript
   async function searchUsers(query: string): Promise<User[]>;
   ```
3. Implement the debounce logic in a `utils` function:

   ```typescript
   function debounce<T extends (...args: any[]) => void>(
     func: T,
     delay: number
   ): (...args: Parameters<T>) => void;
   ```

4. Test the search functionality with multiple users in the database.

---

## **Part 4: Simulating the Backend with JSON Server**

### **Setup Steps**

#### **Step 1: Install Dependencies**

```bash
npm install json-server typescript
```

#### **Step 2: Set Up `db.json`**

Create a `db.json` file to simulate the database with extended fields:

```json
{
  "users": [
    {
      "id": 1,
      "name": "John Doe",
      "email": "john.doe@example.com",
      "role": "admin",
      "createdAt": "2025-01-01T12:00:00.000Z"
    },
    {
      "id": 2,
      "name": "Jane Smith",
      "email": "jane.smith@example.com",
      "role": "user",
      "createdAt": "2025-01-02T12:00:00.000Z"
    }
  ]
}
```

#### **Step 3: Configure `package.json`**

Add the following scripts:

```json
"scripts": {
  "dev": "json-server --watch db.json --port 5000",
  "start": "tsc && node dist/index.js"
}
```

---

## **Part 5: Error Handling**

### **Requirements**

1. Handle the following edge cases:

   - **Network errors**: Simulate timeouts in `handleRequest`.
   - **Duplicate email validation** during `createUser`.
   - **Nonexistent user** during `updateUser` or `deleteUser`.

2. Update the `Response` interface to include detailed error information:

   ```typescript
   interface Response<T> {
     success: boolean;
     data: T | null;
     message: string;
     errorCode?: string;
   }
   ```

3. Test the error handling by simulating failures.

---

## **Folder Structure**

```
/user-management-crud
├── tsconfig.json
├── /src
│   ├── /models
│   │   └── user.ts       # Define Role enum, User interface, and Response interface
│   ├── /utils
│   │   ├── api.ts        # Implement the handleRequest function
│   │   └── debounce.ts   # Implement debounce logic
│   └── index.ts          # Main file to test the CRUD operations and search feature
├── db.json               # Simulated backend data
├── package.json          # Project dependencies and scripts
└── README.md             # Documentation
```

---

## **Submission Instructions**

1. Complete all parts of the assignment.
2. Submit a GitHub repository with your code, including test cases.
3. Include a `README.md` file with setup and usage instructions.

Good luck and happy coding! 🚀
