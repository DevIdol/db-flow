### **Relationship List**

#### **1. Users Table**

- **One-to-Many**:
  - `users` → `orders`: A user can place multiple orders.
    - Foreign Key: `orders.userId`
  - `users` → `warehouses`: A user can be the manager of a warehouse.
    - Foreign Key: `warehouses.managerId`
  - `users` → `drivers`: A user can be a driver.
    - Foreign Key: `drivers.userId`
  - `users` → `complaints`: A user can file multiple complaints.
    - Foreign Key: `complaints.userId`
  - `users` → `returns`: A user can initiate multiple return requests.
    - Foreign Key: `returns.processedBy`

#### **2. Orders Table**

- **One-to-Many**:

  - `orders` → `orderItems`: An order can have multiple items.
    - Foreign Key: `orderItems.orderId`
  - `orders` → `deliveries`: An order can have one or more delivery records.
    - Foreign Key: `deliveries.orderId`
  - `orders` → `complaints`: An order can have multiple complaints.
    - Foreign Key: `complaints.orderId`
  - `orders` → `returns`: An order can have multiple return requests.
    - Foreign Key: `returns.orderId`

- **One-to-One**:
  - `orders` → `invoices`: An order has exactly one invoice.
    - Foreign Key: `orders.invoiceId`

#### **3. Warehouses Table**

- **One-to-Many**:
  - `warehouses` → `orders`: A warehouse can fulfill multiple orders.
    - Foreign Key: `orders.warehouseId`

#### **4. Products Table**

- **One-to-Many**:
  - `products` → `product_color`: A product can have multiple colors.
    - Foreign Key: `product_color.productId`
  - `products` → `orderItems`: A product can appear in multiple order items.
    - Foreign Key: `orderItems.productId`

#### **5. Colors Table**

- **One-to-Many**:
  - `colors` → `product_color`: A color can be associated with multiple products.
    - Foreign Key: `product_color.colorId`
  - `colors` → `orderItems`: A color can be selected for multiple order items.
    - Foreign Key: `orderItems.colorId`

#### **6. Categories Table**

- **One-to-Many**:
  - `categories` → `products`: A category can have multiple products.
    - Foreign Key: `products.categoryId`

#### **7. Product_Color Table**

- **Many-to-One**:
  - `product_color` → `products`: Each product-color combination belongs to one product.
    - Foreign Key: `product_color.productId`
  - `product_color` → `colors`: Each product-color combination belongs to one color.
    - Foreign Key: `product_color.colorId`

#### **8. Order_Items Table**

- **Many-to-One**:
  - `orderItems` → `orders`: Each order item belongs to one order.
    - Foreign Key: `orderItems.orderId`
  - `orderItems` → `products`: Each order item corresponds to one product.
    - Foreign Key: `orderItems.productId`
  - `orderItems` → `colors`: Each order item corresponds to one color.
    - Foreign Key: `orderItems.colorId`

#### **9. Deliveries Table**

- **Many-to-One**:
  - `deliveries` → `orders`: Each delivery record corresponds to one order.
    - Foreign Key: `deliveries.orderId`
  - `deliveries` → `drivers`: Each delivery is assigned to one driver.
    - Foreign Key: `deliveries.driverId`

#### **10. Drivers Table**

- **One-to-Many**:
  - `drivers` → `deliveries`: A driver can handle multiple deliveries.
    - Foreign Key: `deliveries.driverId`

#### **11. Complaints Table**

- **Many-to-One**:
  - `complaints` → `orders`: Each complaint corresponds to one order.
    - Foreign Key: `complaints.orderId`
  - `complaints` → `users`: Each complaint is filed by one user.
    - Foreign Key: `complaints.userId`
  - `complaints` → `users`: Each complaint can be resolved by one user (staff/admin).
    - Foreign Key: `complaints.resolvedBy`

#### **12. Returns Table**

- **Many-to-One**:
  - `returns` → `orders`: Each return request corresponds to one order.
    - Foreign Key: `returns.orderId`
  - `returns` → `products`: Each return request corresponds to one product.
    - Foreign Key: `returns.productId`
  - `returns` → `colors`: Each return request corresponds to one color.
    - Foreign Key: `returns.colorId`
  - `returns` → `users`: Each return request is processed by one user (staff/admin).
    - Foreign Key: `returns.processedBy`

#### **13. Service_Centers Table**

- **No Direct Relationships**:
  - This table is standalone but can be indirectly related to `returns` or `complaints` if faulty products are sent to service centers.

#### **14. Invoices Table**

- **One-to-One**:
  - `invoices` → `orders`: Each invoice corresponds to one order.
    - Foreign Key: `invoices.orderId`

---

### **Summary of Relationship Types**

| **Table**       | **Relationship Type** | **Related Table** | **Foreign Key**           |
| --------------- | --------------------- | ----------------- | ------------------------- |
| `users`         | One-to-Many           | `orders`          | `orders.userId`           |
| `users`         | One-to-Many           | `warehouses`      | `warehouses.managerId`    |
| `users`         | One-to-Many           | `drivers`         | `drivers.userId`          |
| `users`         | One-to-Many           | `complaints`      | `complaints.userId`       |
| `users`         | One-to-Many           | `returns`         | `returns.processedBy`     |
| `orders`        | One-to-Many           | `orderItems`      | `orderItems.orderId`      |
| `orders`        | One-to-Many           | `deliveries`      | `deliveries.orderId`      |
| `orders`        | One-to-Many           | `complaints`      | `complaints.orderId`      |
| `orders`        | One-to-Many           | `returns`         | `returns.orderId`         |
| `orders`        | One-to-One            | `invoices`        | `orders.invoiceId`        |
| `warehouses`    | One-to-Many           | `orders`          | `orders.warehouseId`      |
| `products`      | One-to-Many           | `product_color`   | `product_color.productId` |
| `products`      | One-to-Many           | `orderItems`      | `orderItems.productId`    |
| `colors`        | One-to-Many           | `product_color`   | `product_color.colorId`   |
| `colors`        | One-to-Many           | `orderItems`      | `orderItems.colorId`      |
| `categories`    | One-to-Many           | `products`        | `products.categoryId`     |
| `product_color` | Many-to-One           | `products`        | `product_color.productId` |
| `product_color` | Many-to-One           | `colors`          | `product_color.colorId`   |
| `orderItems`    | Many-to-One           | `orders`          | `orderItems.orderId`      |
| `orderItems`    | Many-to-One           | `products`        | `orderItems.productId`    |
| `orderItems`    | Many-to-One           | `colors`          | `orderItems.colorId`      |
| `deliveries`    | Many-to-One           | `orders`          | `deliveries.orderId`      |
| `deliveries`    | Many-to-One           | `drivers`         | `deliveries.driverId`     |
| `drivers`       | One-to-Many           | `deliveries`      | `deliveries.driverId`     |
| `complaints`    | Many-to-One           | `orders`          | `complaints.orderId`      |
| `complaints`    | Many-to-One           | `users`           | `complaints.userId`       |
| `complaints`    | Many-to-One           | `users`           | `complaints.resolvedBy`   |
| `returns`       | Many-to-One           | `orders`          | `returns.orderId`         |
| `returns`       | Many-to-One           | `products`        | `returns.productId`       |
| `returns`       | Many-to-One           | `colors`          | `returns.colorId`         |
| `returns`       | Many-to-One           | `users`           | `returns.processedBy`     |
| `invoices`      | One-to-One            | `orders`          | `invoices.orderId`        |

---
