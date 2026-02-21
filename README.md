# E-Commerce REST API

A comprehensive Flask-based REST API for managing an e-commerce platform with users, products, and orders.

## 🚀 Features

- **User Management**: Create, read, update, and delete users
- **Product Catalog**: Full CRUD operations for products
- **Order System**: Create orders and manage product associations
- **Many-to-Many Relationships**: Orders can contain multiple products
- **Duplicate Prevention**: Automatic prevention of duplicate products in orders
- **Data Validation**: Input validation using Marshmallow schemas
- **Auto-incrementing IDs**: Database handles ID generation automatically
- **DateTime Support**: Proper timestamp handling for orders

## 🛠️ Tech Stack

- **Framework**: Flask
- **Database**: MySQL with mysql-connector-python
- **ORM**: SQLAlchemy with modern mapped annotations
- **Serialization**: Marshmallow with Flask-Marshmallow
- **Python Version**: 3.11+

## 📊 Database Schema

### Users Table
- `id` (Primary Key, Auto-increment)
- `name` (String, Required)
- `email` (String, Unique, Required)  
- `address` (String, Required)

### Products Table
- `id` (Primary Key, Auto-increment)
- `name` (String, Required)
- `price` (Float, Required)

### Orders Table
- `id` (Primary Key, Auto-increment)
- `order_date` (DateTime, Required)
- `user_id` (Foreign Key to Users)

### Order_Product Association Table
- `order_id` (Foreign Key to Orders)
- `product_id` (Foreign Key to Products)
- Composite Primary Key prevents duplicate products in orders

## 🔗 API Endpoints

### User Endpoints
| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/users` | Get all users |
| GET | `/users/<id>` | Get user by ID |
| POST | `/users` | Create new user |
| PUT | `/users/<id>` | Update user by ID |
| DELETE | `/users/<id>` | Delete user by ID |

### Product Endpoints
| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/products` | Get all products |
| GET | `/products/<id>` | Get product by ID |
| POST | `/products` | Create new product |
| PUT | `/products/<id>` | Update product by ID |
| DELETE | `/products/<id>` | Delete product by ID |

### Order Endpoints
| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/orders` | Create new order |
| PUT | `/orders/<order_id>/add_product/<product_id>` | Add product to order |
| DELETE | `/orders/<order_id>/remove_product/<product_id>` | Remove product from order |
| GET | `/orders/user/<user_id>` | Get all orders for a user |
| GET | `/orders/<order_id>/products` | Get all products in an order |

## ⚡ Features Highlights

### Duplicate Prevention
The API automatically prevents adding the same product to an order twice:
```json
{
  "message": "Product already exists in this order"
}
```

### Auto-Incrementing IDs
All entities use auto-incrementing primary keys - no need to specify IDs when creating.

### DateTime Handling
Orders support proper datetime objects with ISO 8601 format (`YYYY-MM-DDTHH:MM:SS`).

### Relationship Management
- Users can have multiple orders
- Orders can contain multiple products
- Products can be in multiple orders
- Association table prevents duplicate entries
