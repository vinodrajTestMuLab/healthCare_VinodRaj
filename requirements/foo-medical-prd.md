# Foo Medical — Product Requirements Document

## 1. Product Overview

**Product Name:** Foo Medical  
**Application URL:** https://foomedical.com/  
**Product Type:** Healthcare Patient Portal

Foo Medical is an open-source healthcare web application that provides patients with a simple portal for accessing their healthcare information.

The portal supports patient authentication and allows an authenticated patient to view basic health information such as laboratory results and medications.

This PRD intentionally focuses on a small set of core patient workflows suitable for browser-based verification.

---

## 2. Target User

The primary user is an authenticated patient.

For this PRD, testing is performed using a single existing Foo Medical patient account.

The patient should be able to:

- Sign in to the portal.
- View their dashboard.
- View laboratory results.
- View medication information.
- Sign out of the portal.

---

# 3. Core Functional Requirements

## 3.1 Patient Login

### Description

A patient can authenticate using their registered email address and password.

### Functional Requirements

**FR-LOGIN-01**  
The login page must provide fields for:

- Email address
- Password

**FR-LOGIN-02**  
The patient can submit the login form.

**FR-LOGIN-03**  
Valid patient credentials must successfully authenticate the patient.

**FR-LOGIN-04**  
After successful authentication, the patient must be taken to the authenticated patient portal/dashboard.

**FR-LOGIN-05**  
Invalid credentials must not authenticate the patient.

**FR-LOGIN-06**  
An appropriate authentication error must be displayed when invalid credentials are submitted.

### Acceptance Criteria

- Given valid patient credentials, login succeeds.
- After successful login, the authenticated portal is displayed.
- Given invalid credentials, login does not succeed.
- An error is shown for invalid credentials.

---

# 4. Patient Dashboard

## 4.1 View Dashboard

### Description

After authentication, the patient can access their patient dashboard.

### Functional Requirements

**FR-DASHBOARD-01**  
The dashboard must be accessible to an authenticated patient.

**FR-DASHBOARD-02**  
The dashboard must identify the logged-in patient.

**FR-DASHBOARD-03**  
The dashboard must provide access to the patient's healthcare information.

**FR-DASHBOARD-04**  
The dashboard must provide navigation to laboratory results.

**FR-DASHBOARD-05**  
The dashboard must provide access to medication information.

### Acceptance Criteria

- A successfully authenticated patient can open the dashboard.
- The dashboard identifies the logged-in patient.
- Healthcare information is displayed or accessible from the dashboard.
- Laboratory results can be accessed from the portal.
- Medication information can be accessed from the portal.

---

# 5. Laboratory Results

## 5.1 View Laboratory Results

### Description

An authenticated patient can view their laboratory results.

### Functional Requirements

**FR-LAB-01**  
The patient must be able to navigate from the authenticated portal to laboratory results.

**FR-LAB-02**  
The laboratory results page must display laboratory result information belonging to the logged-in patient.

**FR-LAB-03**  
A laboratory result should display the available result information provided by the application, such as:

- Test name
- Result value
- Unit
- Result status

**FR-LAB-04**  
The patient must be able to view the latest available laboratory result.

### Acceptance Criteria

- A logged-in patient can open the laboratory results section.
- Laboratory results are displayed.
- The displayed results belong to the authenticated patient.
- The latest available result can be viewed.
- Available result details are visible.

---

# 6. Medication Information

## 6.1 View Medications

### Description

An authenticated patient can view medication information associated with their healthcare record.

### Functional Requirements

**FR-MED-01**  
The patient must be able to access medication information from the authenticated portal.

**FR-MED-02**  
The medication page or section must display medication information available for the patient.

**FR-MED-03**  
Displayed medication information must belong to the authenticated patient.

### Acceptance Criteria

- A logged-in patient can access medication information.
- Medication information is displayed when available.
- The information belongs to the logged-in patient.

---

# 7. Patient Logout

## 7.1 Sign Out

### Description

An authenticated patient can securely sign out of the portal.

### Functional Requirements

**FR-LOGOUT-01**  
The authenticated portal must provide a logout/sign-out action.

**FR-LOGOUT-02**  
Selecting logout must end the patient's authenticated session.

**FR-LOGOUT-03**  
After logout, the patient must no longer have access to authenticated portal content without logging in again.

### Acceptance Criteria

- The patient can select the logout action.
- The authenticated session is ended.
- The patient is returned to an unauthenticated state.
- Authenticated content cannot be accessed after logout without authentication.

---

# 8. User Journey

The primary end-to-end patient journey is:

1. Open Foo Medical.
2. Enter valid patient credentials.
3. Log in.
4. Verify the patient dashboard.
5. Open laboratory results.
6. Verify laboratory result information.
7. Navigate to medication information.
8. Verify medication information.
9. Log out.
10. Verify the patient is no longer authenticated.

---

# 9. Negative Authentication Journey

A separate negative authentication scenario should verify:

1. Open Foo Medical.
2. Enter an invalid password for the patient account.
3. Submit the login form.
4. Verify that authentication fails.
5. Verify that an authentication error is displayed.
6. Verify that the patient is not granted access to authenticated content.

---

# 10. Scope

## In Scope

- Patient login
- Invalid login handling
- Patient dashboard
- Laboratory results
- Medication information
- Patient logout
- Basic authenticated-session behavior

## Out of Scope

The following Foo Medical capabilities are intentionally excluded from this PRD:

- Patient registration
- Appointment scheduling
- Provider search
- Patient-provider messaging
- Care plans
- Vaccination workflows
- Vitals workflows
- Profile editing
- Notifications
- Global search
- Advanced filtering
- API/FHIR testing
- Backend testing
- Multiple patient accounts
- Cross-patient authorization testing
- Accessibility testing
- Responsive/mobile testing
- Performance testing
- Browser compatibility testing

---

# 11. Test Data Assumptions

The application is assumed to contain an existing patient account with valid credentials.

The patient account must have sample healthcare data available for verification, including laboratory results and medication information.

No additional patient registration or test-data creation is required as part of this PRD.

The test should use the same patient account for the primary workflow.

---

# 12. Environment

**Application:** Foo Medical  
**Environment:** Hosted Foo Medical application  
**URL:** https://foomedical.com/

The application uses the Foo Medical hosted environment and its associated healthcare data.

---

# 13. Success Criteria

The Foo Medical patient portal satisfies the requirements in this PRD when:

- A valid patient can authenticate successfully.
- An invalid login attempt is rejected.
- An authenticated patient can access the dashboard.
- The patient can view laboratory results.
- The patient can view medication information.
- The patient can successfully log out.
- Authenticated content is no longer accessible after logout.

---

# 14. Demo-Focused Requirement Priority

For demonstration and automated verification, requirements should be prioritized in this order:

**Priority 1 — Critical**

- Patient login
- Patient dashboard
- Laboratory results
- Logout

**Priority 2 — High**

- Medication information
- Invalid login handling

The primary demo workflow should focus on the happy path:

**Login → Dashboard → Lab Results → Medications → Logout**

The negative authentication workflow should be demonstrated separately:

**Invalid Login → Authentication Error**
