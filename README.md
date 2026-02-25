# AMGphone Store

A modern e-commerce website for selling mobile phones, built with Next.js, TypeScript, Tailwind CSS, and Firebase.

## Features

- **Home Page**: Hero section, featured products, brand showcase
- **Products Page**: Product listing with filters (brand, price, search)
- **Product Details**: Full product information with image gallery
- **Shopping Cart**: Add/remove items, update quantities, checkout
- **Contact Page**: Contact form with store information
- **Admin Dashboard**: Protected admin panel for managing products and orders
- **Cash on Delivery**: Simple checkout with COD payment

## Tech Stack

- **Framework**: Next.js 14 (App Router)
- **Language**: TypeScript
- **Styling**: Tailwind CSS
- **Backend**: Firebase (Firestore + Auth + Storage)
- **Icons**: Lucide React

## Project Structure

```
AMGphone-store/
├── public/
│   └── images/products/
├── src/
│   ├── app/                    # Next.js App Router
│   │   ├── page.tsx           # Home page
│   │   ├── layout.tsx         # Root layout
│   │   ├── products/          # Products pages
│   │   ├── contact/           # Contact page
│   │   ├── cart/              # Shopping cart
│   │   └── admin/             # Admin panel
│   ├── components/
│   │   ├── ui/                # UI components
│   │   ├── layout/            # Layout components
│   │   └── product/           # Product components
│   ├── context/
│   │   ├── AuthContext.tsx    # Authentication context
│   │   └── CartContext.tsx    # Shopping cart context
│   ├── hooks/
│   │   ├── useAuth.ts
│   │   └── useCart.ts
│   ├── lib/
│   │   ├── firebase.ts        # Firebase config
│   │   ├── db.ts              # Database functions
│   │   └── utils.ts           # Utilities
│   └── styles/
│       └── globals.css
├── .env.local                  # Environment variables
├── next.config.js
├── tailwind.config.ts
└── package.json
```

## Setup Instructions

### 1. Create Firebase Project

1. Go to [Firebase Console](https://console.firebase.google.com/)
2. Create a new project
3. Enable **Authentication** (Email/Password provider)
4. Create a **Firestore Database**
5. Enable **Storage** for product images
6. Go to Project Settings > General > Your apps > Web app
7. Copy the Firebase config object

### 2. Configure Environment Variables

Create a `.env.local` file in the root directory:

```env
NEXT_PUBLIC_FIREBASE_API_KEY=your_api_key
NEXT_PUBLIC_FIREBASE_AUTH_DOMAIN=your_project.firebaseapp.com
NEXT_PUBLIC_FIREBASE_PROJECT_ID=your_project_id
NEXT_PUBLIC_FIREBASE_STORAGE_BUCKET=your_project.appspot.com
NEXT_PUBLIC_FIREBASE_MESSAGING_SENDER_ID=your_sender_id
NEXT_PUBLIC_FIREBASE_APP_ID=your_app_id
```

### 3. Create Admin User

1. Go to Firebase Console > Authentication
2. Add a new user with email: `admin@amgphone.com`
3. Set password: `admin123` (or your preferred password)

### 4. Firestore Database Rules

Set these security rules in Firestore:

```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    // Products - public read, admin write
    match /products/{productId} {
      allow read: if true;
      allow write: if request.auth != null;
    }
    
    // Orders - admin read, public create
    match /orders/{orderId} {
      allow read: if request.auth != null;
      allow create: if true;
    }
  }
}
```

### 5. Storage Rules

```javascript
rules_version = '2';
service firebase.storage {
  match /b/{bucket}/o {
    match /products/{allPaths=**} {
      allow read: if true;
      allow write: if request.auth != null;
    }
  }
}
```

### 6. Install Dependencies

```bash
npm install
```

### 7. Run Development Server

```bash
npm run dev
```

Open [http://localhost:3000](http://localhost:3000)

### 8. Build for Production

```bash
npm run build
```

## Deploy to Vercel

### Option 1: Using Vercel CLI

1. Install Vercel CLI:
```bash
npm i -g vercel
```

2. Login to Vercel:
```bash
vercel login
```

3. Deploy:
```bash
vercel --prod
```

### Option 2: Using GitHub + Vercel Dashboard

1. Push your code to GitHub
2. Go to [Vercel Dashboard](https://vercel.com/dashboard)
3. Click "Add New Project"
4. Import your GitHub repository
5. Add environment variables in Vercel dashboard
6. Deploy!

## Admin Panel Access

- URL: `/admin/login`
- Default credentials: 
  - Email: `admin@amgphone.com`
  - Password: `admin123`

## Features Checklist

- [x] Modern responsive design (Blue/White/Gray theme)
- [x] Home page with hero and featured products
- [x] Products page with filters
- [x] Product detail page
- [x] Shopping cart with local storage
- [x] Contact page
- [x] Admin dashboard (protected)
- [x] Product management (CRUD)
- [x] Order management
- [x] Cash on delivery checkout
- [x] Firebase integration
- [x] Mobile responsive

## License

MIT License
