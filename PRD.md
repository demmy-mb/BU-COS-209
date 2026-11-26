# Product Requirements Document

## Open UMIS

| Field | Details |
| --- | --- |
| Document status | Draft for stakeholder review |
| Course context | Software Engineering / Systems Analysis & Design |
| Product | Open UMIS |
| Platforms | iOS and Android mobile app; web dashboard |
| Document owner | Open UMIS project team |
| Last updated | 25 November 2026 |

---

## 1. Overview

The university UMIS portal is the main system for academic records and course administration, but the current experience is difficult to use on a phone. Attendance is often recorded on paper, official notices are split across WhatsApp groups, and links for online classes are shared through separate channels.

Open UMIS brings important day-to-day academic tasks into a single, accessible product. Students will be able to register for courses, view their timetable and results, check in to classes, open class resources, monitor campus balances, and receive official announcements. Lecturers will have tools for attendance, course materials, and grade entry. Administrators will manage course records and target announcements to the right student groups.

The first release should focus on reliable academic workflows, clear role-based access, and useful offline access. It should complement the university's existing UMIS processes rather than replace them without confirmation from the responsible departments.

## 2. Problem Statement

Students and staff currently need to move between several tools and channels to complete common academic tasks:

- The UMIS portal is not optimized for regular mobile use.
- Physical attendance sheets can be slow to complete and difficult to reconcile.
- Announcements are distributed through informal channels that do not reliably reach the intended audience.
- Online class links and course materials may be posted in different places.
- Students cannot consistently rely on saved academic information when a network connection is unavailable.

Open UMIS should reduce this fragmentation with a mobile-first experience for students and a web experience for staff, while preserving data accuracy and university control over official records.

## 3. Goals and Success

### 3.1 Product Goals

1. Give students a straightforward way to complete core academic tasks from their phones.
2. Make attendance capture faster and easier to verify.
3. Provide one place for official announcements and course-specific resources.
4. Keep recently loaded timetable, grade, and balance information available offline.
5. Apply appropriate permissions so users can access only the information and actions assigned to their role.

### 3.2 Success Measures

The following measures are proposed for pilot evaluation. Final targets should be approved after baseline testing and confirmation with university stakeholders.

| Area | Proposed pilot measure |
| --- | --- |
| Course registration | 90% of test users can select and submit a valid course set within 2 minutes |
| Attendance | A session of up to 100 students can be started and all successful records captured within 60 seconds |
| Offline access | Saved timetable, grades, and balances appear within 1 second on agreed test devices |
| Announcement reach | Report the percentage of official pilot announcements published through Open UMIS |
| Grade entry | Lecturers can submit an approved grade sheet without unresolved validation errors |
| Reliability | Attendance and registration attempts provide a clear pending, success, or failure result |

Results should be measured using representative devices, realistic network conditions, and a documented pilot population. Success targets must not be treated as guaranteed service levels until testing and stakeholder approval are complete.

## 4. Scope

### 4.1 In Scope for the Minimum Viable Product

- Student course registration with prerequisite and credit-unit checks
- Offline viewing of the latest saved timetable and semester results
- CGPA calculation from recorded student grades
- NFC or dynamic QR attendance check-in
- Optional classroom-area validation
- Attendance summaries and exam-threshold warnings
- Campus balance and clearance information
- Course materials and online class links
- Assignment deadlines
- Targeted official announcements
- Push notifications for enabled announcements
- Lecturer attendance, course material, and grade workflows
- Administrator management of course and credit records
- Role-based access and session protection

### 4.2 Out of Scope for the MVP

- A complete replacement for the university UMIS database or academic governance system
- Replacement of the university registrar's final approval processes
- Automated biometric identity verification
- Native desktop applications
- Direct integration with every campus payment or utility provider
- Detailed financial reconciliation or payment processing
- In-app dispute resolution for grades or attendance
- Anonymous posting or student-created official announcements

Integrations, data ownership, and final approval rules must be defined with the registrar and system owners before development is treated as complete.

## 5. Target Users

### 5.1 Students

Students use the product primarily to manage and monitor their academic life. Their main tasks are:

- Register for courses
- View and download timetable information
- Check semester results and CGPA
- Check in to classes
- Open online classes and course materials
- Review campus, meal, and utility balances
- Read announcements intended for their faculty, department, or level

### 5.2 Lecturers

Lecturers use the web dashboard to manage work for their assigned courses. Their main tasks are:

- Start and close attendance sessions
- Monitor attendance for a course
- Upload course materials and links
- Record assignment deadlines
- Submit grades for review or approval according to policy

### 5.3 Administrators

Administrators maintain university records and publish official information. Their main tasks are:

- Manage courses and credit records
- Maintain student or course data supplied through approved systems
- Publish announcements to selected faculties, departments, and levels
- Review operational status and user access

## 6. User Stories

The following stories describe the MVP from the user's perspective.

### Student

- As a student, I want to register for courses so that I can submit a valid selection for approval.
- As a student, I want to see why a course was rejected so that I can correct my selection.
- As a student, I want to view my timetable and results offline so that I can continue to access them during poor connectivity.
- As a student, I want to calculate or view my CGPA so that I can understand my academic standing.
- As a student, I want to check in using NFC or QR so that attendance recording is quick.
- As a student, I want to see my attendance percentage so that I can understand whether I meet the required threshold.
- As a student, I want to see my campus balances so that I can plan expenses and check clearance status.
- As a student, I want to receive official announcements for my profile so that I do not miss important notices.

### Lecturer

- As a lecturer, I want to start an attendance session so that students can check in for the current class.
- As a lecturer, I want to monitor attendance as it is recorded so that I can identify failed or missing submissions.
- As a lecturer, I want to share course materials and class links so that students can find resources in one place.
- As a lecturer, I want to submit grades so that they can pass through the university's approval process.

### Administrator

- As an administrator, I want to maintain course and credit records so that registration rules stay current.
- As an administrator, I want to target announcements by faculty, department, and level so that notices reach the intended audience.
- As an administrator, I want to review published notices so that official communications remain consistent.

## 7. Functional Requirements

### 7.1 Authentication and Roles

1. Students, lecturers, and administrators must authenticate using an approved university identity mechanism.
2. The system must assign permissions from the user's account role and course or organizational assignments.
3. Students must not be able to view or change another student's academic records.
4. Lecturers must only manage courses assigned to them unless separately authorized.
5. Administrators must perform sensitive administrative actions through protected account permissions.
6. Session tokens must expire according to security policy and must be invalidated after logout or account changes.

Implementation of the exact identity provider and authentication flow remains subject to university technical approval.

### 7.2 Course Registration

1. The student sees available courses for the correct academic session and level.
2. The system checks course prerequisites, timetable clashes, and credit-unit limits before presenting a selection as eligible.
3. The student can save a draft selection and submit it for processing.
4. Each submission has a status of draft, pending, confirmed, or rejected.
5. A rejected selection identifies the reason, such as a missing prerequisite or an exceeded credit-unit limit.
6. The system prevents the duplicate submission of the same course in a registration attempt.
7. Final course confirmation is returned by the approved university source or workflow.
8. If submission is delayed by connectivity loss, the app clearly indicates that the request remains pending and provides a retry or sync state.

Exact rules for course selection, credit limits, and confirmation authority must come from the relevant university academic policy.

### 7.3 Timetable and Grades

1. The app downloads and caches the student's timetable for the active academic session.
2. The app downloads and caches semester results and grades from an approved source.
3. The student can view cached information without a network connection.
4. Cached information displays its most recent synchronization time.
5. The app clearly distinguishes saved cached data from newly confirmed data.
6. CGPA is calculated from the student's recorded grades and credit values using the university's approved grading rules.
7. The app does not present a calculated CGPA as official if the underlying grade source or calculation policy has not been confirmed.

### 7.4 Attendance Check-In

1. A lecturer starts an attendance session for an assigned course and class.
2. The attendance session has a start time and an agreed end time or expiry time.
3. A student can check in by scanning the lecturer's dynamic QR code or tapping a classroom NFC tag.
4. A dynamic QR code must expire after 10 seconds and must not be reused for a later session.
5. The system records the student, course, session, timestamp, and accepted check-in method.
6. A successful check-in produces clear in-app confirmation.
7. Duplicate check-ins must not create duplicate attendance records.
8. Failed check-ins must explain whether the cause was an expired code, an inactive session, location validation, or a system error.

#### Location Validation

Location validation may be enabled for a classroom session. Where enabled, the app must verify that the device is within the configured classroom area at check-in. The university must approve:

- When location validation is required
- The allowed accuracy and radius
- The fallback behavior if location permission or position accuracy is unavailable
- Whether an alternative check-in method is permitted

The first release must not use location access without clear user consent.

### 7.5 Attendance Records

1. Students can view the number of sessions attended and the total number of sessions held for each course.
2. The attendance percentage is calculated from the confirmed attendance and session totals.
3. The app warns a student before their attendance falls below the 75% exam threshold.
4. The 75% threshold must be confirmed against current university policy before the warning is enabled.
5. Lecturers can view course attendance summaries for their assigned sessions.
6. Reconciliation of a corrected, missing, or disputed attendance record is handled through an authorized workflow.

### 7.6 Campus Balances

1. The app shows the student's latest available tuition clearance status.
2. The app shows the latest available cafeteria, meal, and utility balances supplied by authorized systems.
3. The screen identifies the data source and last synchronization time.
4. The app does not imply that a balance has been updated if it is only cached data.
5. Balance values are read-only in the MVP.

### 7.7 Course Materials and Virtual Classroom Links

1. Lecturers can add or update course-specific links and materials.
2. Students only see materials for courses to which they are enrolled or otherwise authorized.
3. The app supports links to online classes, lecture slides, and assignments.
4. Assignment deadlines display the due date and course name.
5. A removed or expired link does not remain as an active resource.

### 7.8 Official Announcements

1. Administrators select one or more target audiences.
2. Supported audience fields are faculty, department, and level.
3. Only students whose approved profile matches the selected audience receive the targeted announcement.
4. Administrators can save a draft and publish or schedule an approved announcement.
5. Notifications are sent only when push notifications are enabled and the target user has opted in.
6. Students can view the latest official announcements in a chronological feed.
7. The announcement feed indicates whether a notice is currently relevant to the student.

## 8. Offline Behavior

The app should prioritize availability for data that has already been successfully synchronized.

- Timetables, semester grades, campus balances, and official announcements may be cached on the device.
- Every cached screen displays the latest saved update time.
- Offline screens work with the last approved data stored on the device.
- Offline changes are limited to clearly supported actions, such as draft course selections.
- The app queues supported submission attempts and prevents misleading success messages before confirmation is received.
- Cached academic or financial records must not be shared outside the student's authenticated device session.
- Local data is removed when the user signs out where university security policy requires it.

Specific local storage, cache expiry, and conflict-resolution rules should be documented before implementation.

## 9. Web Dashboard

The web dashboard is the staff-facing interface for lecturers and administrators. The MVP should support:

- Lecturer sign-in and course selection
- Attendance session creation and monitoring
- Course resource management
- Grade entry within authorized workflows
- Administrative course and credit record management
- Announcement targeting and publishing

The dashboard must be responsive and usable on supported desktop and laptop browsers. Mobile dashboard support is not a release requirement unless university stakeholders request it.

## 10. Non-Functional Requirements

### 10.1 Performance

- Saved timetable, grade, and balance screens should appear within 1 second on agreed offline test devices.
- The app should show a loading or pending state for network operations instead of appearing frozen.
- Attendance submission should provide a result promptly on the active network and remain recoverable after temporary failures.

The final performance targets must be validated on the supported device and network set.

### 10.2 Availability and Reliability

- The system should tolerate temporary loss of network access and synchronize recoverable actions when connectivity returns.
- Users should receive an explicit pending, successful, or failed result for submitted actions.
- Duplicate submissions should not create duplicate academic or attendance records.
- The system should retain audit information for significant record changes where required by policy.

### 10.3 Security and Privacy

- Communications with backend services must use encrypted transport.
- Authentication and authorization decisions must be enforced by the backend, not only by the interface.
- Devices must store sensitive data securely and limit access to the signed-in account.
- Logs must not expose credentials, private attendance codes, or unnecessary personal data.
- Role permissions must be reviewed before release and after material changes to workflows.
- Push notifications must not expose sensitive academic or financial details in notification previews.

### 10.4 Compatibility

- The student app will be developed for iOS and Android.
- The lecturer and administrator dashboard will run on a modern web browser.
- Supported operating-system and browser versions must be listed before implementation.
- The interface must work on common screen sizes and remain usable with large text settings.

### 10.5 Accessibility

- Text must meet agreed contrast requirements.
- Controls must have accessible names and visible focus states.
- Information must not be communicated by color alone.
- Core tasks must be usable through a screen reader or comparable assistive technology where supported by the platform.

### 10.6 Maintainability

- Integrations with UMIS and campus systems must be isolated behind documented service boundaries.
- Data models must include identifiers for synchronization status and source records where relevant.
- Configuration such as grading and attendance rules should not require application code changes where practical.

## 11. Proposed Technology

| Area | Proposed technology |
| --- | --- |
| Mobile app | React Native using Expo |
| Web dashboard | Next.js |
| Backend and real-time sync | Convex or Supabase |
| Local storage | SQLite or MMKV |

These are implementation proposals, not settled decisions. The project team should compare the options against university hosting requirements, integration needs, operational cost, offline capabilities, and team experience before selection.

## 12. Integrations and Dependencies

The final implementation depends on access to the following university systems or responsible owners:

- UMIS academic and student profile records
- Course registration rules and approval workflow
- Grade source and grading scale
- Attendance policy and course assignments
- Campus balance, tuition, meal, and utility systems
- Identity and access management
- Push notification service
- NFC and QR device support
- Official announcement approval process

Each integration requires documented ownership, authorization, data fields, update frequency, and failure behavior.

## 13. Assumptions

- The university will provide approved APIs or export mechanisms for authoritative academic data.
- The registrar or another designated authority will approve final registration and grade workflows.
- Students, lecturers, and administrators have approved university accounts.
- The project is permitted to use device NFC and camera features, subject to platform support.
- The 75% attendance threshold will be confirmed against current policy.
- Mobile app and web dashboard users can access the internet at least intermittently for synchronization.
- Stakeholders will identify supported devices and browsers before test planning.

## 14. Risks and Mitigations

| Risk | Mitigation |
| --- | --- |
| University policy differs between faculties or courses | Obtain written policy confirmation before hard-coding thresholds or rules |
| UMIS APIs are unavailable or incomplete | Define integration contracts and provide cached read behavior where supported |
| Students share or impersonate attendance codes | Use short-lived signed sessions, role checks, and duplicate prevention |
| QR or NFC is not available on every device | Support approved alternate check-in methods where policy allows |
| Location accuracy causes false failures | Make fallback and assistance flows explicit; do not block access silently |
| Outdated cached data is mistaken for current data | Show source and synchronization timestamps on all cached data |
| Pilot users enroll different types of devices | Test representative iOS and Android devices early |
| Sensitive announcements are sent to the wrong audience | Validate audience profiles and require publication review |

## 15. Release Plan

### Phase 1: Foundations

- Confirm users, roles, data owners, and academic policies
- Finalize authentication and integration architecture
- Create the core data model and access rules

### Phase 2: MVP Product

- Build student timetable, grades, registration, balance, and announcement flows
- Build the staff attendance and course dashboard
- Implement offline caching and synchronization

### Phase 3: Pilot

- Conduct usability and policy reviews
- Test with representative student and lecturer groups
- Measure the success metrics in Section 3.2
- Resolve critical security, integration, and data-accuracy issues

### Phase 4: Release Readiness

- Approve supported platforms and test environments
- Complete security, privacy, accessibility, and operational checks
- Document support and incident processes
- Publish the MVP to the approved pilot or production audience

## 16. Open Questions

The project team should obtain answers to the following questions before finalizing the MVP:

1. Which systems are authoritative for student records, course registration, grades, balances, and attendance?
2. What exact prerequisite, credit-unit, timetable, and grade rules apply?
3. Is 75% consistently the university-wide attendance threshold, or does policy vary by faculty or course?
4. Which identity provider and account enrollment process will be used?
5. Are students required to grant location permission for attendance?
6. What alternate attendance method is accepted when NFC or QR is unavailable?
7. What device operating-system and browser versions must be supported?
8. Which teams will approve announcements and grade submissions?
9. Is Supabase or Convex preferred, and what hosting and data-residency requirements apply?
10. How long should cached records remain available when they are not synchronized?
11. What are the pilot size and duration?
12. What are the reporting and audit requirements for attendance and course registration?
