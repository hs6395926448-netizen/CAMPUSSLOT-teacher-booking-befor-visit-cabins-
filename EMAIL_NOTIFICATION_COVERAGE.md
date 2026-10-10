# CampusSlot Email Notification Coverage

The notification flow covers these lifecycle events:

- Student registration submitted, approved, rejected
- Teacher registration submitted, approved, rejected
- Appointment booking request (pending)
- Appointment confirmed
- Appointment cancelled or booking rejected
- Appointment completed
- Appointment date/time rescheduled/updated

Appointment emails are sent to both the student's registered email and the teacher's registered email (deduplicated if addresses match). Status changes are queued through the background notification dispatcher so the status-update response stays fast. Delivery failures are written to Render logs and notification logs where available.

## Deploy
Merge these files into the current project and push to the existing GitHub repository. Keep `DATABASE_URL`, `APPS_SCRIPT_URL`, `APPS_SCRIPT_SECRET`, and `BASE_URL` unchanged. After deployment, test a new booking and each status action, then inspect Render logs for `CampusSlot EMAIL SENT`, `CampusSlot EMAIL FAILED`, and `CampusSlot EMAIL RESULT`.

This does not retroactively send emails for past events; notifications occur on new actions after deployment.
