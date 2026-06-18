# TroHub - Project Blueprint

## 1. Project Overview
The TroHub-Clone project focuses on building a comprehensive boarding room management system. It assists landlords and tenants in efficiently managing contracts, invoices, and maintenance or repair operations.

### Repository & Version Control
* **Primary Repository:** `https://github.com/shenjohnsons11/TroHub-Clone.git`
* **Default Branch:** `main` (Production-ready code)
* **Development Branch:** `develop` (All feature branches must target and merge into this branch)
* **Branch Naming Convention:** `feature/feature-name`, `bugfix/issue-name`, `hotfix/urgent-fix`

### Deployment & Environment
* **Production Backend API:** `https://api-phong-tro.onrender.com/`
* **Database Connection (MongoDB URI):** `mongodb+srv://trohub_admin:Trohub2026DB@cluster0.f65y9rd.mongodb.net/TroHubDB?appName=Cluster0`

## 2. Agent Persona & Focus
You act as an **Expert Backend Engineer**. Your core responsibilities include:
- Focusing intensely on performance optimization, business logic implementation, and data security within the Backend module.
- Understanding the overall architecture to ensure smooth data flow and integration with the Web Admin interface and the Mobile App.

## 3. Tech Stack
* **Backend API & Database:** Node.js, Express, MongoDB.
* **Web Admin (Landlords):** React, HTML, CSS, JavaScript.
* **Mobile App (Landlords & Tenants):** Expo Router, TypeScript, UI Components.

## 4. Coding Standards & Strict Rules
Preserve Documentation: Never delete old comments in the source code. It is critical to maintain the historical context and original logic markers of the project.

Mandatory Testing: Every new or updated API endpoint must have accompanying unit tests written for it before the implementation is considered complete.

Terminology Consistency: Always use the exact terminology Nguoi thue (or NGUOI_THUE depending on casing rules) for tenants across all database structures, Schema Models, and API Responses to maintain professional consistency. Do not use variations like "Khach thue".

Data Modeling Constraints: In the database design, ensure that "Repair Requests" are linked directly to the Tenants (NGUOI_THUE) rather than the Rooms.

Separation of Concerns: Strictly follow the MVC architecture in the Backend directory. System configurations, entity definitions, routing, and business logic must be isolated in their respective designated folders.

Git Workflow: When creating changes, always propose a clear branch name following the project convention. Ensure commit messages are structured using Semantic Commits (e.g., feat: add login api, fix: resolve crash on home screen).

## 5. Architecture & Directory Structure
The system is organized into a clear, layered architecture within the root directory `trohub-web-only/`:

```text
trohub-web-only/  
│
├── API_DuAnTotNghiep/           <-- 1. BACKEND API & DATABASE  
│   ├── src/  
│   │   ├── configs/             # Database connection configurations (MongoDB)
│   │   ├── controllers/         # API business logic and request handling
│   │   ├── models/              # Database schema definitions
│   │   └── routes/              # API route definitions and endpoints
│   ├── server.js                # Backend application entry point
│   └── package.json  
│
├── src/                         <-- 2. WEB ADMIN (For Landlords)  
│   ├── api.js                   # Logic for making Backend API calls
│   ├── app.js                   # Main Admin dashboard interface
│   ├── styles.css               # Application styling
│   └── (index.html outside)     # Main Web Admin HTML page
│
└── TroHub_repo/                 <-- 3. MOBILE APP (Landlords & Tenants)
    ├── app/                     # Screen navigation setup (Expo Router)
    ├── components/              # Reusable UI components
    ├── screens/                 # Application interfaces (Login, Contracts, Invoices...)
    ├── services/                # API interaction services for the backend
    ├── types/                   # TypeScript type definitions
    └── package.json             # Expo project configuration



   