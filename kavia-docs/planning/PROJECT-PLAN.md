# Project Planning

## Project Charter
- Purpose: Deliver a production-ready Online Examination System enabling MCQ and theory exams with administrative management and results.
- Scope: As defined in BRD/PRD (user management, exam creation/delivery, queues, results/leaderboards).
- Constraints: Web Forms on .NET Framework 4.8, SQL Server.
- Success Measures: Functional coverage, performance SLAs, security hardening, and stakeholder acceptance.

## Work Breakdown Structure (WBS)
1. Inception and Requirements
   - Stakeholder alignment, BRD/PRD/SRS finalization
2. Architecture and Design
   - HLD/LLD, UML, DB schema validation
3. Infrastructure Setup
   - IIS site, SQL Server database creation, Web.config connectionStrings
4. Authentication and Registration
   - SignUp, Login, session handling, password hashing
5. Exam Authoring (Admin)
   - MCQ and Theory question management, exam setup
6. Student Exam Flows
   - Dashboard/StartExam, MCQExam, TheoryExam, timers
7. Results and Leaderboards
   - ExamResult, Leaderboard, PDF export
8. Queue Management and Evaluation
   - theoryAns processing, theoryQueue/AdminCourseQueue UIs
9. Non-functional
   - Performance tuning, parameterized SQL, validation, logging
10. Testing
    - Unit/Integration tests, UAT
11. Deployment
    - Staging and production rollout, handover

## Schedule and Milestones (Indicative)
- Week 1: Requirements & Architecture sign-off
- Week 2: Infra setup; Auth/Registration
- Week 3: Admin authoring (MCQ/Theory)
- Week 4: Student exam flows (MCQ/Timers)
- Week 5: Theory flows and queues
- Week 6: Results/Leaderboard + PDF
- Week 7: NFR hardening (security/performance), testing
- Week 8: UAT and deployment

## Risks, Impact, and Mitigation
- SQL Injection via concatenation (High): Adopt parameterized queries and input validation.
- Timer inaccuracies (Medium): Use server-side time comparisons and disable reliance on client clocks.
- Session null exceptions (Medium): Defensive checks and centralized session utility.
- Performance under load (Medium): Indexing, connection pooling, caching course lists.
- Admin authentication (Medium): Replace hardcoded admin with secure role-based auth.
- File uploads security (Medium): Enforce content-type/size checks and store outside web root or use GUID filenames.

## Resource Plan
- Roles: Product Manager, Tech Lead, 2-3 Developers, QA, DevOps/Infra.
- Environments: Dev, Staging, Production.

## Acceptance Plan
- Feature acceptance based on PRD acceptance criteria.
- NFR verification via load tests and security reviews.

## References
- All design and requirements documents; database script; Web.config/project files.
