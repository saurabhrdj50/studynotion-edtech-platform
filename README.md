# StudyNotion — Full-Stack EdTech Platform

StudyNotion is an intuitive, full-featured educational technology web application built on the **MERN** stack (MongoDB, Express.js, React.js, Node.js). It provides a seamless, role-based platform where students can browse, purchase, and consume educational courses, while instructors can author rich multimedia curriculum and analyze sales performance.

[![React](https://img.shields.io/badge/React-18-61DAFB?logo=react&logoColor=white)](https://react.dev/)
[![Tailwind CSS](https://img.shields.io/badge/TailwindCSS-3.2-38B2AC?logo=tailwind-css&logoColor=white)](https://tailwindcss.com/)
[![Redux Toolkit](https://img.shields.io/badge/Redux%20Toolkit-2.8-764ABC?logo=redux&logoColor=white)](https://redux-toolkit.js.org/)
[![Node.js](https://img.shields.io/badge/Node.js-18+-339933?logo=node.js&logoColor=white)](https://nodejs.org/)
[![Express.js](https://img.shields.io/badge/Express.js-4.21-000000?logo=express&logoColor=white)](https://expressjs.com/)
[![MongoDB](https://img.shields.io/badge/MongoDB-Mongoose%208-47A248?logo=mongodb&logoColor=white)](https://www.mongodb.com/)
[![Razorpay](https://img.shields.io/badge/Payments-Razorpay-02042B?logo=razorpay&logoColor=blue)](https://razorpay.com/)
[![Cloudinary](https://img.shields.io/badge/Media-Cloudinary-3448C5?logo=cloudinary&logoColor=white)](https://cloudinary.com/)

---

## 🎯 Problem Statement & Goals

Traditional online learning systems are often fragmented, lacking cohesive tools for instructors to construct structured video curricula and for students to track granular lesson completion.

**StudyNotion aims to:**
- Deliver an interactive, responsive learning interface with structured modular curricula (sections and subsections).
- Provide instructors with complete content lifecycle management and revenue visualization.
- Ensure secure access control with role-based permissions and robust payment checkout.

---

## 🖼️ Application Screenshots & Architecture

### Student Platform Interface
![Platform Interface](https://github.com/user-attachments/assets/0ce0ba79-c98c-4e0b-888d-7d120503996d)

### System Architecture
![System Architecture](https://github.com/user-attachments/assets/7b449fa9-c3ce-48f8-8c07-cbb28b132dbb)

### Database Schema Overview
![Database Schema](https://github.com/user-attachments/assets/191756c3-2e05-40a9-8f02-2fc24684021d)

---

## ✨ Features

### 👨‍🎓 For Students
- **Course Catalog & Search**: Browse courses filtered by categories with dynamic search and rating badges.
- **Wishlist & Cart**: Add desired courses to wishlist or shopping cart and proceed through checkout.
- **Integrated Video Player**: Stream course lecture videos with interactive navigation across sections.
- **Progress Tracking**: Automatic tracking of completed sub-sections and percentage course completion.
- **Ratings & Reviews**: Post authenticated star ratings and detailed reviews for completed courses.
- **Student Profile**: Manage personal account information, avatars, and review enrolled courses.

### 👨‍🏫 For Instructors
- **Multi-Step Course Builder**: Create courses in structured stages:
  1. *Course Information*: Title, description, prerequisites, category, thumbnail, and pricing.
  2. *Course Builder*: Add sections and upload nested video lessons with duration.
  3. *Publish Settings*: Toggle course between Draft and Published status.
- **Instructor Analytics Dashboard**: Interactive charts powered by Chart.js displaying total revenue, enrolled student count, and individual course sales stats.
- **Course Management**: Edit curriculum, update lecture videos, or remove courses.

### 🛡️ For Administrators
- **Category Management**: Create and oversee educational categories (e.g., Web Development, Python, AI) required for course categorization.

### 🔒 Authentication & Payments
- **JWT & OTP Verification**: Secure registration with email-based OTP verification via Nodemailer and encrypted passwords via Bcrypt.
- **Password Reset Flow**: Tokenized email reset links for forgotten passwords.
- **Razorpay Integration**: End-to-end payment capture, signature verification, and automatic student course enrollment.
- **Cloud Media Storage**: Secure asset and lecture video uploads offloaded to Cloudinary.

---

## 🛠️ Technology Stack

### Frontend
- **Library/Framework**: React 18
- **State Management**: Redux Toolkit & React-Redux
- **Routing**: React Router DOM (v6/v7)
- **Styling**: Tailwind CSS, PostCSS
- **Form Handling**: React Hook Form
- **Video & Media**: Video-React
- **Visualizations**: Chart.js, React-ChartJS-2
- **Notifications**: React Hot Toast
- **Icons**: React Icons (Lucide, Feather, FontAwesome)

### Backend
- **Runtime**: Node.js (v18+)
- **Framework**: Express.js (v4.21)
- **Database**: MongoDB with Mongoose (v8)
- **Authentication**: JSON Web Tokens (jsonwebtoken), Bcrypt.js, Cookie-Parser
- **File Uploads**: Express-FileUpload, Cloudinary SDK
- **Payment Processing**: Razorpay Node.js SDK
- **Email Service**: Nodemailer with SMTP
- **Scheduling**: Node-Schedule

---

## 🏛️ System Architecture

StudyNotion follows a decoupled client-server architecture:
- **Client Tier**: A responsive React SPA styled with Tailwind CSS, utilizing Redux Toolkit slices for centralized auth, cart, profile, and course progress states.
- **API Tier**: A RESTful Express.js service providing token-based authentication middleware (`auth`, `isStudent`, `isInstructor`, `isAdmin`) and specialized controllers for course authoring, payments, and ratings.
- **Storage Tier**: MongoDB storing collections for `Users`, `Courses`, `Sections`, `SubSections`, `Categories`, `RatingsAndReviews`, and `CourseProgress`. Heavy media assets are stored on Cloudinary with URLs referenced in documents.

---

## 🔌 API Design Reference

| Method | Endpoint | Description | Auth Required |
|---|---|---|---|
| `POST` | `/api/v1/auth/signup` | Register a new user | No |
| `POST` | `/api/v1/auth/login` | Authenticate user and issue JWT | No |
| `POST` | `/api/v1/auth/sendotp` | Generate and dispatch email OTP | No |
| `POST` | `/api/v1/auth/changepassword` | Update user password | Yes |
| `POST` | `/api/v1/auth/reset-password-token` | Send password reset link | No |
| `POST` | `/api/v1/auth/reset-password` | Update password via token | No |
| `GET` | `/api/v1/course/getAllCourses` | Fetch all published courses | No |
| `GET` | `/api/v1/course/getCourseDetails` | Fetch full details for a course | No |
| `POST` | `/api/v1/course/createCourse` | Create a new course | Instructor |
| `POST` | `/api/v1/course/addSection` | Add a curriculum section | Instructor |
| `POST` | `/api/v1/course/addSubSection` | Add a video sub-section | Instructor |
| `GET` | `/api/v1/course/showAllCategories` | List all course categories | No |
| `POST` | `/api/v1/course/createCategory` | Create a new category | Admin |
| `POST` | `/api/v1/payment/capturePayment` | Initiate Razorpay order | Student |
| `POST` | `/api/v1/payment/verifyPayment` | Verify signature and enroll | Student |
| `POST` | `/api/v1/course/createRating` | Submit rating and review | Student |

---

## 🚀 Getting Started

### Prerequisites
- [Node.js](https://nodejs.org/) (v18 or higher)
- [npm](https://www.npmjs.com/) (v9 or higher)
- [MongoDB](https://www.mongodb.com/) (local instance or MongoDB Atlas cluster URI)
- [Cloudinary](https://cloudinary.com/) account (Cloud Name, API Key, API Secret)
- [Razorpay](https://razorpay.com/) test account (Key ID, Secret)
- SMTP email credentials (e.g., Gmail App Password)

---

### Installation

1. **Clone the repository:**
   ```bash
   git clone https://github.com/saurabhrdj50/studynotion-edtech-platform.git
   cd studynotion-edtech-platform
   ```

2. **Install frontend dependencies:**
   ```bash
   npm install
   ```

3. **Install backend dependencies:**
   ```bash
   cd server
   npm install
   cd ..
   ```

---

### Environment Configuration

#### 1. Backend Configuration (`server/.env`)
Create a `.env` file in the `server/` directory modeled on `server/.env.example`:
```env
PORT=4000
DATABASE_URL=mongodb+srv://<username>:<password>@cluster.mongodb.net/studynotion
CORS_ORIGIN=["http://localhost:3000"]
JWT_SECRET=your_jwt_secret_key

# Mail Configuration
MAIL_HOST=smtp.gmail.com
MAIL_USER=your-email@gmail.com
MAIL_PASS=your-gmail-app-password
CONTACT_MAIL=your-email@gmail.com

# Cloudinary Credentials
CLOUD_NAME=your_cloudinary_cloud_name
API_KEY=your_cloudinary_api_key
API_SECRET=your_cloudinary_api_secret
FOLDER_NAME=images
FOLDER_VIDEO=videos

# Razorpay Credentials
RAZORPAY_KEY=your_razorpay_key_id
RAZORPAY_SECRET=your_razorpay_key_secret
```

#### 2. Frontend Configuration (`src/.env`)
Create a `.env` file in the root or `src/` directory modeled on `src/.env.example`:
```env
REACT_APP_BASE_URL=http://localhost:4000/api/v1
```

---

### Running the Application

You can start both client and server concurrently from the root directory:
```bash
npm run dev
```

Alternatively, run them in separate terminals:

- **Terminal 1: Backend Server**
  ```bash
  cd server
  npm run dev
  # Server runs at http://localhost:4000
  ```

- **Terminal 2: Frontend Client**
  ```bash
  npm start
  # Client opens at http://localhost:3000
  ```

---

### ⚠️ Initial Setup Note (Creating Categories)
Before instructors can publish courses, at least one **Category** (e.g., *Web Development*, *Data Science*) must exist in the database:
1. Sign up a new user account through the UI.
2. In your MongoDB database (`users` collection), update that user document's `accountType` field to `"Admin"`.
3. Log in with the Admin account, navigate to the Admin dashboard, and create your initial course categories.

---

## 👨‍💻 Maintainer

**Saurabh Gupta**
- GitHub: [@saurabhrdj50](https://github.com/saurabhrdj50)
- LinkedIn: [saurabh-gupta](https://www.linkedin.com/in/saurabh-gupta-9470372b6/)
- Repository: [studynotion-edtech-platform](https://github.com/saurabhrdj50/studynotion-edtech-platform)

---

## 🙏 Acknowledgements

- Built with modern open-source technologies including React, Node.js, Express, and MongoDB.
- Razorpay for test payment gateway infrastructure.
- Cloudinary for scalable multimedia asset hosting.
