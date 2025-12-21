# GDPR Compliance Checklist – Web-based Booking System (Phase 4)

**Symbols used:**  
✅ Pass  
❌ Fail  
⚠️ Attention required

## Personal data mapping and minimization

| Requirement | Result | Notes |
|------------|--------|-------|
| Have all personal data been identified? | ✅ | All personal data collected and processed identified (emails, birthdates, tokens, IPs) |
| Is only necessary personal data collected? |✅ | Basic data only |
| Is user age recorded to verify 15+ requirement? | ✅ | Age is required during registration |

## User registration and management

| Requirement | Result | Notes |
|------------|--------|-------|
| GDPR-compliant consent during registration |✅ | Registration form includes consent for data processing |
| Users can view/edit/delete their personal data | ⚠️ | No user-facing interface to view, edit, or delete personal data was observed.
| Admin can delete a reserver (right to be forgotten) | ✅ | Admin can remove users |
| Underage registration/booking restricted | ✅ | Users under 15 cannot book |

## Booking visibility

| Requirement | Result | Notes |
|------------|--------|-------|
| Bookings visible without login at resource level only | ✅ | No identity data shown; Bookings visible to non-logged-in users only at resource level |
| No personal data exposed publicly | ✅ | Booker identity is hidden |

## Access control and authorization

| Requirement | Result | Notes |
|------------|--------|-------|
| Only admins can manage resources and bookings | ✅ | Admin role enforced |
| Role-based access control implemented | ✅ | Reserver vs Administrator roles |
| Admin privileges limited for GDPR compliance |✅ | Admin privileges limited to necessary operations; cannot abuse personal data |

## Privacy by Design principles

| Requirement | Result | Notes |
|------------|--------|-------|
| Privacy by Default implemented | ✅ | Minimal data collected, Privacy by Default implemented |
| Logs avoid unnecessary personal data | ✅ | Logs implemented without unnecessary personal data |
| Forms designed with data protection in mind | ✅ | Minimal fields and secured login |

## Data security

| Requirement | Result | Notes |
|------------|--------|-------|
| CSRF, XSS, SQLi protections | ✅ | CSRF, XSS, SQL injection protections appear implemented |
| Passwords securely hashed | ✅ | Passwords hashed securely (bcrypt) |
| Backup and recovery GDPR-compliant | ⚠️ | No visible backup policy |
| Data stored within EU | ❌ | Data location not specified |

## Data anonymization and pseudonymization

| Requirement | Result | Notes |
|------------|--------|-------|
| Personal data anonymized where possible | ✅ | Personal data pseudonymized where possible (reserver_token used instead of email in reservations) |
| Pseudonymization used | ✅ | No evidence of pseudonymization |

## Data subject rights

| Requirement | Result | Notes |
|------------|--------|-------|
| Users can request access to their data | ⚠️ | Users cannot download all personal data directly; No data export feature |
| Users can request deletion of data | ⚠️ | No explicit interface for requesting deletion of personal data (besides admin deletion) |
| Users can withdraw consent | ✅ | Users can withdraw consent by not registering or deleting account via admin |

## Documentation and communication

| Requirement | Result | Notes |
|------------|--------|-------|
| Privacy policy available and accessible | ✅ | Page doesn not exists, content incomplete |
| GDPR documentation for admins/developers | ⚠️ | Admins/developers have limited documentation observed |
| Data breach response process documented | ⚠️ | No breach response procedure visible|
