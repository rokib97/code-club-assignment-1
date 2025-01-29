# **Advanced User Management CRUD Application with TypeScript**

This assignment will strengthen your **TypeScript** skills, covering **enums, interfaces, type aliases, generic functions, and error handling**. You will build a **User Management CRUD** application with **data validation, a generic fetch function, debounced search**, and a **simulated backend** using **JSON Server**.

---

## **Assignment Breakdown**

1. **Implement a generic `handleRequest` function** for API communication.
2. **Build CRUD operations** for managing users with validation.
3. **Add a debounced search feature**.
4. **Set up a JSON Server backend**.
5. **Implement robust error handling**.

---

## **1. Implementing `handleRequest` Function**

### **Requirements**

- Create a generic function `handleRequest<T>`:
  - Accepts `url`, HTTP `method`, optional `headers`, and an optional `body`.
  - Returns a response object:
    ```typescript
    interface Response<T> {
      success: boolean;
      data: T | null;
      message: string;
      errorCode?: string;
    }
    ```
  - Simulates **network delays (2s)** and handles errors.

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

## **2. Implementing CRUD Operations**

### **Data Models**

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
```

### **CRUD Functions**

#### **1. Create User**

- Validate `email` format and uniqueness.
- Validate `role` against `Role` enum.

```typescript
async function createUser(
  user: Omit<User, "id" | "createdAt">
): Promise<Response<User>>;
```

**Test Input:**

```typescript
createUser({
  name: "Alice Brown",
  email: "alice.brown@example.com",
  role: Role.User,
});
```

#### **2. Get Users (Optional Role Filter)**

```typescript
async function getUsers(roleFilter?: Role): Promise<Response<User[]>>;
```

**Test Input:**

```typescript
getUsers(Role.Admin); // Fetch only admin users
```

#### **3. Update User**

- Allow updating only specific fields (`Partial<User>`).
- Throw error if `id` does not exist.

```typescript
async function updateUser(
  id: number,
  updatedUser: Partial<Omit<User, "id" | "createdAt">>
): Promise<Response<User | null>>;
```

**Test Input:**

```typescript
updateUser(1, { name: "Updated Name" });
```

#### **4. Delete User**

- Simulate a confirmation step before deletion.

```typescript
async function deleteUser(id: number): Promise<Response<boolean>>;
```

**Test Input:**

```typescript
deleteUser(2);
```

---

## **3. Implementing Debounced Search**

### **Requirements**

- Implement a debounced search for users by `name` or `email`.
- Use a `debounce` utility function.

```typescript
function debounce<T extends (...args: any[]) => void>(
  func: T,
  delay: number
): (...args: Parameters<T>) => void;
```

```typescript
async function searchUsers(query: string): Promise<Response<User[]>>;
```

**Test Input:**

```typescript
searchUsers("Alice");
```

---

## **4. Simulating Backend with JSON Server**

### **Setup Steps**

#### **1. Install Dependencies**

```bash
npm install json-server typescript
```

#### **2. Create `db.json`**

```json
{
  "users": [
    {
      "id": 1,
      "name": "John Doe",
      "email": "john.doe@example.com",
      "role": "admin",
      "createdAt": "2025-01-01T12:00:00.000Z"
    }
  ]
}
```

#### **3. Add `package.json` Scripts**

```json
"scripts": {
  "dev": "json-server --watch db.json --port 5000",
  "start": "tsc && node dist/index.js"
}
```

- JSON Server will be accessible at: `http://localhost:5000/users`

---

## **5. Error Handling**

### **Requirements**

1. Handle:

   - **Network failures** (Simulated in `handleRequest`).
   - **Duplicate email validation** in `createUser`.
   - **Nonexistent user** in `updateUser` / `deleteUser`.

2. Use `errorCode` in `Response<T>` to indicate error types.

3. Simulate error scenarios and validate responses.

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
2. Submit a **GitHub repository** with:
   - Your **TypeScript code**.
   - A **README.md** with setup and usage instructions.
   - Test cases for each function.

Good luck and happy coding! 🚀
