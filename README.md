
# Brief Development Report – THEi HR System

**Student 1:** Chu Lok Hang Thomson (250511652)  
**Student 2:** Yeung Chun Kit (250276567)

---

## 1. Introduction
The **THEi HR System** is a Java EE 8 web application designed to support internal HR administration. The system allows administrators to manage employee profiles, training enrollments, and installment-based fee payments, while also providing automated compliance monitoring through scheduled warning generation.

The system is implemented using **EJB 3.2**, **JPA 2.2**, and **JSF 2.3**, and is deployable on a Java EE–compatible server such as **GlassFish 5**.

---

## 2. Enterprise Session Beans

### 2.1 CrudServiceBean (Stateless)
This bean provides core **CRUD operations** for Employees, Enrollments, Payments, and Warnings.

It is implemented as a **Stateless session bean** because:
- Operations are independent and request-based  
- No conversational state is required  
- Supports efficient pooling and scalability  

---

### 2.2 TimerServiceBean (Singleton)
This bean implements automated checks using the **EJB Timer Service**. It scans enrollments periodically to detect unpaid fees and generates warnings when deadlines approach.

It is implemented as a **Singleton session bean** to:
- Ensure only one instance runs  
- Prevent duplicate warnings  
- Avoid race conditions  

---

## 3. Transaction Management
The system uses **Container-Managed Transactions (CMT)** to ensure data consistency.

All update operations are executed within transactions.

**Example:**
When recording an installment payment:
1. A payment record is inserted  
2. The enrollment balance is updated  

Both actions are completed together or rolled back together if an error occurs.

---

## 4. JSF Pages and Backing Beans

### Authentication
- **login.xhtml (LoginController)**  
Validates administrator login using hashed credentials (SHA-256).

---

### Dashboard
- **index.xhtml (DashboardController)**  
Displays system overview and warning notifications.

---

### Employee Management
- **employees.xhtml (EmployeeController)**  
Supports create, update, delete operations with validation.

---

### Enrollment Management
- **enrollment.xhtml (EnrollmentController)**  
Manages training creation and employee enrollment.

- **editEnrollment.xhtml (EditEnrollmentController)**  
Allows controlled updates to training details.

---

### Enrollment Details & Payment
- **enrollmentDetail.xhtml (EnrollmentDetailController)**  
Displays participant list, payment history, and outstanding balance.  
Supports installment payment updates.

---

## 5. System Design (UML)
The system uses JPA entity relationships:

- Employees ↔ Training Programs (many-to-many via enrollment)  
- Enrollment stores fee and status  
- Payments are stored as records  
- Warnings are generated automatically  

*A UML class diagram is included to illustrate the design.*

---

## 6. Assumptions
- Single admin account is sufficient  
- Timer intervals are shortened for testing  
- Currency uses standard decimal format  
- System uses Hong Kong timezone  

---

## 7. References
- Oracle Java EE 8 Documentation  
- Apache Maven Documentation  
- Oracle EJB Timer Service Guide  
