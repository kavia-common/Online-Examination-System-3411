# Business Requirements Document (BRD)

## Executive Summary
The Online Examination System (OES) enables institutions to administer multiple choice (MCQ) and theory examinations online. It digitizes exam creation, delivery, submission, grading, and result publishing to reduce administrative burden, increase exam integrity, and provide timely feedback.

## Business Goals and Objectives
- Digitize examination workflows to reduce paper, time, and operational costs.
- Enable scalable delivery of MCQ and theory exams to students across courses and semesters.
- Provide transparent results and leaderboards to improve student engagement.
- Equip teachers/admins with efficient tooling to create, manage, and evaluate exams and answers.
- Improve data quality and integrity through centralized storage and access controls.

## Problem Statement
Traditional paper-based or ad-hoc exam processes are error-prone, slow, and resource-heavy. There is a need for a platform to streamline end-to-end exam management with proper auditability and timely insights.

## Scope
### In Scope
- Student registration and authentication.
- Admin/teacher login to manage exams and questions.
- MCQ exam delivery with timers and automated marking.
- Theory exam delivery with timers, answer submission, and evaluation queue.
- Leaderboards and result display for students and admins.
- SQL Server–backed data storage and retrieval.
- Deployment on IIS with ASP.NET Web Forms.

### Out of Scope
- Proctoring features (webcam monitoring, cheating detection).
- Advanced analytics, AI-based grading, or plagiarism detection.
- Multi-tenant segmentation for multiple independent institutions.
- Native mobile applications.

## Stakeholders
- Students: Participate in exams, view results, and leaderboards.
- Teachers/Admins: Create and manage exams, evaluate theory answers, publish results.
- Department/Program Heads: Oversee exam operations and compliance.
- IT/Operations: Deploy, maintain, and secure the platform.
- Compliance/Audit: Ensure data security and privacy policies are followed.

## Expected Benefits and KPIs
- Reduced time-to-publish results (target: >50% faster).
- Reduced paper and administrative overhead (target: >60%).
- Increased student satisfaction via timely feedback (survey-based KPI).
- Improved data accuracy and consistency in exam records.

## Assumptions
- Users have access to web browsers and stable internet connections.
- Institution provides SQL Server and IIS hosting.
- Departments define courses, semesters, and policies off-platform.

## Constraints
- Technology stack anchored to .NET Framework 4.8 and ASP.NET Web Forms.
- Bootstrap-based styling within traditional server-rendered pages.
- Database schema aligns with provided SQL script.

## High-Level Success Criteria
- Successful administration of MCQ and theory exams across multiple courses/semesters.
- Secure authentication, session management, and data protection.
- Timely generation of leaderboards and results with acceptable performance.

## References
- Source: Web.config, OnlineExamSystem.csproj, LoginPage.aspx.cs, SignUpPage.aspx.cs, StartExam.aspx.cs, MCQExam.aspx.cs, TheoryExam.aspx.cs, ExamResult.aspx.cs, AdminCourseQueue.aspx.cs, AdminQueue.aspx.cs, Leaderboard.aspx.cs, database SQL script, repository README.md.
