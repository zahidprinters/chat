# Finalized Main Decision Document: Store Management System for Sheikh Plastic Industries (SPI)

## 1. Project Overview
**Goal**:  
To create a scalable, user-friendly store management system that streamlines inventory, order processing, and reporting for SPI, ensuring operational efficiency, reduced errors, and actionable insights.

---

## 2. Features and Requirements
### Core Features
**User Management**:
- Secure authentication (MFA, password reset).
- Role-based access control (Admin, Manager, Staff).
- Audit logs and security alerts.

**Inventory Management**:
- Real-time stock tracking with **unit of measurement (UoM) conversions** (e.g., kg ↔ grams, liters ↔ milliliters).
- Low-stock alerts and supplier integration.
- Manual product search (no barcodes) with autocomplete and CSV bulk operations.

**Order Processing**:
- Order creation/status tracking (pending, completed).
- Email/SMS notifications and return management.

**Reporting**:
- Customizable reports (CSV/PDF) and real-time dashboards.
- Sales analytics and predictive forecasting.

---

## 3. Architecture & Technology Stack
- **Frontend**: HTML/CSS, JavaScript, Bootstrap.
- **Backend**: PHP, Laravel.
- **Database**: MySQL.
- **Server**: XAMPP (dev), AWS/DigitalOcean (prod).

---

## 4. Software Requirements
- **Development**: VS Code, Git, Docker, Composer.
- **Testing**: PHPUnit, Postman.

---

## 5. Project Structure
```plaintext
/spidatabas
├── css/
├── js/
├── php/
├── assets/
├── views/
├── routes/
├── models/
├── tests/
└── database/

---

## 6. Database Structure
**Tables**:
- **users**: `id, username, password, role, email, ...`
- **products**: `id, name, unit_id (FK), category_id, ...`
- **inventory**: `id, product_id (FK), quantity, stock_threshold, ...`
- **units**: `id, name (e.g., "Kilogram"), abbreviation (e.g., "kg")`
- **product_unit_conversions**: `product_id (FK), from_unit_id (FK), to_unit_id (FK), conversion_factor`
- **orders**, **suppliers**, **logs**, **notifications**, etc.

---

## 7. Key Exclusions
- **Removed Features**: Barcode scanning, QR code labels, batch/expiry tracking.
- **Rationale**: Simplified workflows to reduce complexity and maintenance.

---

## 8. Next Steps
1. Implement UoM conversion UI (unit dropdowns, CSV templates).
2. Update inventory/order forms to support unit selection.
3. Write user guides for UoM management and reporting.
4. Conduct staff training on unit conversions and manual product search.

---

## 9. Notes
- **Validation**: Ensure units are compatible (e.g., no kg → liters).
- **Performance**: Optimize database indexing for unit conversions.
- **Backups**: Daily database backups to AWS S3.

---

## 10. Recent Updates
- Added unit of measurement (UoM) conversion logic.
- Removed barcode, QR code, and batch tracking features.
- Finalized database schema and inventory workflows.

---

**Document Version**: 1.0  
**Approved By**: [SPI Management/Stakeholder Name]  
**Date**: [Insert Date]

---

This document reflects all finalized decisions, ensuring alignment with SPI’s operational needs. Let me know if further adjustments are required! 🚀
