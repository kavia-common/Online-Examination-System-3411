# Project Structure

## Overview
This project is a classic ASP.NET Web Forms application. The structure below reflects best practices and the current repository layout. Maintain this document by updating it when folders or files change.

## Solution and Projects
- OnlineExamSystem.sln
  - OnlineExamSystem (Web Application, .NET Framework 4.8)

## Current Repository Layout (key parts)
- Online-Examination-System-3411/
  - OnlineExamSystem/ (Web Forms app root)
    - Web.config
    - Web.Debug.config
    - Web.Release.config
    - CSS/bootstrap.css
    - Pages (ASPX and code-behind):
      - LoginPage.aspx (+ .cs + .designer.cs)
      - SignUpPage.aspx (+ .cs + .designer.cs)
      - Dashboard.aspx (+ .cs + .designer.cs)
      - StartExam.aspx (+ .cs + .designer.cs)
      - MCQExam.aspx (+ .cs + .designer.cs)
      - TheoryExam.aspx (+ .cs + .designer.cs)
      - ExamResult.aspx (+ .cs + .designer.cs)
      - Leaderboard.aspx (+ .cs + .designer.cs)
      - UserProfile.aspx (+ .cs + .designer.cs)
      - AdminPanel.aspx (+ .cs + .designer.cs)
      - AdminLeaderboard.aspx (+ .cs + .designer.cs)
      - AdminCourseQueue.aspx / AdminQueue.aspx (+ .cs + .designer.cs)
      - SetExam.aspx (+ .cs + .designer.cs)
      - EditExam.aspx (+ .cs + .designer.cs)
      - EditMCQ.aspx (+ .cs + .designer.cs)
      - EditTheory.aspx (+ .cs + .designer.cs)
      - MCQSet.aspx (+ .cs + .designer.cs)
      - TheorySet.aspx (+ .cs + .designer.cs)
      - ShowAns.aspx (+ .cs + .designer.cs)
      - TakenCourses.aspx (+ .cs + .designer.cs)
      - DownloadPdf.aspx (+ .cs + .designer.cs)
    - Properties/AssemblyInfo.cs
    - Images/ (static assets)
    - packages.config
    - bin/ (build output)
    - obj/ (build artifacts)
  - database-script/
    - Online-Examination-System-Databse-Script.sql
  - images/ (documentation screenshots)
  - packages/ (NuGet package content)
  - LICENSE

## Template Structure (fill in if you add new layers)
If you add new folders such as Models/, App_Code/, Services/, or Repositories/, document them here.

- App_Code/
  - Shared business logic or helper classes compiled by ASP.NET
- Models/
  - POCO classes representing entities (User, Exam, Question, Answer, Result)
- Services/
  - Business services encapsulating core workflows (ExamService, AuthService)
- Repositories/
  - Data access components using ADO.NET or Entity Framework

## TODO for Maintainers
- Verify and update the list of pages if new ones are added.
- If master pages or user controls (.master, .ascx) are introduced, create a subsection documenting them.
- If additional client-side libraries are added (e.g., newer Bootstrap, jQuery), note file paths and versions here.
