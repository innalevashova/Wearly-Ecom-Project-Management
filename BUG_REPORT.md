# Bug Report: User Authentication Blocked During Sign-In

* **Component:** Authentication / Sign-In Flow
* **Environment:** Production (great-wearly-shop.vercel.app)
* **Severity:** Medium (Blocks verified/unverified user entry)
* **Reporter:** Inna Levashova, Project Manager

---

## Description
When a user attempts to log in with valid credentials, the system blocks the authentication attempt and displays a combined error message: 
*"Could not sign in. Check email and password, or complete email verification first."*

The current system implementation lacks clear error differentiation. The UI does not specify whether the failure is caused by an incorrect password or an unverified email address, leading to a confusing user experience (UX).

---

## Steps to Reproduce
1. Navigate to the Wearly landing page.
2. Click on the User Profile icon to open the Login modal.
3. Enter registered email (`innalevashova14@gmail.com`) and password.
4. Click the **"Log In"** button.

## Expected Result
* Scenario A (Wrong Credentials): The system should explicitly state: *"Invalid email or password."*
* Scenario B (Unverified Email): The system should explicitly state: *"Your email is not verified yet."* and provide a link: *"Resend verification link"*.

## Actual Result
The system throws a generic, non-specific error banner covering both potential root causes.

---

## Root Cause Analysis (PM Note)
* During verification, no verification email was received in the inbox, Spam, or Promotions folders. 
* Potential Root Causes: 
  1. Automated email dispatch (SMTP server configuration) is broken or missing on the backend.
  2. The user registration logic fails to trigger the activation token creation database-side.

---

## Action Items for the Development Team

### For Backend Developer (Python / Django)
* Verify if the SMTP backend setting (e.g., SendGrid, Mailgun, or Gmail SMTP) is correctly configured in `settings.py`.
* Check Celery logs to ensure the asynchronous email task is being triggered and executed without errors.
* Separate API error codes for `INVALID_CREDENTIALS` and `EMAIL_NOT_VERIFIED`.

### For Frontend Developer (Next.js / RTK Query)
* Implement a conditional check for backend error responses to display distinct messages.
* Prepare a "Resend Verification Email" button component for future implementation.
