☁️ Cloud Storage

A full-stack photo-sharing app. Upload an image with a caption, and it appears in a feed of everyone's posts. Images are stored on **ImageKit** (cloud CDN) and post data is stored in **MongoDB**.

✨ Features

- Upload an image with a caption
- Images stored in the cloud via ImageKit (not on your server's disk)
- Feed page showing all uploaded photos and captions
- REST API built with Express

 🧰 Tech Stack

| Layer | Technology |
|-------|-----------|
| Frontend | React 19, Vite, React Router, Axios |
| Backend | Node.js, Express 5, Multer (file handling) |
| Database | MongoDB with Mongoose |
| Image storage | ImageKit |

📁 Project Structure

```
Cloud-storage/
├── Backend/
│   ├── server.js                  # Entry point
│   └── src/
│       ├── app.js                 # Express app and routes
│       ├── db/db.js               # MongoDB connection
│       ├── models/post.model.js   # Post schema (image, caption)
│       └── services/storage.service.js  # ImageKit upload
└── Frontend/
    └── src/
        ├── App.jsx                # Routes
        └── pages/
            ├── CreatePost.jsx     # Upload form
            └── Feed.jsx           # Photo feed
```
🚀 Getting Started (Local)

### Prerequisites

- Node.js 18+
- A [MongoDB Atlas](https://www.mongodb.com/atlas) database (free tier works)
- An [ImageKit](https://imagekit.io) account (free tier works)

### 1. Clone


git clone https://github.com/Dimple9812/Cloud-storage.git
cd Cloud-storage

### 2. Backend

cd Backend
npm install

Create a `Backend/.env` file:

```env
MONGODB_URI=your_mongodb_connection_string
IMAGEKIT_PRIVATE_KEY=your_imagekit_private_key
```

Start the server:

node server.js

The API runs at `http://localhost:3000`.

### 3. Frontend


cd Frontend
npm install
npm run dev

Open the URL Vite prints (usually `http://localhost:5173`).

- Upload a photo: `/create-post`
- View the feed: `/feed`

 🔌 API Reference

### `POST /create-post`

Uploads an image and creates a post. Send as `multipart/form-data`.

| Field | Type | Description |
|-------|------|-------------|
| `image` | file | The image to upload |
| `caption` | string | Caption for the photo |

**Response `201`**

```json
{
  "message": "Post created successfully",
  "post": { "_id": "...", "image": "https://ik.imagekit.io/...", "caption": "..." }
}
```

### `GET /posts`

Returns all posts.

**Response `200`**

```json
{
  "message": "Posts fetched successfully",
  "posts": [{ "_id": "...", "image": "https://...", "caption": "..." }]
}
```

## ☁️ Deployment

Recommended free setup: **Render** (backend) + **Vercel** or **Netlify** (frontend).

### Backend on Render

1. New → **Web Service**, connect this repo.
2. Root directory: `Backend`
3. Build command: `npm install`
4. Start command: `node server.js`
5. Add environment variables: `MONGODB_URI`, `IMAGEKIT_PRIVATE_KEY`
6. In MongoDB Atlas → Network Access, allow access from `0.0.0.0/0` (or Render's IPs).

### Frontend on Vercel

1. New Project, import this repo.
2. Root directory: `Frontend`
3. Framework preset: **Vite**
4. Add environment variable `VITE_API_URL` = your Render backend URL.
5. Add a `Frontend/vercel.json` so routes like `/feed` work on refresh:

json
{ "rewrites": [{ "source": "/(.*)", "destination": "/" }] }


> Before deploying, replace the hardcoded `http://localhost:3000` in `CreatePost.jsx` and `Feed.jsx` with `import.meta.env.VITE_API_URL`, and change `app.listen(3000, ...)` in `server.js` to `app.listen(process.env.PORT || 3000, ...)`.
 🔒 Security Notes

- Never commit `.env` or `node_modules/`. Add a `.gitignore` containing both.
- If keys were ever pushed to GitHub, rotate them immediately.
  
🛣️ Ideas for Improvement

- Error handling and validation (file type, size limits)
- User authentication
- Delete and edit posts
- Pagination for the feed
- Navigation bar linking Create Post and Feed

ISC
