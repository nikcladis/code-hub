# **Code Hub (SaaS)** 🚀💻

Code snippet manager. This project demonstrates user's ability to share, execute, and comment on code snippets in various programming languages.

---

## **Tech Stack** 🛠️
- **Frontend:** Next.js 15 ⚛️
- **Authentication:** [Clerk](https://clerk.dev) 🔑 (Google 🌐 and GitHub 🐙 authentication)
- **Database:** [Convex](https://convex.dev) 📦

---

## **Key Features** ✨
- **Authentication:**  
  🔑 Secure login via Google 🌐 and GitHub 🐙 using Clerk.
- **Code Snippet Management:**  
  📄 Create, share, and manage code snippets.  
  💬 Add comments on snippets.  
  ⭐ Star favorite snippets for quick access.
- **Code Execution Logs:**  
  🖥️ Store and view details of executed code.
- **User Management:**  
  🌟 Pro user support with LemonSqueezy integration for subscriptions.

---

## **Convex Database Schema** 🗄️
The database is structured using Convex for real-time interactions. Below is the schema definition:

```ts
import { defineSchema, defineTable } from "convex/server";
import { v } from "convex/values";

export default defineSchema({
  codeExecutions: defineTable({
    code: v.string(),
    error: v.optional(v.string()),
    language: v.string(),
    output: v.optional(v.string()),
    userId: v.string(),
  }).index("by_user_id", ["userId"]),
  snippetComments: defineTable({
    content: v.string(),
    snippetId: v.id("snippets"),
    userId: v.string(),
    userName: v.string(),
  }).index("by_snippet_id", ["snippetId"]),
  snippets: defineTable({
    code: v.string(),
    language: v.string(),
    title: v.string(),
    userId: v.string(),
    userName: v.string(),
  }).index("by_user_id", ["userId"]),
  stars: defineTable({
    snippetId: v.id("snippets"),
    userId: v.string(),
  })
    .index("by_snippet_id", ["snippetId"])
    .index("by_user_id", ["userId"])
    .index("by_user_id_and_snippet_id", [
      "userId",
      "snippetId",
    ]),
  users: defineTable({
    email: v.string(),
    isPro: v.boolean(),
    lemonSqueezyId: v.optional(v.string()),
    lemonSqueezyOrderId: v.optional(v.string()),
    name: v.string(),
    proSince: v.optional(v.float64()),
    userId: v.string(),
  }).index("by_user_id", ["userId"]),
});
```

## **Getting Started** 🏁

### **Prerequisites** ✅
- **Node.js** (v16 or higher) 🟢
- **npm** or **yarn** 📦
- **Convex CLI** 🔧
- **Clerk API keys** 🔑

---

### **Installation** 📥
1. **Clone the repository:**
   ```bash
   git clone https://github.com/yourusername/code-hub-saas.git
   ```
2. **Navigate to the project directory:**
    ```bash
    cd code-hub-saas
    ```

3. **Install dependencies:**

    ```bash
    npm install
    ```

4. **Setup ⚙️**

    Create a .env file and add your Clerk and Convex credentials:

    ```env
    NEXT_PUBLIC_CLERK_FRONTEND_API=<your-clerk-api>
    CONVEX_URL=<your-convex-url>
    ```

5. **Run the Convex schema:**
    
    ```bash
    npx convex dev
    ```

6. **Start the development server:**
    ```bash
    npm run dev
    ```
7. **Access the application at:**
    ```arduino
    http://localhost:3000
    ```
---

## Usage 📘
- **Sign In**: Log in using your Google 🌐 or GitHub 🐙 account.
- **Create Snippets**: Add code snippets with a title, language, and optional description.
- **Collaborate**: Add comments 💬 and discuss snippets with other users.
- **Pro Features**: Unlock advanced features 🌟 by upgrading to Pro via LemonSqueezy.

