# Authorization Testing Report — Phase 3  
**Booking System**

## Scope

This document contains authorization testing results for Phase 3 of the Booking System.  
The goal was to verify **role-based access control** for:

- Guest (unauthenticated)
- Reserver (authenticated user)
- Administrator (privileged user)

Testing was performed using:

- Manual browser testing
- URL manipulation
- OWASP ZAP active scanning
- Gobuster / wfuzz endpoint discovery


---

## 🧑‍🦲 Guest (Unauthenticated User)

### ✅ Can do

- **Can access login page** — `/login`  
  Observation: Login form loads correctly  
  Spec match: ✅ Yes

- **Can access registration page** — `/register`  
  Observation: Registration form available  
  Spec match: ✅ Yes

- **Can view public resources** — `/api/resources`  
  Observation: Resource list returned without authentication  
  Spec match: ✅ Yes

- **Can view reservations without identity data** — `/api/reservations`  
  Observation: Reservations visible, no reserver identity shown  
  Spec match: ✅ Yes (Spec 8)

### ❌ Cannot do

- **Cannot access reservation creation page** — `/reservation`  
  Observation: Access denied / redirected  
  Spec match: ✅ Yes

- **Cannot create reservations via API** — `POST /api/reservations`  
  Observation: Request rejected  
  Spec match: ✅ Yes

- **Cannot access profile page** — `/profile`  
  Observation: Page not accessible  
  Spec match: ✅ Yes

- **Cannot access admin pages** — `/admin`, `/admin/users`, `/admin/resources`  
  Observation: Pages not found or blocked  
  Spec match: ✅ Yes

### Notes
- No protected content is accessible as Guest
- GDPR requirement met: no personal data exposure

---

## 🧑‍💼 Reserver (Authenticated User)

### ✅ Can do

- **Can create a reservation** — `/reservation` + `POST /api/reservations`  
  Observation: Reservation created successfully  
  Spec match: ✅ Yes

- **Can view available resources** — `/api/resources`  
  Observation: Data returned correctly  
  Spec match: ✅ Yes

- **Can view reservations** — `/api/reservations`  
  Observation: Reservation data visible without user identities  
  Spec match: ✅ Yes

### ❌ Cannot do

- **Cannot access admin dashboard** — `/admin`  
  Observation: Access blocked  
  Spec match: ✅ Yes

- **Cannot manage users** — `/admin/users`, `/api/admin/users`  
  Observation: Access denied  
  Spec match: ✅ Yes

- **Cannot manage resources** — `/admin/resources`  
  Observation: Page unavailable  
  Spec match: ✅ Yes (Admin only)

- **Cannot edit or delete other users’ reservations**  
  Observation: No IDOR or privilege escalation found  
  Spec match: ✅ Yes

- **Cannot escalate privileges via URL or form manipulation**  
  Observation: Manual testing unsuccessful  
  Spec match: ✅ Yes

### Notes
- Reserver role is correctly limited to booking functionality
- No admin capabilities exposed

---

## 🧑‍💼🛡️ Administrator (Privileged User)

### ✅ Can do

- **Can view all resources**
  Observation: Data returned successfully  
  Spec match: ✅ Yes

- **Can view all reservations**
  Observation: Full reservation list available  
  Spec match: ✅ Yes

- **Can edit reservations**   
  Observation: Reservation modification possible  
  Spec match: ✅ Yes (Spec: admin can modify reservations)

### ❌ Cannot do / Limitations

- **Cannot manage users via UI** — `/admin/users`  
  Observation: UI not implemented in Phase 3  
  Spec match: ⚠️ Partially (spec allows, implementation missing)

- **Cannot manage resources via UI** — `/admin/resources`  
  Observation: Add/edit/delete resource not exposed  
  Spec match: ⚠️ Partially implemented

### Notes
- Administrator has backend authority to modify reservations
- Other admin features are intentionally not exposed, reducing attack surface
- No unnecessary privilege exposure detected

---

## 🔍 Hidden Endpoint Discovery

### Tools Used
- OWASP ZAP
- Gobuster

### Results

- No undocumented pages or endpoints discovered
- No authorization bypasses found
- No IDOR vulnerabilities detected
- All discovered endpoints were already known

---

## 🧪 ZAP Testing Summary

- Target: `http://localhost:8003`
- Discovered endpoints:
  - `/login`
  - `/register`
  - `/reservation`
  - `/api/resources`
  - `/api/reservations`
- Alerts:
  - Informational only (headers, session handling)
- No authorization-related vulnerabilities found

---

## ✅ Final Assessment

- Guests cannot access protected content
- Reservers cannot perform administrative actions
- Administrators can edit reservations but are not overexposed
- No hidden endpoints, IDORs, or authorization bypasses found
- Backend authorization is correctly enforced

**Conclusion:**  
The Phase 3 implementation satisfies the authorization requirements defined in the specifications and follows Privacy by Design principles.
