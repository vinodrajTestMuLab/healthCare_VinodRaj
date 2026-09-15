# Foo Medical — Patient Portal / EHR-Style Demo Application
## Product Requirements Document (PRD)

**Version:** 1.0  
**Product:** Foo Medical  
**Type:** Synthetic healthcare patient portal / EHR-style web application  
**Primary user:** Patient  
**Application URL:** https://foomedical.com/

---

## Application Access

Foo Medical is available as a publicly accessible healthcare demonstration application.

**Application URL:** https://foomedical.com/

## 1. Product Overview

Foo Medical is a browser-based patient portal that allows patients to securely access their healthcare information and complete common healthcare tasks online.

The product provides a unified experience for viewing medical records, laboratory results, medications, allergies, vital signs, appointments, healthcare documents, notifications, and provider messages.

The application is intended to behave like a realistic modern healthcare portal while remaining simple enough for demonstrations, development, and automated quality engineering.

The product uses synthetic patient data. No real patient or protected health information is required.

---

## 2. Product Vision

Foo Medical gives patients a single digital destination to:

- Understand their current health information.
- Review their historical healthcare records.
- Manage appointments.
- Review medications and allergies.
- Review laboratory results and vital measurements.
- Communicate with healthcare providers.
- Access healthcare documents.
- Maintain selected personal/contact information.

The portal should feel like one connected product rather than a collection of unrelated demo screens.

---

## 3. Product Goals

### Primary Goals

1. Give patients centralized access to their healthcare information.
2. Make common patient tasks easy to complete online.
3. Present healthcare information in a clear and understandable format.
4. Allow patients to schedule and manage appointments.
5. Provide secure patient-provider communication.
6. Provide a realistic healthcare data model.
7. Support desktop and mobile browser experiences.
8. Demonstrate healthcare workflows using synthetic data.

### Secondary Goals

- Support accessibility for core workflows.
- Provide consistent navigation and terminology.
- Clearly communicate loading, success, error, and empty states.
- Maintain strict separation between different patient records.
- Provide a foundation for FHIR-compatible healthcare data.

---

## 4. Target Users

### 4.1 Patient

The primary user of the product.

The patient can:

- Sign in and sign out.
- View the dashboard.
- View and edit permitted profile information.
- View medical conditions.
- View medications.
- View allergies.
- View laboratory results.
- View vital signs.
- View appointments.
- Schedule appointments.
- Cancel eligible appointments.
- View and send provider messages.
- View healthcare documents.
- View notifications.
- Search patient records.

### 4.2 Provider

Providers are represented in patient records and appointment data.

Provider-facing portal functionality is outside the initial scope.

### 4.3 Demo Administrator

An internal/demo role may seed or reset synthetic data.

Administrative functionality is outside the normal patient experience.

---

# 5. Product Navigation

The main application navigation contains:

- Dashboard
- Profile
- Medical Records
  - Conditions
  - Medications
  - Allergies
  - Laboratory Results
  - Vitals
- Appointments
- Messages
- Documents
- Notifications

The account menu contains:

- My Profile
- Settings
- Help
- Sign Out

---

# 6. Authentication

## 6.1 Login

The login screen contains:

- Foo Medical logo/name.
- Email or username field.
- Password field.
- Show/hide password control.
- Remember Me option.
- Sign In button.
- Forgot Password link.
- Help link.

### Product Behavior

When valid credentials are submitted, the user is authenticated and taken to the Dashboard.

When credentials are invalid, the portal remains on the login experience and displays an appropriate authentication error.

Authentication errors must not reveal unnecessary information about user accounts.

## 6.2 Forgot Password

The password-recovery experience contains:

1. Email/username input.
2. Continue action.
3. Confirmation screen.

The demo implementation may simulate password-reset delivery.

## 6.3 Session

An authenticated session remains active according to the configured session policy.

An inactive session may expire.

When a session expires:

- The user is returned to Login.
- The portal displays a session-expired message.
- Protected healthcare information is no longer accessible.

## 6.4 Sign Out

When the user selects Sign Out:

- The session is terminated.
- The user is returned to Login.
- Protected pages require authentication again.

---

# 7. Dashboard

The Dashboard is the default page after successful login.

## 7.1 Header

The header displays:

- Patient name.
- Greeting.
- Current date.
- Notifications indicator.
- Account menu.

Example:

> Good morning, Maya

## 7.2 Upcoming Appointment

The upcoming appointment card displays:

- Provider.
- Specialty.
- Appointment type.
- Date.
- Time.
- Location.
- Visit mode.
- Status.

The card contains a View Appointment action.

If no appointment exists, the card displays an empty state and a Schedule Appointment action.

## 7.3 Health Summary

The dashboard summarizes:

- Active conditions.
- Current medications.
- Allergies.
- Most recent vitals.

## 7.4 Recent Laboratory Results

The dashboard displays recent laboratory results with:

- Test name.
- Result.
- Unit.
- Status.
- Date.

A View All action opens the Laboratory Results page.

## 7.5 Recent Activity

Recent activity can include:

- New lab result.
- New provider message.
- Appointment confirmation.
- Appointment change.
- New document.

## 7.6 Quick Actions

Quick actions include:

- Schedule Appointment.
- View Lab Results.
- View Medications.
- Message Provider.
- View Documents.

---

# 8. Patient Profile

The Profile page shows demographic and contact information.

## 8.1 Demographic Information

Profile information includes:

- Full name.
- Preferred name.
- Date of birth.
- Gender.
- Address.
- Email.
- Phone.
- Emergency contact.
- Primary care provider.

## 8.2 Editable Information

Patients can edit:

- Email.
- Phone.
- Address.
- Emergency contact.

Clinical records such as diagnoses and laboratory results are read-only in the initial patient portal.

## 8.3 Edit Experience

When Edit is selected:

1. Current values are displayed in editable fields.
2. Patient changes permitted fields.
3. Patient selects Save.
4. Data is validated.
5. Valid changes are saved.
6. A success message is displayed.

Cancel discards unsaved changes.

---

# 9. Medical Records

The Medical Records area contains:

- Conditions.
- Medications.
- Allergies.
- Laboratory Results.
- Vitals.

All records are associated with the currently authenticated patient.

---

# 10. Conditions

The Conditions page displays current and historical medical conditions.

## 10.1 Condition List

Each condition displays:

- Condition name.
- Status.
- Onset date.
- Recorded/updated date.
- Provider.

Supported statuses:

- Active.
- Resolved.
- Inactive.

## 10.2 Condition Details

Selecting a condition displays:

- Condition name.
- Clinical status.
- Onset date.
- Recorded date.
- Provider.
- Additional notes when available.

## 10.3 Empty State

When the patient has no conditions:

> No medical conditions have been recorded.

---

# 11. Medications

The Medications page contains current and historical medication records.

## 11.1 Medication Information

Each medication contains:

- Medication name.
- Strength.
- Dosage.
- Route.
- Frequency.
- Start date.
- End date, if applicable.
- Status.
- Prescribing provider.

Supported statuses:

- Active.
- Completed.
- Discontinued.
- On Hold.

## 11.2 Medication Details

Selecting a medication opens a detail view with all available medication information and instructions.

## 11.3 Medication Search

The patient can search medications by name.

Search is case-insensitive.

When there are no matching medications, the portal displays a clear no-results message.

---

# 12. Allergies

The Allergies page shows recorded allergies.

Each allergy includes:

- Substance/allergen.
- Reaction.
- Severity.
- Status.
- Recorded date.

Severity values:

- Mild.
- Moderate.
- Severe.

Status values:

- Active.
- Inactive.
- Resolved.

Selecting an allergy displays the complete record.

When no allergies exist, the portal displays an appropriate no-records state.

---

# 13. Laboratory Results

Laboratory Results is a primary clinical-information module.

## 13.1 Result List

Each laboratory record contains:

- Test name.
- Result value.
- Unit.
- Reference range.
- Status.
- Collection date.
- Result date.
- Ordering provider.

## 13.2 Result Status

Supported statuses include:

- Normal.
- Abnormal.
- High.
- Low.
- Critical.
- Pending.

## 13.3 Result Details

Selecting a result displays:

- Test name.
- Result.
- Unit.
- Reference range.
- Interpretation/status.
- Collection date.
- Result date.
- Ordering provider.
- Additional information, if available.

## 13.4 Result History

Results are displayed with newest records first.

## 13.5 Filtering

Patients can filter results by:

- Test name.
- Date range.
- Status.

Filters may be combined.

## 13.6 Abnormal Results

Abnormal results are visually identifiable.

The design must not rely only on color to communicate abnormal status.

---

# 14. Vital Signs

The Vitals page contains historical measurements.

Supported measurements:

- Blood pressure.
- Heart rate.
- Respiratory rate.
- Temperature.
- Weight.
- Height.
- Oxygen saturation.

Each measurement contains:

- Measurement type.
- Value.
- Unit.
- Measurement date.
- Source/provider when available.

The portal may provide a historical trend view.

---

# 15. Appointments

The Appointments module allows patients to manage visits.

## 15.1 Appointment Categories

Appointments are grouped into:

- Upcoming.
- Past.
- Cancelled.

## 15.2 Appointment Information

Each appointment contains:

- Appointment ID.
- Provider.
- Specialty.
- Appointment type.
- Date.
- Start time.
- End time.
- Location.
- Visit mode.
- Status.
- Instructions.

Visit modes:

- In-person.
- Video.
- Phone.

Appointment statuses:

- Scheduled.
- Confirmed.
- Completed.
- Cancelled.
- No Show.

---

# 16. Appointment Scheduling

Patients can schedule an appointment through a guided flow.

## 16.1 Scheduling Flow

```text
Appointments
    ↓
Schedule Appointment
    ↓
Select Provider
    ↓
Select Appointment Type
    ↓
Select Date
    ↓
Select Time
    ↓
Review
    ↓
Confirm
    ↓
Confirmation
```

## 16.2 Provider Selection

Providers show:

- Name.
- Specialty.
- Location.
- Available visit modes.
- Availability.

## 16.3 Appointment Types

Initial appointment types include:

- General consultation.
- Follow-up visit.
- Annual checkup.
- Medication review.
- Lab follow-up.

## 16.4 Date Selection

The patient chooses an eligible future date.

Unavailable dates cannot be selected.

## 16.5 Time Selection

The portal displays available appointment slots.

Unavailable slots cannot be selected.

## 16.6 Review

Before confirmation, the patient reviews:

- Provider.
- Specialty.
- Appointment type.
- Date.
- Time.
- Location.
- Visit mode.

## 16.7 Confirmation

After confirmation:

- Appointment is created.
- Confirmation message appears.
- Appointment appears in Upcoming Appointments.
- Confirmation notification may be generated.

---

# 17. Appointment Cancellation

Patients may cancel eligible upcoming appointments.

## Cancellation Flow

```text
Upcoming Appointment
    ↓
Appointment Details
    ↓
Cancel Appointment
    ↓
Cancellation Confirmation
    ↓
Confirm Cancellation
```

After confirmation:

- Appointment status becomes Cancelled.
- It is no longer considered an active upcoming appointment.
- Cancellation confirmation is displayed.
- A notification may be generated.

Selecting Don't Cancel leaves the appointment unchanged.

---

# 18. Messages

The Messages module provides secure communication between patients and eligible providers.

## 18.1 Inbox

The inbox displays:

- Sender.
- Subject.
- Date/time.
- Read/unread state.

Unread messages are visually distinct.

## 18.2 Message Details

A message contains:

- Sender.
- Recipient.
- Subject.
- Message body.
- Date/time.
- Conversation history where applicable.

## 18.3 Compose

The compose experience contains:

- Recipient.
- Subject.
- Message body.
- Send button.
- Cancel button.

## 18.4 Send

A valid message is sent when Send is selected.

After successful submission:

- Confirmation is displayed.
- Conversation/history is updated.
- Sent content is visible in the appropriate view.

A message requires:

- Recipient.
- Subject.
- Body.

---

# 19. Documents

The Documents page allows patients to view healthcare documents.

Supported document examples:

- Visit summary.
- Lab report.
- Referral document.
- Discharge summary.
- Clinical note.
- Patient instructions.

Each document displays:

- Title.
- Document type.
- Date.
- Provider.
- Availability/status.

Selecting a document opens the document viewer or document display.

Patients may only access documents belonging to their account.

---

# 20. Notifications

The notification center informs patients about important activity.

Notification types include:

- Appointment reminder.
- Appointment confirmation.
- Appointment cancellation.
- New laboratory result.
- New provider message.
- New document.
- Profile update.

Each notification includes:

- Title.
- Summary.
- Date/time.
- Read/unread state.
- Related action when applicable.

Opening an unread notification marks it as read.

The unread notification count updates accordingly.

---

# 21. Global Search

A global search allows patients to search their permitted records.

Searchable areas:

- Conditions.
- Medications.
- Allergies.
- Laboratory results.
- Appointments.
- Documents.
- Messages.

Search results display:

- Record type.
- Record title/name.
- Relevant date where available.

Selecting a search result opens the corresponding record.

Search must only return records available to the authenticated patient.

---

# 22. Data Model

## Patient

```text
patientId
firstName
lastName
preferredName
dateOfBirth
gender
email
phone
address
emergencyContact
primaryProviderId
```

## Provider

```text
providerId
name
specialty
location
visitModes
```

## Condition

```text
conditionId
patientId
name
status
onsetDate
recordedDate
providerId
notes
```

## Medication

```text
medicationId
patientId
name
strength
dosage
route
frequency
status
startDate
endDate
providerId
instructions
```

## Allergy

```text
allergyId
patientId
substance
reaction
severity
status
recordedDate
```

## Observation

```text
observationId
patientId
category
testName
value
unit
referenceRange
status
effectiveDate
providerId
```

## Appointment

```text
appointmentId
patientId
providerId
appointmentType
date
startTime
endTime
location
visitMode
status
instructions
```

## Message

```text
messageId
patientId
senderId
recipientId
subject
body
createdAt
readStatus
```

## Document

```text
documentId
patientId
title
documentType
providerId
documentDate
contentReference
```

## Notification

```text
notificationId
patientId
type
title
summary
createdAt
readStatus
targetReference
```

---

# 23. Relationships Between Product Modules

The modules are interconnected.

```text
Patient
 ├── Profile
 ├── Conditions
 ├── Medications
 ├── Allergies
 ├── Laboratory Results
 ├── Vitals
 ├── Appointments
 │     └── Provider
 ├── Messages
 │     └── Provider
 ├── Documents
 │     └── Provider
 └── Notifications
```

Examples:

- A newly scheduled appointment appears in Upcoming Appointments.
- Scheduling may create an appointment confirmation notification.
- A new provider message increases the unread message count.
- A new lab result can appear in Recent Laboratory Results and Notifications.
- A profile update can create a confirmation message/notification.
- Cancelling an appointment updates the appointment status and may create a notification.

---

# 24. Healthcare Interoperability Model

Where APIs are implemented, the application may represent data using simplified FHIR-compatible concepts.

| Foo Medical Data | FHIR Concept |
|---|---|
| Patient profile | Patient |
| Medical condition | Condition |
| Medication | MedicationRequest |
| Allergy | AllergyIntolerance |
| Laboratory result | Observation |
| Vital sign | Observation |
| Appointment | Appointment |
| Provider | Practitioner |
| Clinical document | DocumentReference |
| Provider message | Communication |

The UI and API should use consistent patient and record identifiers.

---

# 25. Business Rules

### BR-001 — Protected Information

Healthcare information requires authentication.

### BR-002 — Patient Ownership

Patients can access only records belonging to their account.

### BR-003 — Future Appointment

Appointments cannot be scheduled in the past.

### BR-004 — Available Slot

Only available appointment slots can be booked.

### BR-005 — Duplicate Booking

The same patient cannot create duplicate appointments for the same provider/date/time.

### BR-006 — Cancellation

Only eligible upcoming appointments can be cancelled.

### BR-007 — Message

Messages require a recipient, subject, and body.

### BR-008 — Contact Validation

Email and phone values must use valid formats.

### BR-009 — Read-Only Clinical Data

Read-only clinical fields cannot be modified through the patient portal.

### BR-010 — Empty Data

Modules without records display a meaningful empty state.

### BR-011 — Record Dates

Healthcare records display dates consistently.

### BR-012 — Synthetic Data

All patient data in the demo environment is synthetic.

---

# 26. Empty States

Each major list/module has a deliberate empty state.

Examples:

### Appointments

> You don't have any upcoming appointments.

### Lab Results

> No laboratory results are available.

### Medications

> No medications are currently listed.

### Allergies

> No allergies have been recorded.

### Messages

> You don't have any messages.

### Documents

> No documents are currently available.

### Search

> No records match your search.

---

# 27. Error States

The product handles common operational errors.

Examples:

### Invalid Login

> The username or password is incorrect.

### Expired Session

> Your session has expired. Please sign in again.

### Appointment Slot Unavailable

> This appointment slot is no longer available. Please choose another time.

### Record Not Found

> The requested record could not be found.

### Service Failure

> We couldn't load this information right now. Please try again.

Error messages should not expose technical implementation details or sensitive patient information.

---

# 28. Loading States

Pages retrieving information asynchronously display a loading state.

Loading behavior applies to:

- Dashboard.
- Medical records.
- Laboratory results.
- Vitals.
- Appointments.
- Messages.
- Documents.
- Notifications.

The interface should prevent accidental duplicate actions while an operation is being processed.

---

# 29. Accessibility

The product should support accessible core workflows.

The following should be accessible using keyboard navigation:

- Login.
- Navigation.
- Profile editing.
- Lab-result browsing.
- Appointment scheduling.
- Appointment cancellation.
- Messaging.

Interactive elements should have meaningful accessible names.

Important status information should not depend only on color.

Dialogs and modals should provide understandable focus behavior.

---

# 30. Responsive Design

## Desktop

The portal provides a full navigation layout and multi-column dashboard where appropriate.

## Tablet

Navigation and cards adapt to the available width.

## Mobile

The portal provides a mobile-friendly navigation pattern.

Information may change from tables to stacked cards when required for readability.

Forms and appointment workflows remain usable on small screens.

---

# 31. Sample Synthetic Patient — Maya Chen

**Patient ID:** P001  
**Name:** Maya Chen  
**Date of Birth:** April 14, 1987  
**Primary Provider:** Dr. Sarah Wilson

### Conditions

- Hypertension — Active
- Seasonal allergic rhinitis — Active
- Migraine — Resolved

### Medications

- Lisinopril 10 mg — Active
- Cetirizine 10 mg — Active
- Sumatriptan 50 mg — As needed

### Allergy

- Penicillin
- Reaction: Rash
- Severity: Moderate
- Status: Active

### Laboratory Results

| Test | Result | Unit | Status |
|---|---:|---|---|
| Hemoglobin A1c | 5.7 | % | Normal |
| Total Cholesterol | 192 | mg/dL | Normal |
| LDL Cholesterol | 118 | mg/dL | Normal |

### Vital Signs

| Measurement | Value |
|---|---|
| Blood Pressure | 128/82 mmHg |
| Heart Rate | 72 bpm |
| Weight | 68 kg |

---

# 32. Sample Synthetic Patient — Daniel Brooks

**Patient ID:** P002  
**Name:** Daniel Brooks  
**Date of Birth:** September 21, 1979  
**Primary Provider:** Dr. Michael Lee

P002 is a separate synthetic patient dataset.

The presence of multiple patients allows Foo Medical to represent a realistic multi-patient healthcare environment while preserving separate patient records.

---

# 33. Sample Providers

## Dr. Sarah Wilson

- Specialty: Primary Care
- Location: Downtown Medical Center
- Visit modes: In-person, Video

## Dr. Michael Lee

- Specialty: Internal Medicine
- Location: North Medical Center
- Visit modes: In-person, Video

## Dr. Emily Carter

- Specialty: Cardiology
- Location: Downtown Medical Center
- Visit modes: In-person

---

# 34. Example Patient Experience

A typical patient session may look like:

```text
Sign In
   ↓
Dashboard
   ↓
Review upcoming appointment
   ↓
Review health summary
   ↓
Open Laboratory Results
   ↓
Filter recent results
   ↓
Review a laboratory result
   ↓
Open Medications
   ↓
Review current medication
   ↓
Open Appointments
   ↓
Schedule a future appointment
   ↓
Receive confirmation
   ↓
Open Messages
   ↓
Send provider message
   ↓
Open Documents
   ↓
Review visit summary
   ↓
Sign Out
```

---

# 35. Future Product Capabilities

Possible later versions may include:

- Prescription refill requests.
- Insurance information.
- Insurance eligibility.
- Telehealth visits.
- Health forms.
- Family/dependent access.
- Proxy access.
- Immunization records.
- Care plans.
- Provider-facing application.
- Secure file upload.
- Advanced FHIR/SMART on FHIR integration.
- Audit history.
- Localization.
- Additional healthcare specialties.

These are not part of the initial release.

---

# 36. Product Release Scope

The initial release of Foo Medical includes:

### Account

- Login.
- Logout.
- Password recovery.
- Session handling.

### Patient Information

- Profile.
- Contact information.

### Clinical Records

- Conditions.
- Medications.
- Allergies.
- Laboratory Results.
- Vitals.

### Care Management

- Appointment viewing.
- Appointment scheduling.
- Appointment cancellation.

### Communication

- Messages.
- Notifications.

### Information Access

- Documents.
- Global search.

### Experience

- Loading states.
- Empty states.
- Error states.
- Responsive behavior.
- Accessibility for core workflows.

---

# 37. Product Definition of Done

The Foo Medical product is considered ready for demonstration when:

1. A patient can authenticate successfully.
2. A patient sees a personalized dashboard.
3. Medical records are displayed using synthetic data.
4. Laboratory results and vitals can be reviewed.
5. Medications and allergies can be reviewed.
6. Appointments can be viewed and managed.
7. A patient can schedule an available appointment.
8. A patient can cancel an eligible appointment.
9. A patient can view and send messages.
10. A patient can access documents.
11. Notifications reflect relevant product activity.
12. Search works across permitted records.
13. Empty and error states are understandable.
14. Core workflows work on supported desktop and mobile layouts.
15. Patient information remains associated with the correct patient.

---

# 38. Product Context Summary

Foo Medical is a synthetic patient portal centered around a patient's relationship with their healthcare information.

The core product entities are:

```text
Patient
Provider
Condition
Medication
Allergy
Observation
Appointment
Message
Document
Notification
```

The core product capabilities are:

```text
Authenticate
   ↓
Understand health summary
   ↓
Review clinical records
   ↓
Manage appointments
   ↓
Communicate with providers
   ↓
Access documents
   ↓
Manage personal information
```

The product should provide enough realistic domain context, interconnected records, workflows, states, and business rules to represent a modern patient-facing healthcare application.

This document is the product source of truth for the initial Foo Medical demonstration application.
