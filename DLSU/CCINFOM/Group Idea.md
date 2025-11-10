
Ah nice 🔥 that’s a **unique angle** — focusing on a **meat supplier database for samgyupsal restaurants**.  
This sits in between _food processing_ and _restaurant management_, but more niche and specialized. It’s perfect because:

- Samgyupsal restaurants rely on **high-volume meat supply** (pork, beef, chicken).
    
- Supply chain & quality control are critical.
    
- Restaurants often order in bulk and track **cuts, marinades, packaging, and expiry**.
    
- There’s also **traceability** — where the meat came from, which batch went to which restaurant.
    

---

## 🥩 Database Scope: Meat Supplier for Samgyupsal

### 1. **Suppliers & Farms**

- Manage farms/ranches that provide meat.
    
- Track health certificates, delivery schedules, and quality checks.
    

**Tables:**

- `Farms` → FarmID, Name, Location, Contact, CertificationStatus
    
- `MeatSuppliers` → SupplierID, FarmID, Name, Contact, LicenseNumber
    
- `HealthCertifications` → CertID, SupplierID, Type, IssuedDate, ExpiryDate
    

---

### 2. **Meat Inventory & Processing**

- Track cuts (belly, shoulder, ribs, brisket, etc.), marinated vs plain, and packaging.
    
- Manage perishable items with expiry tracking.
    

**Tables:**

- `MeatCuts` → CutID, Name (Pork Belly, Beef Brisket, Chicken Thigh), Category
    
- `Inventory` → InventoryID, CutID, SupplierID, QuantityKg, DateReceived, ExpiryDate, StorageLocation
    
- `Marinades` → MarinadeID, Name, Ingredients, ShelfLifeDays
    
- `ProcessedMeats` → ProcessID, CutID, MarinadeID, BatchID, QuantityKg
    

---

### 3. **Orders & Distribution**

- Restaurants order in bulk, supplier delivers.
    
- Need to track restaurant branches, delivery schedules, and order fulfillment.
    

**Tables:**

- `Restaurants` → RestaurantID, Name, BranchLocation, Contact, FranchiseOwner
    
- `Orders` → OrderID, RestaurantID, OrderDate, Status (Pending/Delivered)
    
- `OrderDetails` → OrderID, ProcessID (or CutID), QuantityKg, PricePerKg
    
- `Deliveries` → DeliveryID, OrderID, TruckID, DepartureDate, ArrivalDate, Status
    

---

### 4. **Logistics & Storage**

- Cold chain management for transporting meat.
    
- Refrigerated trucks, warehouse freezers, etc.
    

**Tables:**

- `Trucks` → TruckID, PlateNumber, CapacityKg, HasFreezer (Y/N)
    
- `Warehouses` → WarehouseID, Location, CapacityKg, TemperatureControl
    
- `StockMovements` → MovementID, InventoryID, FromWarehouse, ToRestaurant, Date, QuantityKg
    

---

### 5. **Traceability & Compliance**

- Important in case of **food safety audits or recalls**.
    
- Track which supplier → which batch → which restaurant.
    

**Tables:**

- `MeatBatches` → BatchID, SupplierID, CutID, DateProcessed, ExpiryDate, InspectionStatus
    
- `BatchDistribution` → BatchID, RestaurantID, DeliveryID
    
- `Recalls` → RecallID, BatchID, Reason, RecallDate, Status
    

---

⚡ With this, you get a **large and realistic database model** that connects:

- Farms → Supplier → Processing → Restaurants → Customers.
    
- Perfect for a **capstone-style project** since it covers supply chain, food safety, and business ops.
    

---

👉 Do you want me to **sketch a full ER diagram** for this samgyupsal meat supplier database so your group has a visual model, or should I give you the **SQL schema scripts** first?