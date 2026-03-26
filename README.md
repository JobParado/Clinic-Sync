## 📋 **CLINIC SYNC - Queue Management System**

### **Project Overview**
Clinic Sync is a **multi-role clinic patient queue management system** built as a Java Swing desktop application. It enables real-time patient registration, doctor assignment, queue tracking, and status management for clinic staff.

---

### **🏗️ Core Architecture**

**Main Component:** MainFrame.java - A single monolithic JFrame using CardLayout for multi-screen navigation

**Key Technologies:**
- **GUI Framework:** Java Swing (JFrame, JPanel, JTable, JComboBox)
- **Database:** MySQL with JDBC connectivity
- **Authentication:** Bcrypt password hashing (Password4j library)
- **Email:** Jakarta Mail (SMTP) for OTP verification
- **Environment Config:** dotenv for database & SMTP credentials

---

### **👥 Three User Roles**

| Role | Responsibilities |
|------|------------------|
| **Admin** | Approve/reject accounts, assign doctor specializations, view system-wide activity logs, manage feedback |
| **Receptionist** | Register patients, assign patients to doctors, manage patient queue status, add intake notes |
| **Doctor** | View assigned patients, manage patient notes, update patient status (Pending → Consulting → Finished) |

---

### **🔄 Key Features**

#### **1. Authentication & Account Management**
- Registration with email OTP verification
- Admin approval workflow (2-step: email verified + admin approved)
- Password hashing with Bcrypt
- Role-based login routing
- Password change functionality

#### **2. Patient Queue Management**
- Patient registration with intake notes
- Auto-generated queue numbers
- Doctor assignment system
- Patient status tracking (3 states: Pending/Queued, Consulting/Serving, Finished)
- Search & filter patients by name

#### **3. Real-Time Data Sync**
- **Auto-refresh mechanism:** 60-second interval (adjustable)
- Prevents database overload with busy-flag
- Separate refresh for each role's data

#### **4. Doctor Management**
- Assign medical specializations (12 types: Cardiology, ENT, etc.)
- Track patient counts per doctor
- View doctor availability

#### **5. Admin Controls**
- Account approval/rejection system
- Account deletion (non-admin only)
- Doctor specialization assignment
- Activity logging (all user actions recorded)
- Feedback/message viewing system

---

### **📊 Database Schema (Key Tables)**

```
account:
  - fullname, email, password_hash, role (Admin/Doctor/Receptionist)
  - is_approved, is_verified, otp_code
  - doctor_specialization (nullable for non-doctors)

patient:
  - patient_id (auto), fullname, gender_age, date_time
  - doctor_assigned, queue_number, status
  - recep_notes (intake notes), created_by

activity_log:
  - log_id (auto), fullname, action, date_time

feedback:
  - feedback_id (auto), fullname, message, date_time
```

---

### **🎨 UI/UX Design (5 Main Screens)**

1. **Login Page** - Username/password entry, create account button
2. **Create Account** - Registration form with role selection
3. **Email Verification** - OTP validation screen
4. **Admin Dashboard** - 5 tabs:
   - Accounts (approval/rejection)
   - Doctor Specializations
   - Patient Lists
   - Activity Logs
   - Feedbacks
5. **Receptionist Dashboard** - 2 tabs:
   - Patient Registration & Assignment
   - Patient Queue & Status
6. **Doctor Dashboard** - Patient queue list, notes, status updates
7. **Settings Page** - Common to all roles (profile, password change, feedback)

---

### **🔐 Security Features**

- **Password Storage:** Bcrypt hashing (8-16 character requirement)
- **Session Management:** Role-based access control
- **Secure OTP:** 6-digit random codes sent via email
- **Input Validation:** Regex patterns for names, emails, ages
- **SQL Prepared Statements:** Prevents SQL injection
- **Admin Protection:** Can't delete/modify admin accounts

---

### **⚙️ Business Logic Highlights**

- **Doctor Approval:** Doctors must have specialization before admin approval
- **Patient Assignment:** Only unassigned patients can be assigned to doctors
- **Auto-Refresh:** Non-blocking refresh every 60 seconds (configurable)
- **Activity Logging:** Every action (patient registration, assignments, approvals) logged
- **Search Optimization:** Smart ordering (exact match → starts-with → partial)

---

### **📁 Project Structure**

```
src/com/mycompany/clinic_system/
  ├── MainFrame.java (3700+ lines - entire application)
  └── resources/
      ├── clinic.png, doctor.png, admin.png, recep.png, etc.
nbproject/
  ├── build-impl.xml, project.properties
database_grab_files/
  └── [Grab file backups for tables]
build/
  └── [Compiled .class files]
```

---
