# Lego Store

## Links

- Website/Frontend: <https://legostore.namakita.com>
  - Backend API: <https://legostore.namakita.com>
- Repositories:
  - General: <https://github.com/ADaneshS1/legostore>
  - Backend API: <https://github.com/ADaneshS1/legostore-backend>
  - Frontend Web: <https://github.com/ADaneshS1/legostore-frontend>
- Project Management: <https://linear.app/lego-store>

Inspirations:

- <https://store.epicgames.com/en-US> - Official digital retailer and merchandise shop for Ubisoft games, offering PC digital downloads, exclusive collector’s editions, and apparel

## Features

- Home page
  - Hero section
  - Products catalogue. Example: <https://store.ubisoft.com/sea/category-best-sellers?lang=en_ID>
- Product page
  - Image URL
  - SKU (stock keeping unit)
  - Name
  - Price
  - Description
  - Stock level / In stock or not
  - Genre (Action, Adventure, Building, Fantasy, Horror, Mystery, Sci-Fi, Sports, Superhero, War)
  - Add to Cart Form:
    - Quantity Input
    - Increment & Decrement Button
    - Add to Cart Submit Button
- Shopping Cart page
  - Product items to buy
    - Image, name, price, quantity, subtotal (price x quantity)
    - Remove item
    - Change quantity form
  - Link: continue shopping, go to products catalogue
  - Link: checkout
- Checkout page
  - Order summary
    - Product items to buy
    - Grand total of all product items to buy
- Place order / transaction is being processed

## UI Designs

- Figma: <https://www.figma.com/design/PVqc1U4wZXOhI6TJZx3EHt/legostore-designs?node-id=0-1&t=O7nHxm8buiD1fqD0-1>

### Home Page

<img alt="Home Page" src="./designs/home.jpg" width="400" />

### Product by Slug

<img alt="Product by Slug" src="./designs/product-by-slug.jpg" width="400" />

## Backend REST API Endpoints

- Production: `https://legostore.namakita.com`
- Local: `http://localhost:3000`

Priority:

| Endpoint           | HTTP  | Description         | Permission |
| ------------------ | ----- | ------------------- | ---------- |
| `/products`        | `GET` | Get all products    | Public     |
| `/products/{slug}` | `GET` | Get product by slug | Public     |

With Auth:

| Endpoint         | HTTP   | Description              | Permission    |
| ---------------- | ------ | ------------------------ | ------------- |
| `/users`         | `GET`  | Get all users            | Public        |
| `/users/{id}`    | `GET`  | Get user by id           | Public        |
| `/auth/register` | `POST` | Register new user        | Public        |
| `/auth/login`    | `POST` | Login user               | Public        |
| `/auth/me`       | `GET`  | Check authenticated user | Authenticated |
| `/auth/logout`   | `POST` | Logout user              | Authenticated |

Cart:

| Endpoint           | HTTP     | Description                    | Permission    |
| ------------------ | -------- | ------------------------------ | ------------- |
| `/cart`            | `GET`    | Get user's cart                | Authenticated |
| `/cart/items`      | `PUT`    | Add product & quantity to cart | Authenticated |
| `/cart/items/{id}` | `DELETE` | Delete product from cart       | Authenticated |
| `/cart/items/{id}` | `PATCH`  | Update product quantity        | Authenticated |

## Frontend Pages

Priority:

| Route             | Title                    |
| ----------------- | ------------------------ |
| `/`               | Home Page                |
| `/products`       | All Products Page        |
| `/products/:slug` | One Product by Slug Page |

With Auth:

| Route        | Title                   | Permission    |
| ------------ | ----------------------- | ------------- |
| `/register`  | Register Page           | Public        |
| `/login`     | Login Page              | Public        |
| `/dashboard` | Authenticated User Page | Authenticated |
| `/logout`    | Logout Page             | Authenticated |
| `/cart`      | Cart Page               | Authenticated |

## Data Structure

### Product

```json
{
  "id": "LEGO-001",
  "slug": "lego-marvel-super-heroes-2",
  "name": "LEGO® Marvel Super Heroes 2",
  "sku": "LG-MARVEL-02",
  "price": 150000,
  "stockQuantity": 25,
  "imageUrl": "https://link-your-pic.com/marvel-2.jpg",
  "createdAt": "2024-05-20T10:00:00Z",
  "updatedAt": "2024-05-20T10:00:00Z"
}
```

### Add New Product

Request Body:

```json
{
  "name": "LEGO® Jurassic World™",
  "price": 150000,
  "sku": "LG-JURASSIC-01",
  "stockQuantity": 20,
  "imageUrl": "https://example.com/jurassic-world.jpg"
}
```

Response Body:

```json
{
  "id": "ULID-JW99",
  "slug": "lego-jurassic-world",
  "name": "LEGO® Jurassic World™",
  "price": 150000,
  "sku": "LG-JURASSIC-01",
  "stockQuantity": 20,
  "imageUrl": "https://example.com/jurassic-world.jpg"
}
```
