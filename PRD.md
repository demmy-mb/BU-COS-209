# Product Requirements Document

## Open UMIS

| Field | Details |
| --- | --- |
| Document status | School-project MVP draft |
| Product type | Responsive web application prototype |
| Course context | Software Engineering / Systems Analysis & Design |
| Intended users | Students, lecturers, project demonstrators |
| Document owner | Open UMIS project team |
| Last updated | 26 November 2026 |

---

## 1. Executive Summary

Open UMIS is a student-project prototype that brings a few common academic tasks into one responsive website. A student can view a sample timetable, request course registration, check into a sample class using a QR code, and read announcements. A lecturer can start an attendance session and review its attendance list. An administrator can manage the sample course catalogue and publish announcements.

The prototype is deliberately smaller than a university information system. It will use fictional or clearly approved test data and will not make official academic, attendance, or financial decisions. Its purpose is to demonstrate useful workflows and a foundation that could be evaluated for a future pilot.

The project should be simple enough for beginner developers to complete: one web application, one relational database, a small number of roles, and no direct integrations with university systems. The design should avoid choices that make future growth unnecessarily difficult, without trying to solve production-scale concerns before the prototype is proven.

## 2. Problem Statement

Students may need to check academic information in one system, find attendance details in another, and look for class updates across separate channels. This can make routine tasks harder to find and follow.

Open UMIS will demonstrate how a single, role-aware website could make a few of those tasks clearer. The school-project version will focus on a small, testable set of workflows using sample data. It will not claim to replace the university's official UMIS or its policies.

## 3. Product Goals

1. Demonstrate a clear student, lecturer, and administrator experience in one web application.
2. Let students submit a sample course registration request and see its status.
3. Demonstrate classroom attendance using a session-specific QR code.
4. Give students one place to find a timetable and official project announcements.
5. Keep the implementation understandable to beginner developers and straightforward to test.
6. Make future production work possible through a structured data model and clear separation between the interface and data access.

## 4. Non-Goals

The school-project prototype will not:

- Replace the university's official UMIS or registrar approval process.
- Use real student records, official grades, or personal financial information.
- Display or calculate official CGPA.
- Process tuition, meal, or utility payments or balances.
- Connect to university identity, academic, finance, or attendance systems.
- Guarantee that a student is physically present because a QR code was scanned.
- Provide rotating QR codes, NFC check-in, GPS or classroom geofencing.
- Provide native iOS or Android applications.
- Support offline submissions or background synchronization.
- Claim production security, regulatory compliance, or institutional readiness.

## 5. Scope

### 5.1 Included in the School-Project MVP

- One responsive website for phone, tablet, and desktop-sized screens
- Sign-in for three roles using project test accounts
- Student dashboard with sample timetable and announcements
- Sample course catalogue and course registration requests
- Lecturer attendance session creation and attendance list
- Student QR check-in for an active session
- Administrator tools for managing sample courses and announcements
- Basic role-based access checks
- Seeded demonstration data and a documented demo flow

### 5.2 Deferred Until After the School Project

- Live integration with the university UMIS
- Real student onboarding and identity verification
- Official course approval and grade workflows
- Official academic results and CGPA calculation
- Financial balances and payment services
- Attendance corrections, disputes, appeals, and policy enforcement
- NFC and location-based attendance checks
- Push notifications
- Offline data and synchronization
- Native mobile applications
- Advanced analytics, audit exports, and high-volume load testing

## 6. Users and Permissions

### 6.1 Student

Students can:

- View their own sample timetable.
- Browse the published course catalogue.
- Submit a course registration request and view its status.
- Check in to an active attendance session by scanning its QR code.
- View their own attendance records.
- Read published announcements.

Students cannot approve their own registration, edit attendance records, manage courses, or publish official announcements.

### 6.2 Lecturer

Lecturers can:

- View only the sample courses assigned to their test account.
- Start and end an attendance session for an assigned course.
- Display the QR code for an active session.
- View the attendance list for sessions they started.
- Read announcements.

Lecturers cannot manage users, change course catalogue rules, or publish administrator announcements.

### 6.3 Administrator

The administrator can:

- Create, edit, and archive sample courses.
- Assign sample courses to lecturers.
- Review student registration requests and set them to approved or rejected.
- Publish, edit, and archive announcements.
- View sample users and overall prototype activity.

The administrator role is for project demonstration only. A production product would require more carefully separated and audited permissions.

## 7. Main User Journeys

### 7.1 Student Registration

1. The student signs in using a project test account.
2. The student opens the course catalogue.
3. The student chooses one or more available courses.
4. The system checks the simple prototype rules described in Section 8.2.
5. The student submits the selection.
6. The request appears as pending until an administrator approves or rejects it.
7. The student sees the updated status and, if rejected, a short reason.

### 7.2 Lecturer Attendance

1. The lecturer signs in and selects an assigned course.
2. The lecturer starts a session for that course.
3. The system creates a session-specific QR code.
4. Students scan the code while signed in and confirm their check-in.
5. The lecturer sees the attendance list update after refresh or a normal page update.
6. The lecturer ends the session; further check-ins are rejected.

### 7.3 Administrator Announcement

1. The administrator signs in and opens announcement management.
2. The administrator enters a title and message.
3. The administrator publishes the announcement.
4. Students can see the published announcement on their dashboard.

## 8. Functional Requirements

### 8.1 Sign-In and Role Access

1. Each demo user must sign in before accessing role-specific pages.
2. The prototype must provide at least one test account for each role.
3. The application must determine the user's role from trusted account data, not from a role value submitted by the browser.
4. Students can only view their own registration requests and attendance records.
5. Lecturers can only manage attendance for courses assigned to them.
6. Only administrators can manage courses, review registration requests, or publish announcements.
7. Signing out returns the user to the sign-in page and ends the application session.
8. A user who opens a page without the required role receives a clear access-denied message or is redirected to an appropriate page.

### 8.2 Course Catalogue and Registration

1. The catalogue shows each sample course's code, title, credit units, and assigned lecturer.
2. Archived courses cannot be selected for new requests.
3. A student can select available courses and submit one registration request for the current sample term.
4. For the prototype, the system rejects duplicate course selections and requests that exceed the project-configured credit-unit limit.
5. Course prerequisites and timetable-clash rules are excluded unless the team has time after the main flows work.
6. A submitted request has one of these statuses: pending, approved, or rejected.
7. Only an administrator can change a pending request's status.
8. When rejecting a request, the administrator enters a short reason.
9. A student can see the status and rejection reason for their own request.
10. The prototype must make clear that its course approval is a demonstration and not official university registration.

The project team should choose a simple credit limit for its fictional dataset and state it in the demo instructions. It must not present that limit as university policy.

### 8.3 Sample Timetable

1. A student can see a weekly timetable populated from sample course schedule data.
2. Each timetable entry shows course title, day, start time, end time, and room.
3. The timetable is based on the student's sample course enrolments.
4. Empty states explain when no timetable entries are available.
5. The timetable is available only while the application can reach its backend; offline access is not part of this MVP.

### 8.4 Attendance Sessions and QR Check-In

1. A lecturer can start one attendance session for an assigned course.
2. A session records its course, lecturer, start time, and active or ended status.
3. The system creates a QR code that identifies the active session.
4. A student must be signed in to check in.
5. The server verifies that the session exists and is active before recording attendance.
6. Each student can check in only once per session.
7. A student receives a clear success or failure message.
8. The lecturer can view a list of students recorded for that session.
9. Ending a session stops additional check-ins.
10. Repeated check-in attempts do not create duplicate attendance records.
11. The QR flow is a classroom demonstration only. It must not be described as proof of physical presence or as resistant to code sharing.

For the prototype, the QR code may contain a link to the check-in page with an unguessable session identifier. The backend must still check the signed-in user and session status; hiding a page or button in the browser is not access control.

### 8.5 Announcements

1. An administrator can create an announcement with a title and message.
2. An administrator can save a draft or publish an announcement.
3. Students can see published announcements in reverse chronological order.
4. Draft and archived announcements are not shown to students.
5. An announcement with a missing title or message cannot be published.
6. The MVP supports announcements for all demo students; faculty, department, and level targeting are deferred.

### 8.6 Course Administration

1. An administrator can create a sample course with a unique course code, title, credit units, lecturer, and schedule.
2. The system rejects a duplicate course code.
3. An administrator can edit course information.
4. Archiving a course prevents new registration requests and attendance sessions for that course.
5. Existing sample records remain available for the demonstration after a course is archived.

## 9. Data Requirements

The initial database should use a small relational model. Exact field names can be chosen during implementation, but the following records and relationships are needed:

| Record | Minimum information |
| --- | --- |
| User profile | Authentication user ID, display name, role |
| Course | Unique code, title, credit units, lecturer ID, archived status |
| Course schedule | Course ID, day, start time, end time, room |
| Registration request | Student ID, term, status, submitted time, reviewer ID, rejection reason |
| Registration item | Registration request ID, course ID |
| Attendance session | Course ID, lecturer ID, start time, end time, active status, session identifier |
| Attendance record | Session ID, student ID, check-in time |
| Announcement | Title, message, author ID, status, created time, published time |

Database relationships must use stable identifiers rather than display names. The project should include a small seed dataset with fictional users, courses, schedules, announcements, and registrations.

## 10. User Interface Requirements

- The application must use one consistent navigation structure, with options appropriate to the signed-in role.
- The main student tasks must be reachable from the student dashboard.
- Every page must include a visible page title and a clear way to return to the dashboard.
- Forms must label their fields and show validation errors beside the relevant field or form.
- Destructive or irreversible prototype actions must require confirmation.
- Loading, empty, success, and error states must be designed for the main workflows.
- Layouts must adapt to phone and desktop widths without requiring separate applications.
- Controls must be usable by keyboard, have visible focus, and not rely on color alone to communicate status.

## 11. Non-Functional Requirements

### 11.1 Performance and Reliability

- With the small seeded dataset and a normal development or demonstration network, the main pages should become usable within 3 seconds.
- The application must show a loading state while waiting for data.
- Failed requests must show an error and a way to retry where appropriate.
- The application must not show a registration approval or attendance check-in as successful until the backend confirms it.
- The school-project demo target is up to 10 concurrent test users. This is a test scenario, not a production capacity guarantee.

### 11.2 Security and Privacy

- Use fictional data for demonstrations. Do not enter real student grades, financial details, or sensitive identifiers.
- Enforce role and ownership checks on server-side requests and database access.
- Do not put database service-role secrets or other private credentials in browser code or source control.
- Validate submitted data on the server as well as in the interface.
- Use HTTPS for any deployed demo.
- Avoid logging passwords, session credentials, or unnecessary personal information.
- Test that a student cannot access another student's records by changing a URL or request identifier.
- The prototype has not been reviewed for production use and must not be used to make official academic decisions.

### 11.3 Accessibility

- Use readable text sizes and sufficient contrast.
- Provide labels for form controls and useful alternative text for meaningful images.
- Support keyboard navigation and visible focus indicators.
- Present status with text as well as color.

### 11.4 Maintainability

- Keep the prototype as one application with clear modules for authentication, courses, registration, attendance, and announcements.
- Keep database reads and writes out of presentation-only components where practical.
- Store schema changes as database migrations or another documented, repeatable process.
- Keep secrets and environment-specific settings in local environment configuration, not committed files.
- Document how to install, seed, run, and demonstrate the application.

## 12. Recommended Implementation

To keep the school project approachable, use one agreed stack rather than maintaining multiple alternatives:

| Area | Recommendation |
| --- | --- |
| Web application | Next.js with TypeScript |
| Database | Supabase PostgreSQL |
| Authentication | Supabase Auth with manually created project test accounts |
| Hosting | Local development first; one approved low-cost hosting service for the demo if needed |
| QR generation and scanning | A maintained QR library selected by the team and tested in target browsers |

This is a recommendation, not a requirement to use a particular vendor. The team should use tools it can understand and support. Do not add a separate mobile application, microservices, real-time infrastructure, or offline database for the school-project MVP.

The application should use a conventional web application structure and PostgreSQL foreign keys. Use database access policies and server-side authorization carefully, and test them with all three roles. Keep the service-role key exclusively on the server. If the team cannot confidently configure database row-level security, limit access through server-side routes and do not expose unrestricted database credentials to the browser.

## 13. Acceptance Criteria

The MVP is ready for its school demonstration when all of the following are true:

1. The team can install and run the application using the setup instructions.
2. A student, lecturer, and administrator can each sign in using a separate test account.
3. A student can view the sample timetable and announcements.
4. A student can submit a valid course request and see it as pending.
5. An administrator can approve or reject that request, and the student sees the updated status.
6. A lecturer can start an attendance session for an assigned course and end it.
7. A signed-in student can check in to an active session by scanning its QR code.
8. A second check-in by the same student does not create another attendance record.
9. A student cannot check in to an ended session.
10. A student cannot view another student's registration or attendance data.
11. A lecturer cannot manage a course that is not assigned to them.
12. An administrator can publish an announcement and the student can see it.
13. Invalid form submissions show understandable errors.
14. The demonstration uses fictional data and explains that the system is a prototype.

## 14. Success Measures

Evaluate the prototype with a small, documented usability test. A suggested school-project test is five classmates or representative test users completing the following tasks:

- Find the next class in the timetable.
- Submit a course request.
- Check the status of the request after an administrator decision.
- Scan a QR code and confirm attendance.
- Find the latest announcement.

Suggested success criteria:

- At least four of five testers complete the main tasks without the team taking over their device.
- Testers can identify whether a registration is pending, approved, or rejected.
- Duplicate check-in attempts are prevented in every test.
- Each role is unable to perform at least one action outside its permissions in role testing.
- The team records usability issues and demonstrates fixes for any issue that blocks a core task.

These are classroom evaluation goals, not production service-level commitments.

## 15. Risks and Mitigations

| Risk | Mitigation |
| --- | --- |
| Team attempts too many features at once | Complete sign-in, course requests, announcements, and QR attendance before optional enhancements |
| Real student data is used in the demo | Use fictional seed data and exclude sensitive data from screenshots and logs |
| Role restrictions exist only in the interface | Enforce and test permissions at server and database boundaries |
| QR codes are copied or shared | State the prototype limitation; require sign-in, active session checks, and one record per student |
| Camera scanning fails on a test device | Test early and provide a lecturer-assisted demo fallback that does not pretend to be secure |
| Database credentials are exposed | Keep privileged credentials server-side and out of source control |
| Course rules are mistaken for university policy | Label sample values as project assumptions and use only fictional course data |
| Team has limited development time | Defer timetable editing, advanced validation, real-time updates, and optional interface polish |

## 16. Suggested Project Phases

### Phase 1: Setup

- Agree on the framework and repository workflow.
- Create the database schema and fictional seed accounts.
- Build sign-in and role-aware navigation.
- Confirm each role is enforced on the server.

### Phase 2: Core Academic Demo

- Add the course catalogue and course administration.
- Add student registration requests and administrator decisions.
- Add the sample timetable and announcements.
- Test input validation and access boundaries.

### Phase 3: Attendance Demo

- Add lecturer-created attendance sessions.
- Generate and scan session QR codes.
- Prevent duplicate check-ins and reject inactive sessions.
- Test the full flow on the browsers and phones available to the team.

### Phase 4: Evaluation and Delivery

- Seed a clean demonstration dataset.
- Run the acceptance tests in Section 13.
- Conduct the usability test in Section 14.
- Fix core workflow and permission issues before adding optional features.
- Deliver setup instructions, a short user guide, and a list of known limitations.

The team should adjust the calendar to its course deadline and experience. A working end-to-end flow is more important than implementing every deferred idea.

## 17. Path from Prototype to a Licensable Product

The school-project MVP is not a licensable university product by itself. If the prototype is successful, further work should be planned and funded in deliberate stages:

### Stage A: Validate the Product

- Interview students, lecturers, registrars, IT staff, and administrators.
- Confirm which workflows are valuable and which policies vary by faculty.
- Obtain written agreement from the university system owners.
- Revisit accessibility, privacy, and data-retention requirements.

### Stage B: Build an Institutional Pilot

- Integrate with an approved identity provider and authoritative academic systems.
- Define who owns each record and which system is the source of truth.
- Add real approval, correction, and support workflows.
- Perform a security and privacy review before using personal data.
- Create backup, monitoring, incident response, and data recovery procedures.
- Run a limited pilot and load tests with an agreed number of users.

### Stage C: Prepare for Licensing

- Define service availability, support hours, onboarding, and incident responsibilities.
- Agree on hosting location, data residency, retention, and deletion requirements.
- Complete independent security testing and resolve findings.
- Establish tenant isolation if multiple universities will use the same service.
- Document service levels, pricing, implementation responsibilities, and product limitations.
- Confirm legal, procurement, accessibility, and regulatory requirements with qualified professionals.

Keep the initial codebase modular and the data model relational, but do not build multi-tenant infrastructure, microservices, or enterprise operations into the school project without a real requirement. Those decisions should be made with a university pilot customer and technical review.

## 18. Assumptions and Open Questions

For the school-project MVP, this document assumes:

- The team can create and use a hosted or local PostgreSQL database.
- The demonstration will use fictional accounts and academic data.
- One responsive website is acceptable in place of separate mobile and staff applications.
- Administrators will manually approve sample course requests.
- The timetable and course rules are sample data rather than official university policy.
- QR scanning will be tested on devices and browsers available to the team.

Questions for the project team or instructor:

1. How many developers are on the team, and what is the delivery deadline?
2. Is a responsive web application acceptable for assessment, or is a native mobile app required?
3. Does the instructor require a specific programming language, database, or hosting platform?
4. Will the demonstration be local, deployed, or both?
5. Which QR scanning devices and browsers can the team test?
6. Are there marking criteria that require any feature not included in this MVP?
