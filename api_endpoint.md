

### **API Endpoints**

#### **1. Authentication**
- **POST `/auth/signup`**  
  - Allows `customer` and `business` roles to sign up themselves.
  - Admin can create `staff` and `manager` accounts.
  - Example Payload:
    ```json
    {
      "name": "John Doe",
      "email": "john.doe@example.com",
      "password": "securepassword",
      "role": "customer"
    }
    ```
  - **Access**: Public (for `customer` and `business`), Admin-only for `staff` and `manager`.

- **POST `/auth/login`**  
  - Allows users to log in and receive a JWT token.
  - Example Payload:
    ```json
    {
      "email": "john.doe@example.com",
      "password": "securepassword"
    }
    ```
  - **Access**: Public.

---

#### **2. Users Management**
- **GET `/users/me`**  
  - Fetches the current user's details.
  - **Access**: Authenticated users (`customer`, `business`, `staff`, `driver`, `admin`).

- **PUT `/users/me`**  
  - Updates the current user's details (e.g., name, address, phone).
  - **Access**: Authenticated users (`customer`, `business`, `staff`, `driver`, `admin`).

- **GET `/users/:id`**  
  - Fetches details of a specific user.
  - **Access**: Admin only.

- **PUT `/users/:id`**  
  - Updates details of a specific user.
  - **Access**: Admin only.

- **DELETE `/users/:id`**  
  - Deletes a specific user.
  - **Access**: Admin only.

---

#### **3. Orders**
- **POST `/orders`**  
  - Creates a new order.
  - Example Payload:
    ```json
    {
      "userId": "user-id",
      "warehouseId": "warehouse-id",
      "deliveryAddress": "Yangon, Myanmar",
      "items": [
        {
          "productId": "product-id",
          "colorId": "color-id",
          "quantity": 2
        }
      ]
    }
    ```
  - **Access**: `customer`, `business`.

- **GET `/orders`**  
  - Fetches all orders (paginated).
  - **Access**: `staff`, `admin`.

- **GET `/orders/me`**  
  - Fetches orders placed by the current user.
  - **Access**: `customer`, `business`.

- **GET `/orders/:id`**  
  - Fetches details of a specific order.
  - **Access**: `customer`, `business`, `staff`, `admin`.

- **PUT `/orders/:id`**  
  - Updates the status of an order (e.g., cancel, process).
  - **Access**: `staff`, `admin`.

---

#### **4. Deliveries**
- **GET `/deliveries`**  
  - Fetches all deliveries (paginated).
  - **Access**: `staff`, `admin`.

- **GET `/deliveries/me`**  
  - Fetches deliveries assigned to the current driver.
  - **Access**: `driver`.

- **POST `/deliveries`**  
  - Assigns a delivery to a driver.
  - Example Payload:
    ```json
    {
      "orderId": "order-id",
      "driverId": "driver-id",
      "deliveryRoute": "Yangon > Mandalay"
    }
    ```
  - **Access**: `staff`, `admin`.

- **PUT `/deliveries/:id`**  
  - Updates the status of a delivery (e.g., in transit, delivered).
  - **Access**: `driver`, `staff`, `admin`.

---

#### **5. Complaints**
- **POST `/complaints`**  
  - Files a new complaint.
  - Example Payload:
    ```json
    {
      "orderId": "order-id",
      "issue": "Wrong product delivered."
    }
    ```
  - **Access**: `customer`, `business`.

- **GET `/complaints`**  
  - Fetches all complaints (paginated).
  - **Access**: `staff`, `admin`.

- **GET `/complaints/me`**  
  - Fetches complaints filed by the current user.
  - **Access**: `customer`, `business`.

- **PUT `/complaints/:id`**  
  - Resolves or escalates a complaint.
  - **Access**: `staff`, `admin`.

---

#### **6. Returns**
- **POST `/returns`**  
  - Requests a return.
  - Example Payload:
    ```json
    {
      "orderId": "order-id",
      "productId": "product-id",
      "colorId": "color-id",
      "reason": "Product is faulty."
    }
    ```
  - **Access**: `customer`, `business`.

- **GET `/returns`**  
  - Fetches all returns (paginated).
  - **Access**: `staff`, `admin`.

- **GET `/returns/me`**  
  - Fetches returns requested by the current user.
  - **Access**: `customer`, `business`.

- **PUT `/returns/:id`**  
  - Processes or rejects a return.
  - **Access**: `staff`, `admin`.

---

#### **7. Warehouses**
- **GET `/warehouses`**  
  - Fetches all warehouses (paginated).
  - **Access**: `staff`, `admin`.

- **POST `/warehouses`**  
  - Creates a new warehouse.
  - **Access**: `admin`.

- **PUT `/warehouses/:id`**  
  - Updates details of a specific warehouse.
  - **Access**: `admin`.

- **DELETE `/warehouses/:id`**  
  - Deletes a specific warehouse.
  - **Access**: `admin`.

---

#### **8. Products**
- **GET `/products`**  
  - Fetches all products (paginated).
  - **Access**: Public.

- **POST `/products`**  
  - Creates a new product.
  - **Access**: `admin`.

- **PUT `/products/:id`**  
  - Updates details of a specific product.
  - **Access**: `admin`.

- **DELETE `/products/:id`**  
  - Deletes a specific product.
  - **Access**: `admin`.

---

#### **9. Service Centers**
- **GET `/service-centers`**  
  - Fetches all service centers (paginated).
  - **Access**: Public OR Admin, Staff, Manager.

- **POST `/service-centers`**  
  - Registers a new service center.
  - **Access**: `admin`.

- **PUT `/service-centers/:id`**  
  - Updates details of a specific service center.
  - **Access**: `admin`.

- **DELETE `/service-centers/:id`**  
  - Deletes a specific service center.
  - **Access**: `admin`.

---
