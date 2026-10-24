# ⚙️ Nova Store Backend API

![Strapi](https://img.shields.io/badge/Strapi-v4-2E7AEA?style=for-the-badge&logo=strapi)
![Node.js](https://img.shields.io/badge/Node.js-18+-339933?style=for-the-badge&logo=nodedotjs)
![REST API](https://img.shields.io/badge/API-RESTful-orange?style=for-the-badge)

Headless CMS API service powering the **Nova Store** e-commerce platform. Built with **Strapi v4** to manage products, categories, media assets, and RESTful endpoints for the frontend.

---

## 🔗 Live Links

- **Frontend App:** [Nova Store Live](https://nova-store-git-main-ahmed-hamdy.vercel.app/)
- **Frontend Repo:** [front-end-ecommerce](https://github.com/Ahmed207-dev/front-end-ecommerce)

---

## 🏗️ Content Architecture

- **Products (`api::product`)**: Title, Description, Price, OldPrice, IsNew, Images, Category (Many-to-One).
- **Categories (`api::category`)**: Title, Description, Image, Products (One-to-Many).

---

## 🔌 Core Endpoints

| Method | Endpoint | Query / Filter Example |
| :--- | :--- | :--- |
| `GET` | `/api/products` | `/api/products?populate=*` |
| `GET` | `/api/products/:id` | `/api/products/1?populate=*` |
| `GET` | `/api/categories` | `/api/categories?populate=*` |
| `GET` | `/api/products` | `/api/products?filters[category][id][$eq]=:id&populate=*` |

---

## 🛠️ Quick Start

```bash
# Clone & install
git clone [https://github.com/Ahmed207-dev/nova-store-backend.git](https://github.com/Ahmed207-dev/nova-store-backend.git)
cd nova-store-backend
npm install

# Environment setup
cp .env.example .env

# Run development server
npm run develop
