

# 🧩 **WeConnect Backend**

![WeConnect Banner](https://gsxytqtnlgirrrxhwjvr.supabase.co/storage/v1/object/public/media_materials/WeConnect_banner.png)  
*A powerful backend service for the WeConnect social platform — enabling authentication, posts, follows, likes, and comments.*

---

### 🏷️ **Badges**

![Node.js](https://img.shields.io/badge/Runtime-Node.js-green?logo=node.js)
![Express](https://img.shields.io/badge/Framework-Express-black?logo=express)
![PostgreSQL](https://img.shields.io/badge/Database-PostgreSQL-316192?logo=postgresql)
![Prisma](https://img.shields.io/badge/ORM-Prisma-2D3748?logo=prisma)
![Passport.js](https://img.shields.io/badge/Auth-Passport.js-334155?logo=passport)
![License](https://img.shields.io/badge/License-MIT-yellow?logo=open-source-initiative)
![Status](https://img.shields.io/badge/Status-Active-brightgreen)

---

## ⚙️ **Overview**

The **WeConnect Backend** powers all RESTful API endpoints for the **WeConnect frontend**.  
It handles authentication, user management, post creation, comments, likes, and following relationships.

---

## ✨ **Key Features**

* 🔐 **Authentication** – Supports **GitHub** and **Google OAuth** via **Passport.js**.  
* 🧑‍💼 **User Management** – Create, update, and retrieve user profiles.  
* 📝 **Posts API** – Create, edit, delete, and fetch posts.  
* 💬 **Comments API** – Add and retrieve comments on posts.  
* ❤️ **Likes API** – Like or unlike posts.  
* 🤝 **Follow System** – Send, accept, or reject follow requests.  
* 🧭 **Feed API** – Retrieve posts from users you follow.  
* 🗄️ **Database Integration** – Managed using **Prisma ORM** with **PostgreSQL**.  
* 🔒 **JWT Tokens** – For secure API access after login.

---

## 💻 **Tech Stack**

The backend uses a **scalable, modular architecture** for maintainability and performance.

| Layer | Technology |
|-------|-------------|
| **Runtime** | Node.js |
| **Framework** | Express |
| **Database** | PostgreSQL |
| **ORM** | Prisma |
| **Authentication** | Passport.js (GitHub + Google) |
| **Token Management** | JWT |
| **Environment Management** | dotenv |

---

## 🚀 **Getting Started**

Follow these instructions to set up and run the backend server locally.

### **Prerequisites**

You must have installed:
* **Node.js**
* **npm** or **yarn**
* **PostgreSQL**

---

### **Installation**

#### 1️⃣ Clone the Repository
```bash
git clone https://github.com/VietAnhPhan/weconnect-backend.git
````

#### 2️⃣ Install Dependencies

```bash
cd weconnect-backend
npm install
# or
yarn install
```

---

## ⚙️ **Environment Variables**

Create a `.env` file in the root directory and configure the following:

```bash
PORT=5000
DATABASE_URL=postgresql://user:password@localhost:5432/weconnect
JWT_SECRET=your_jwt_secret
GOOGLE_CLIENT_ID=your_google_client_id
GOOGLE_CLIENT_SECRET=your_google_client_secret
GITHUB_CLIENT_ID=your_github_client_id
GITHUB_CLIENT_SECRET=your_github_client_secret
FRONTEND_URL=http://localhost:5173
```

---

## ▶️ **Running the Server**

### **Development Mode**

```bash
npm run dev
```

### **Production Mode**

```bash
npm run start
```

Server runs at: **[http://localhost:5000](http://localhost:5000)**

---

## 🌐 **API Endpoints**

| Method   | Endpoint           | Description                       |
| -------- | ------------------ | --------------------------------- |
| **POST** | `/api/auth/google` | Sign in using Google OAuth        |
| **POST** | `/api/auth/github` | Sign in using GitHub OAuth        |
| **GET**  | `/api/users`       | Get all users                     |
| **GET**  | `/api/users/:id`   | Get user profile                  |
| **POST** | `/api/posts`       | Create a new post                 |
| **GET**  | `/api/posts`       | Get all posts (feed)              |
| **GET**  | `/api/posts/:id`   | Get post details                  |
| **POST** | `/api/comments`    | Add a comment to a post           |
| **POST** | `/api/likes`       | Like or unlike a post             |
| **POST** | `/api/follow`      | Send a follow request             |
| **GET**  | `/api/followers`   | Get followers and following users |

---

## 🧱 **Database Schema (Prisma)**

Example `schema.prisma` outline:

```prisma
model User {
  id          String    @id @default(uuid())
  name        String
  email       String    @unique
  avatarUrl   String?
  posts       Post[]
  comments    Comment[]
  likes       Like[]
  followers   Follower[] @relation("FollowerRelation")
  following   Follower[] @relation("FollowingRelation")
}

model Post {
  id          String    @id @default(uuid())
  content     String
  imageUrl    String?
  authorId    String
  author      User       @relation(fields: [authorId], references: [id])
  comments    Comment[]
  likes       Like[]
  createdAt   DateTime   @default(now())
}

model Comment {
  id        String    @id @default(uuid())
  text      String
  authorId  String
  postId    String
  author    User      @relation(fields: [authorId], references: [id])
  post      Post      @relation(fields: [postId], references: [id])
  createdAt DateTime  @default(now())
}

model Like {
  id        String    @id @default(uuid())
  userId    String
  postId    String
  user      User      @relation(fields: [userId], references: [id])
  post      Post      @relation(fields: [postId], references: [id])
}

model Follower {
  id          String    @id @default(uuid())
  followerId  String
  followingId String
  follower    User      @relation("FollowerRelation", fields: [followerId], references: [id])
  following   User      @relation("FollowingRelation", fields: [followingId], references: [id])
}
```

---

## 🧪 **Testing**

Run tests (if configured):

```bash
npm run test
```

---

## 🤝 **Contributing**

We welcome all contributions!

1. **Fork** the repository
2. **Create** a feature branch

   ```bash
   git checkout -b feature/AmazingFeature
   ```
3. **Commit** your changes

   ```bash
   git commit -m "Add some AmazingFeature"
   ```
4. **Push** to your branch

   ```bash
   git push origin feature/AmazingFeature
   ```
5. **Open a Pull Request**

---

## 📄 **License**

Distributed under the **MIT License**.
See the `LICENSE` file for more details.

---

## 📧 **Contact**

**Viet Anh Phan** – [vietanhphan2810@gmail.com](mailto:vietanhphan2810@gmail.com)

**Project Link:** [GitHub Repository](https://github.com/VietAnhPhan/weconnect-backend)
