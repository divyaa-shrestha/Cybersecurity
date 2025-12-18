# GDPR Compliance Checklist – Web-based Booking System (Phase 4)

## Personal data mapping and minimization

| Requirement | Result | Notes |
|------------|--------|-------|
| Have all personal data been identified? | ⚠️ | email and age are collected |
| Is only necessary personal data collected? | ⚠️ | Basic data only, but justification not documented |
| Is user age recorded to verify 15+ requirement? | ✅ | Age is required during registration |

## User registration and management

| Requirement | Result | Notes |
|------------|--------|-------|
| GDPR-compliant consent during registration | ❌ | No explicit consent checkbox or wording |
| Users can view/edit/delete their personal data | ⚠️ | Editing is possible, deletion process unclear |
| Admin can delete a reserver (right to be forgotten) | ✅ | Admin can remove users |
| Underage registration/booking restricted | ✅ | Users under 15 cannot book |

## Booking visibility

| Requirement | Result | Notes |
|------------|--------|-------|
| Bookings visible without login at resource level only | ✅ | No identity data shown |
| No personal data exposed publicly | ✅ | Booker identity is hidden |

## Access control and authorization

| Requirement | Result | Notes |
|------------|--------|-------|
| Only admins can manage resources and bookings | ✅ | Admin role enforced |
| Role-based access control implemented | ✅ | Reserver vs Administrator roles |
| Admin privileges limited for GDPR compliance | ⚠️ | No explicit policy restricting data misuse |

## Privacy by Design principles

| Requirement | Result | Notes |
|------------|--------|-------|
| Privacy by Default implemented | ⚠️ | Minimal data collected, defaults undocumented |
| Logs avoid unnecessary personal data | ⚠️ | Logging exists, data content unclear |
| Forms designed with data protection in mind | ✅ | Minimal fields and secured login |

## Data security

| Requirement | Result | Notes |
|------------|--------|-------|
| CSRF, XSS, SQLi protections | ⚠️ | Assumed framework-level protections |
| Passwords securely hashed | ⚠️ | Hashing assumed, algorithm not disclosed |
| Backup and recovery GDPR-compliant | ⚠️ | No visible backup policy |
| Data stored within EU | ⚠️ | Data location not specified |

## Data anonymization and pseudonymization

| Requirement | Result | Notes |
|------------|--------|-------|
| Personal data anonymized where possible | ⚠️ | Public bookings do not show identities |
| Pseudonymization used | ❌ | No evidence of pseudonymization |

## Data subject rights

| Requirement | Result | Notes |
|------------|--------|-------|
| Users can request access to their data | ❌ | No data export feature |
| Users can request deletion of data | ⚠️ | Admin deletion exists, user request unclear |
| Users can withdraw consent | ❌ | No withdrawal mechanism |

## Documentation and communication

| Requirement | Result | Notes |
|------------|--------|-------|
| Privacy policy available and accessible | ❌ | Page doesn not exists, content incomplete |
| GDPR documentation for admins/developers | ❌ | No internal documentation |
| Data breach response process documented | ❌ | No breach response procedure |
