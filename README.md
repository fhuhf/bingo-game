# Brief Development Report – THEi HR System

**Student 1:** Chu Lok Hang Thomson (250511652)  
**Student 2:** Yeung Chun Kit (250276567)

---

## 1. Introduction
The **THEi HR System** is a Java EE 8 web application designed to support HR administration. It provides functions for managing employee profiles, training enrollments, installment-based payments, and automated warning generation.

The system is built using **EJB 3.2**, **JPA 2.2**, and **JSF 2.3**, and runs on a Java EE server such as GlassFish.

---

## 2. Enterprise Session Beans

### 2.1 CrudServiceBean (Stateless)
Provides **CRUD operations** for Employees, Enrollments, Payments, and Warnings.

**Reason for Stateless:**
- No need to store client state  
- Each request is independent  
- Supports efficient pooling and scalability  

---

### 2.2 TimerServiceBean (Singleton)
Performs periodic checks using the **EJB Timer Service** to detect unpaid fees and generate warnings.

**Reason for Singleton:**
- Ensures only one instance runs  
- Prevents duplicate execution  
- Avoids race conditions  

---

## 3. Transaction Management
The system uses **Container-Managed Transactions (CMT)** to ensure consistency.

**Example: Installment Payment**
1. Insert payment record  
2. Update enrollment balance  

Both operations succeed or fail together.

---

## 4. JSF Pages and Backing Beans

- **login.xhtml (LoginController)** – User authentication  
- **index.xhtml (DashboardController)** – System overview and warnings  
- **employees.xhtml (EmployeeController)** – Manage employee data  
- **enrollment.xhtml (EnrollmentController)** – Manage training records  
- **editEnrollment.xhtml (EditEnrollmentController)** – Update course details  
- **enrollmentDetail.xhtml (EnrollmentDetailController)** – Payment and details view  

---

## 5. System Design (UML)
The system uses JPA entity relationships:

- Employee ↔ Training (many-to-many)  
- Enrollment stores fee and status  
- Payment records track installments  
- Warning records monitor unpaid cases  

**Figure 1: UML Class Diagram**

![UML Diagram](uml-diagram.png)

> Replace `uml-diagram.png` with your actual image file name.

---

## 6. Assumptions
- Single admin account is sufficient  
- Timer is shortened for demonstration  
- Currency uses standard decimal format  
- System uses Hong Kong timezone  

---

## 7. References
- Oracle Java EE 8 Documentation  
- Apache Maven Documentation  
- Oracle EJB Timer Service Guide  
