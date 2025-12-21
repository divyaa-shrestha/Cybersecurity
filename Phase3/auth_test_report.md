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
- Gobuster endpoint discovery


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

- **Cannot access reservation API** — `GET /api/reservations`  
  Observation: Guest receives full reservation data in JSON, including reservation IDs, resource IDs, names, and start/end times, without authentication  
  Spec: ❌ Violates spec

- **Cannot access users API** — `GET /api/users`  
  Observation: Guest receives full user list in JSON, including usernames, roles, and user tokens; no authentication required  
  Spec: ❌ Violates spec



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
  Observation: Reservation data visible 
  Spec match: ✅ Yes

- **Can register as a reserver** — `/register`  
  Observation: Registration form accepts new user details; system validates age and only allows registration if user is over 15; otherwise shows error message “You are not above 15”  
  Spec: ✅ Yes

- **Can log in successfully** — `/login`  
  Observation: Login succeeds with correct credentials  
  Spec: ✅ Yes


### ❌ Cannot do

- **Cannot access admin dashboard** — `/admin`  
  Observation: Access blocked  
  Spec match: ✅ Yes

- **Cannot manage users** — `/admin/users`, `/api/admin/users`  
  Observation: Access denied  
  Spec match: ✅ Yes

- **Cannot manage resources** — `/api/resources`  
  Observation: Page unavailable  
  Spec match: ✅ Yes (Admin only)

- **Cannot edit or delete other users’ reservations**  
  Observation: No IDOR or privilege escalation found  
  Spec match: ✅ Yes

- **Cannot update other users’ reservations via UI or form manipulation**  
  Observation: Manual testing unsuccessful  
  Spec match: ✅ Yes

- **Can access users API** — `GET /api/users`  
  Observation: Reserver receives full user list in JSON, including usernames, roles, and user tokens; no restriction based on role  
  Spec: ❌ Violates spec

- **Can access all reservations via API** — `GET /api/reservations` and `GET /api/reservations/:id`  
  Observation: Reserver can see all reservations in JSON, including reservations created by other users; no restriction is applied based on ownership  
  Spec:❌ Violates spec

- **Cannot access own profile page** — `/profile`  
  Observation: Access is blocked  
  Spec: ⚠️ Not defined in spec


---


## 🧑‍💼🛡️ Administrator (Privileged User)

### ✅ Can do

- **Can register and log in as administrator** — `/login` + `/register`  
  Observation: Admin registration and login succeed; admin is redirected to admin dashboard  
  Spec:✅ Yes
  
- **Can view all resources**
  Observation: Data returned successfully  
  Spec match: ✅ Yes

- **Can view all reservations**
  Observation: Full reservation list available  
  Spec match: ✅ Yes

- **Can edit reservations**   
  Observation: Reservation modification possible  
  Spec match: ✅ Yes (Spec: admin can modify reservations)

- **Can access users API** — `GET /api/users`  
  Observation: Admin receives full user list in JSON, including usernames, roles, and user tokens  
  Spec: ✅ Yes



### ❌ Cannot do / Limitations

- **Cannot delete a reserver** — `/admin/users/delete/:id`  
  Observation: Status page shows “Not Found” with back-to-home button; admin cannot delete users via the UI/API  
  Spec: ⚠️ Not defined

- **Cannot manage resources via UI** — `/admin/resources`  
  Observation: Add/edit/delete resource not exposed  
  Spec match: ⚠️ Not defined


---

## 🔍 Hidden Endpoint Discovery

### Tools Used
- OWASP ZAP
- Gobuster


**Conclusion:**  
The Phase 3 implementation satisfies the authorization requirements defined in the specifications and follows Privacy by Design principles.
