
# ResumeEdge: AI-Powered Professional Resume Builder

**ResumeEdge** is a comprehensive **MERN stack application** designed to streamline the professional resume creation process. It features a robust architecture including containerization, cloud storage integration, and a fully automated **CI/CD pipeline** for seamless deployment.

---

## 📸 Demo & Deployment Gallery

> **TIP:** This section is reserved for visual proof of the working deployment.

### 🔁 Automated CI/CD Pipeline
_Insert a video or GIF here showing a Git push triggering a green checkmark in GitHub Actions._

### ☁️ AWS Infrastructure
_Insert screenshots of:_
- EC2 Dashboard showing the running instance  
- S3 Bucket displaying uploaded assets  

### 🌐 Live Application
_Insert screenshots of:_
- Final website dashboard  
- Resume editor interface  

---

## ✨ Features

- **Interactive Resume Builder** – User-friendly interface to create and edit resumes in real time  
- **AI Resume Analysis** – Smart analysis to optimize resume content  
- **Cloud Storage** – Secure storage of profile images and PDFs using Amazon S3  
- **Persistent Database** – MongoDB integration for user profiles and resume data  
- **Fully Dockerized** – Multi-container architecture using Docker Compose  
- **CI/CD Pipeline** – Automated deployment to AWS EC2 via GitHub Actions  

---

## 🧰 Technology Stack

### Frontend
- React.js  
- Vite  
- Tailwind CSS  

### Backend
- Node.js  
- Express.js  

### Database
- MongoDB  

### Cloud & DevOps
- AWS EC2 (Hosting)  
- AWS S3 (Storage)  
- Docker & Docker Compose  
- GitHub Actions  

---

## 🏗 Infrastructure & Deployment Architecture

The application is deployed on an **AWS EC2 (t2.micro)** instance. Docker is used to isolate:
- Backend API  
- Frontend Web Application  
- Database  

This ensures consistency across development, testing, and production environments.

---

## 📦 Storage Integration

File uploads are handled using **Multer-S3**. When a user uploads a profile picture or saves a resume:
- Files are streamed directly to an **Amazon S3 bucket**
- Ensures high availability and durability of user assets  

---

## 🔄 CI/CD Pipeline

A fully automated deployment pipeline is implemented using **GitHub Actions**.  
On every push to the `main` branch:

1. **SSH Connection** – Secure connection to EC2 using SSH keys  
2. **Code Sync** – Latest changes pulled from GitHub  
3. **Docker Rebuild** – Docker Compose rebuilds images  
4. **Zero-Downtime Restart** – Containers restart seamlessly  

---

## ▶️ How to Run This Project

You can run this project **locally** or deploy it using the **full cloud CI/CD setup**.

---

## Option 1: Local Development (Pre-CI/CD)

### 1️⃣ Clone the Archive Branch
```bash
git clone -b pre-cicd-archive https://github.com/yourusername/ResumeEdge.git
cd ResumeEdge
```

### 2️⃣ Install Dependencies

**Backend**
```bash
cd server
npm install
```

**Frontend**
```bash
cd ../client
npm install
```

### 3️⃣ Environment Variables

Create a `.env` file inside the `server` directory:

```env
PORT=3000
MONGO_URI=your_mongodb_connection_string
JWT_SECRET=your_secret_key

# Optional: AWS Credentials (for S3 usage locally)
AWS_ACCESS_KEY_ID=your_key
AWS_SECRET_ACCESS_KEY=your_secret
S3_BUCKET_NAME=your_bucket
```

### 4️⃣ Run the Application

**Start Backend**
```bash
npm start
```

**Start Frontend**
```bash
npm run dev
```

---

## Option 2: Full Cloud Deployment with CI/CD

### 1️⃣ Repository Setup
```bash
git clone https://github.com/yourusername/ResumeEdge.git
```

### 2️⃣ Docker Setup
Ensure **Docker** and **Docker Compose** are installed.

```bash
docker compose up -d --build
```

### 3️⃣ AWS Infrastructure

- **S3 Bucket**
  - Create an S3 bucket
  - Disable *Block all public access* for image hosting  

- **EC2 Instance**
  - Ubuntu `t2.micro`
  - Open ports:
    - `80` (HTTP)
    - `5173` (Frontend)
    - `3000` (Backend API)

- **IAM User**
  - Assign `AmazonS3FullAccess`
  - Save access credentials  

### 4️⃣ GitHub Actions Configuration

Add the following secrets in  
**GitHub → Settings → Secrets & Variables → Actions**:

- `EC2_HOST` – EC2 Public IP  
- `EC2_USER` – ubuntu  
- `EC2_SSH_KEY` – content of `.pem` private key  
- `ENV_FILE` – full content of `.env` file  

### 5️⃣ Deployment

Push changes to `main` branch:

```bash
git add .
git commit -m "Deploying to production"
git push origin main
```

GitHub Actions will automatically deploy the updates to EC2.

---

## 🛠 Troubleshooting

| Issue | Cause | Solution |
|-----|------|---------|
| `ERR_CONNECTION_TIMED_OUT` | AWS Security Group | Open ports `3000` & `5173` |
| `bucket is required` | Missing env var | Define `S3_BUCKET_NAME` |
| Changes not showing | Docker cache | Use `docker compose up -d --build` |
| Server freezing | Low RAM | Enable 2GB swap on EC2 |
| Module not found | Case sensitivity | Match file names exactly |

---

## 🧹 Maintenance Commands

Free disk space on EC2:

```bash
docker system prune -a --volumes -f
```

---

## 📄 License

This project is for **educational purposes**.  
Feel free to clone, modify, and build upon it for your own use.
