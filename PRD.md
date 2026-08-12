# Project Requirements Document (PRD) — Wearly MVP

* **Project Name:** Wearly (E-Commerce Platform)
* **Author:** Inna Levashova, Project Manager
* **Status:** In Progress / Released (MVP)

---

## 1. Executive Summary & Objective
Wearly is a modern online marketplace for clothing and accessories. The primary objective is to build a fast, reliable, and scalable MVP (Minimum Viable Product) that allows users to seamlessly browse products, authenticate securely, and complete a purchase. 

Live Demo: [great-wearly-shop.vercel.app](https://vercel.app)

---

## 2. Target Audience & User Persona
* Primary Users: Tech-savvy individuals looking for a fast, minimalist, and mobile-friendly shopping experience.
* Key Pain Points to Solve:
  * Slow loading times on mobile devices.
  * Complicated registration forms.
  * Lack of real-time inventory updates.

---

## 3. Scope of MVP (Functional Requirements)

### 3.1. User Authentication
* Users must be able to sign up and log in using an email and password.
* Authentication must be secured using JWT tokens (Django Rest Framework & SimpleJWT).
* Users must have a social login option via Google OAuth for one-click registration.

### 3.2. Product Catalog & Search
* The homepage must display featured products and categories (Clothing, Accessories).
* Users must be able to filter products by size, color, and price range.
* Data fetching for the catalog must be optimized using RTK Query to prevent redundant API calls.

### 3.3. Shopping Cart & Checkout Flow
* Unauthenticated users can add items to the cart (stored locally via Redux Toolkit).
* To proceed to checkout, the user must be authenticated.
* The checkout page must collect: Full Name, Shipping Address, and Contact Information.

### 3.4. Background Management & Scheduling
* System must sync inventory and stock levels asynchronously using Celery & Redis.
* Celery Beat schedules periodic background updates for product catalogs and availability.

---

## 4. ClickUp Task Workflow (Dev & QA Alignment)
To maintain transparency and track team velocity, the team follows a structured task lifecycle configured on the ClickUp board:

1. **PLANNING → IN PROGRESS:** The developer selects a task from the Planning column, drags it to *In Progress*, and assigns it to themselves.
2. **IN PROGRESS → IN REVIEW:** Once the feature branch is ready, the developer moves the task to *In Review* for peer code review.
3. **IN REVIEW → READY FOR QA:** After a successful code review, the developer moves the task to *Ready for QA* and changes the assignee to a QA engineer.
4. **READY FOR QA → QA IN PROGRESS:** The tester moves the task to *QA In Progress* and begins verification against Acceptance Criteria.
5. **QA IN PROGRESS → DONE:** If no bugs are found and the feature meets all requirements, the tester moves the task to the final *Done* status.
6. **QA IN PROGRESS → BLOCKED / REJECTED:** If a bug is detected, the tester leaves a descriptive comment with steps to reproduce, moves the task to *Blocked / Rejected*, and reassigns it back to the developer.

---

## 5. Non-Functional Requirements (NFR)
* Performance: Frontend pages deployed on Vercel (Next.js App Router) must achieve a Lighthouse performance score of 85+.
* Security: All API communication must be encrypted via HTTPS. Passwords must be hashed in the PostgreSQL database.
