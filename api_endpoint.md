#### **Role Permissions**
| **Role**      | **Permissions**                                                                 |
|---------------|---------------------------------------------------------------------------------|
| **Admin**     | Full access to all endpoints (create users, manage warehouses, drivers, etc.).  |
| **Staff**     | Manage orders, complaints, returns, deliveries, and service centers.            |
| **Customer**  | Place orders, file complaints, request returns, track deliveries.               |
| **Business**  | Place bulk orders, track deliveries, manage invoices.                          |
| **Driver**    | View assigned deliveries, update delivery status.                              |

---

### **2. API Endpoints**

#### **User Management**
- **Signup**
  - `POST /api/auth/signup`  
    - **Access**: Public (for `customer` and `business` roles only).  
    - **Description**: Allows customers and businesses to sign up themselves.  
    - **Request Body**: `{ name, email, password, phone, address, role }`.  

  - `POST /api/users/create`  
    - **Access**: Admin-only.  
    - **Description**: Admin creates staff or manager accounts.  
    - **Request Body**: `{ name, email, password, phone, address, role }`.

- **Login**
  - `POST /api/auth/login`  
    - **Access**: Public.  
    - **Description**: Authenticate users and return a JWT token.  
    - **Request Body**: `{ email, password }`.

- **Get User Profile**
  - `GET /api/users/me`  
    - **Access**: Authenticated users.  
    - **Description**: Fetch the logged-in user's profile.  

- **Update User Profile**
  - `PUT /api/users/me`  
    - **Access**: Authenticated users.  
    - **Description**: Update the logged-in user's details.  
    - **Request Body**: `{ name, phone, address }`.

---

#### **Order Management**
- **Create Order**
  - `POST /api/orders`  
    - **Access**: `customer`, `business`.  
    - **Description**: Create a new order.  
    - **Request Body**: `{ warehouseId, deliveryAddress, items: [{ productId, colorId, quantity }] }`.

- **Get Orders**
  - `GET /api/orders`  
    - **Access**: `customer`, `business` (only their orders), `staff`, `admin`.  
    - **Description**: Fetch all orders (filtered by user or globally for staff/admin).

- **Update Order Status**
  - `PUT /api/orders/:id/status`  
    - **Access**: `staff`, `admin`.  
    - **Description**: Update the status of an order (e.g., `pending`, `shipped`, `delivered`).  
    - **Request Body**: `{ status }`.

- **Cancel Order**
  - `DELETE /api/orders/:id`  
    - **Access**: `customer`, `business` (only their orders), `staff`, `admin`.  
    - **Description**: Cancel an order.

---

#### **Warehouse Management**
- **Create Warehouse**
  - `POST /api/warehouses`  
    - **Access**: `admin`.  
    - **Description**: Create a new warehouse.  
    - **Request Body**: `{ name, address, region, contact, managerId }`.

- **Get Warehouses**
  - `GET /api/warehouses`  
    - **Access**: `staff`, `admin`.  
    - **Description**: Fetch all warehouses.

- **Update Warehouse**
  - `PUT /api/warehouses/:id`  
    - **Access**: `admin`.  
    - **Description**: Update warehouse details.  
    - **Request Body**: `{ name, address, region, contact, managerId }`.

- **Delete Warehouse**
  - `DELETE /api/warehouses/:id`  
    - **Access**: `admin`.  
    - **Description**: Delete a warehouse.

---

#### **Driver Management**
- **Create Driver**
  - `POST /api/drivers`  
    - **Access**: `admin`.  
    - **Description**: Create a new driver.  
    - **Request Body**: `{ userId, licenseNumber, vehiclePlateNumber, preferredRoutes }`.

- **Get Drivers**
  - `GET /api/drivers`  
    - **Access**: `staff`, `admin`.  
    - **Description**: Fetch all drivers.

- **Update Driver**
  - `PUT /api/drivers/:id`  
    - **Access**: `admin`.  
    - **Description**: Update driver details.  
    - **Request Body**: `{ licenseNumber, vehiclePlateNumber, isActive, preferredRoutes }`.

- **Delete Driver**
  - `DELETE /api/drivers/:id`  
    - **Access**: `admin`.  
    - **Description**: Delete a driver.

---

#### **Delivery Management**
- **Assign Driver**
  - `POST /api/deliveries/assign`  
    - **Access**: `staff`, `admin`.  
    - **Description**: Assign a driver to a delivery.  
    - **Request Body**: `{ orderId, driverId, deliveryRoute }`.

- **Update Delivery Status**
  - `PUT /api/deliveries/:id/status`  
    - **Access**: `driver`, `staff`, `admin`.  
    - **Description**: Update the status of a delivery (e.g., `in_transit`, `delivered`).  
    - **Request Body**: `{ status }`.

- **Track Delivery**
  - `GET /api/deliveries/:id`  
    - **Access**: `customer`, `business`, `staff`, `admin`.  
    - **Description**: Track the status of a specific delivery.

---

#### **Complaints Management**
- **File Complaint**
  - `POST /api/complaints`  
    - **Access**: `customer`, `business`.  
    - **Description**: File a complaint about an order.  
    - **Request Body**: `{ orderId, issue }`.

- **Resolve Complaint**
  - `PUT /api/complaints/:id/resolve`  
    - **Access**: `staff`, `admin`.  
    - **Description**: Mark a complaint as resolved.  
    - **Request Body**: `{ resolvedBy }`.

---

#### **Returns Management**
- **Request Return**
  - `POST /api/returns`  
    - **Access**: `customer`, `business`.  
    - **Description**: Request a return for a faulty/wrong product.  
    - **Request Body**: `{ orderId, productId, colorId, reason }`.

- **Process Return**
  - `PUT /api/returns/:id/process`  
    - **Access**: `staff`, `admin`.  
    - **Description**: Mark a return as processed.  
    - **Request Body**: `{ processedBy }`.

---

#### **Service Centers**
- **Register Service Center**
  - `POST /api/service-centers`  
    - **Access**: `admin`.  
    - **Description**: Register a new service center.  
    - **Request Body**: `{ name, address, contact, region, brandSpecialization }`.

- **Get Service Centers**
  - `GET /api/service-centers`  
    - **Access**: `staff`, `admin`.  
    - **Description**: Fetch all service centers.

---
