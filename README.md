# ⚙️ Nova Store Backend - Strapi Headless CMS

![Strapi](https://img.shields.io/badge/Strapi-v4-2E7AEA?style=for-the-badge&logo=strapi)
![Node.js](https://img.shields.io/badge/Node.js-18+-339933?style=for-the-badge&logo=nodedotjs)
![Database](https://img.shields.io/badge/Database-SQLite%2FPostgreSQL-4169E1?style=for-the-badge)
![API](https://img.shields.io/badge/API-RESTful-orange?style=for-the-badge)

هذا المستودع يحتوي على خادم الخلفية (Backend) لمتجر **Nova Store** الإلكتروني، والمبني باستخدام **Strapi Headless CMS**. يُوفر الخادم لوحة تحكم إدارية كاملة لإدارة المنتجات، التصنيفات، الصور، والبيانات، بالإضافة إلى تقديم RESTful APIs لتغذية الواجهة الأمامية المرفوعة على Vercel.

---

##  Connected Frontend | الواجهة الأمامية المرتبطة

- **Live Frontend App:** [https://nova-store-git-main-ahmed-hamdy.vercel.app]

---

##  Content Architecture | هيكلة البيانات (Content Types)

تم بناء هيكلة البيانات (Schemas) داخل Strapi لتغطية متطلبات المتجر كالتالي:

### 1. Products (`api::product.product`)
- **Title** (`Short Text`): اسم المنتج.
- **Description** (`Long Text` / `Rich Text`): تفاصيل ووصف المنتج.
- **Price** (`Decimal`): سعر المنتج الحالي.
- **OldPrice** (`Decimal` - Optional): السعر قبل الخصم.
- **IsNew** (`Boolean`): تحديد ما إذا كان المنتج حديثاً.
- **Images** (`Media - Multiple`): صور المنتج المعروضة.
- **Category** (`Relation`): علاقة (Many-to-One) لربط المنتج بتصنيف معين.

### 2. Categories (`api::category.category`)
- **Title** (`Short Text`): اسم التصنيف.
- **Description** (`Long Text`): وصف التصنيف.
- **Image** (`Media - Single`): صورة غلاف التصنيف.
- **Products** (`Relation`): علاقة (One-to-Many) تضم كافة المنتجات التابعة لهذا التصنيف.

---

## 🔌 REST API Endpoints | نقاط الاتصال

يوفر الخادم نقاط اتصال جاهزة لاستدعاء البيانات من الفرونت إند:

| Method | Endpoint | Description | Example Query |
| :--- | :--- | :--- | :--- |
| `GET` | `/api/products` | جلب كافة المنتجات | `/api/products?populate=*` |
| `GET` | `/api/products/:id` | جلب منتج محدد حسب الـ ID | `/api/products/1?populate=*` |
| `GET` | `/api/categories` | جلب كافة التصنيفات مع صورها | `/api/categories?populate=*` |
| `GET` | `/api/products` | تصفية المنتجات حسب التصنيف | `/api/products?filters[category][id][$eq]=1&populate=*` |

> 📌 **ملاحظة:** ينبغي إرفاق `?populate=*` مع الـ Requests لضمان استرجاع العلاقات الصور والبيانات المرتبطة.

---

## 🔑 Permissions & Security Setup | إعداد الأذونات

لكي يتمكن تطبيق الفرونت إند من جلب البيانات بدون التعرض لخطأ `403 Forbidden`:

1. افتح لوحة تحكم الأدمن: `http://localhost:1337/admin`
2. اذهب إلى **Settings** ➔ **Users & Permissions Plugin** ➔ **Roles**.
3. اختر دور **Public**.
4. في القائمة المنسدلة لـ **Product**: حدد `find` و `findOne`.
5. في القائمة المنسدلة لـ **Category**: حدد `find` و `findOne`.
6. اضغط **Save** لحفظ التغييرات.

---

## 🚀 Local Installation & Setup | التشغيل محلياً

### 1. Clone Repository
```bash
git clone <YOUR_BACKEND_REPOSITORY_URL>
cd nova-store-backend
