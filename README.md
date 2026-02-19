# Institution Onboarding Guide

This guide helps institutions prepare Excel files for bulk imports into Turtil CMS. All imports support `.xlsx` and `.xls` formats.

---

## Table of Contents

1. [Institution Details (manual)](#1-institution-details)
2. [Staff Import](#2-staff-import)
3. [Academic Structure Import](#3-academic-structure-import)
4. [Subjects Import](#4-subjects-import)
5. [Subject-Staff Mapping (manual)](#5-subject-staff-mapping)
6. [Student Import](#6-student-import)

---

## 1. Institution Details (manual)

Provide your institution's basic information and address details.

### Sample File

[institution-details-sample.xlsx](./institution-details-sample.xlsx)

### Column Reference

| Column | Required | Max Length | Description | Example |
|--------|----------|------------|-------------|---------|
| Institution Name | Yes | 255 characters | Full name of your institution | Your Institution Name |
| Institution Code | No | 50 characters | Short unique identifier | INST001 |
| Institution Type | Yes | - | Type of institution | College / School |
| Phone Number | No | 20 characters | Contact phone with country code | +91 9876543210 |
| Website | No | - | Institution website URL | www.example.edu.in |
| Street Address | No | 200 characters | Building/Plot address | 123, Main Road |
| City | No | 100 characters | City name | Your City |
| State / Province | No | 100 characters | State or province | Your State |
| Country | No | 100 characters | Country name | India |
| Postal Code | No | 20 characters | PIN/ZIP code | 123456 |

### Institution Type Values

- `School` - K-12 schools
- `College` - Colleges and universities

### Notes

- Institution Logo should be uploaded separately through the CMS interface
- Address fields help with location-based features and reports

---

## 2. Staff Import

Bulk invite staff members (teaching and non-teaching) to your institution.

### Sample File

[staff-import-sample.xlsx](./staff-import-sample.xlsx)

### Column Reference

| Column | Required | Description | Example |
|--------|----------|-------------|---------|
| Employee Name | Yes | Full name of the employee | John Doe |
| Email ID | Yes | Official email (institution/university emails only) | john.doe@institution.edu |
| Phone Number | No | 10 digits (no country code) | 9876543210 |
| Employee ID | No | Unique employee identifier (cannot be changed once set) | EMP001 |
| Account Level | Yes | Access level | Staff |
| Department | Yes | Department name | Computer Science |
| Employee Category | Yes | Category of employment | Teaching / Non-Teaching |
| Designation | Yes | Job title/position | Assistant Professor |

### Account Level Values

- `Admin` - Full administrative access
- `Head of Department` - Department-level management access
- `Staff` - Regular staff access

### Employee Category Values

- `Teaching` - Faculty members
- `Non-Teaching` - Administrative and support staff

### Validation Rules

1. **Email format**: Must be a valid institutional email address
2. **Phone format**: Exactly 10 digits, no spaces or special characters
3. **No duplicate emails**: Each email must be unique
4. **Employee ID**: Once set, cannot be modified

### Constraints

- **Maximum file size**: 30 MB
- **Maximum rows**: 500 staff per import

---

## 3. Academic Structure Import

Import your institution's hierarchy (departments, programs, years, sections, etc.) in bulk.

### Sample Files

| Institution Type | Sample File |
|-----------------|-------------|
| School (K-12) | [school-structure-sample.xlsx](./school-structure-sample.xlsx) |
| Engineering College | [engineering-college-sample.xlsx](./engineering-college-sample.xlsx) |
| Arts & Science College | [arts-science-college-sample.xlsx](./arts-science-college-sample.xlsx) |
| Pharmacy College | [pharmacy-college-sample.xlsx](./pharmacy-college-sample.xlsx) |

### Column Structure by Institution Type

The column structure depends on your institution type. Each row represents a leaf node (the most granular level where students are assigned).

#### School (K-12)

| Column | Required | Description | Example |
|--------|----------|-------------|---------|
| ACADEMIC YEAR | Yes | Academic session | 2025-2026 |
| GRADE | Yes | Grade/Class level | Grade 10 |
| SECTION | Yes | Section name under a grade | Section A |

**Hierarchy**: ACADEMIC YEAR → GRADE → SECTION

#### Engineering College

| Column | Required | Description | Example |
|--------|----------|-------------|---------|
| ACADEMIC YEAR | Yes | Academic session | 2025-2026 |
| BRANCH | Yes | Engineering branch/department | Computer Science |
| YEAR | Yes | Year of study | First Year |
| SEMESTER | Yes | Semester within the year | Semester 1 |

**Hierarchy**: ACADEMIC YEAR → BRANCH → YEAR → SEMESTER

#### Arts & Science College

| Column | Required | Description | Example |
|--------|----------|-------------|---------|
| ACADEMIC YEAR | Yes | Academic session | 2025-2026 |
| COURSE | Yes | Course/Program name | Bachelor of Commerce |
| YEAR | Yes | Year of study | First Year |
| SEMESTER | Yes | Semester within the year | Semester 1 |

**Hierarchy**: ACADEMIC YEAR → COURSE → YEAR → SEMESTER

#### Pharmacy College

| Column | Required | Description | Example |
|--------|----------|-------------|---------|
| ACADEMIC YEAR | Yes | Academic session | 2025-2026 |
| YEAR | Yes | Year of study | First Year |
| SEMESTER | Yes | Semester within the year | Semester 1 |

**Hierarchy**: ACADEMIC YEAR → YEAR → SEMESTER

**Programs included in sample**:
- **B.Pharm (4-Year)**: 8 semesters across 4 years
- **M.Pharm (2-Year)**: 4 semesters across 2 years

### Constraints

- **Maximum file size**: 30 MB
- **Fill columns sequentially**: Do not leave gaps between columns
- **No duplicate rows**: Each combination must be unique

---

## 4. Subjects Import

Add subjects in bulk to any academic node.

### Column Reference

| Column | Required | Max Length | Description | Example |
|--------|----------|------------|-------------|---------|
| Subject Code | Yes | 50 characters | Unique subject identifier | CS101 |
| Subject Name | Yes | 255 characters | Full subject name | Introduction to Computer Science |
| Short Form | No | 50 characters | Abbreviated name for display | Intro CS |

### Validation Rules

1. **Subject Code**: Must be unique within the academic node
2. **Subject Name**: Cannot be empty or whitespace only
3. **No duplicates**: Subject codes must not already exist in the target node

### Constraints

- **Maximum file size**: 10 MB
- **Maximum rows**: 500 subjects per import
- **Target node**: Subjects are added to a specific academic node

---

## 5. Subject-Staff Mapping (manual)

Link subjects to academic structure and assign staff members to teach each subject.

### Sample File

[subject-staff-mapping-sample.xlsx](./subject-staff-mapping-sample.xlsx)

### Column Reference

| Column | Required | Description | Example |
|--------|----------|-------------|---------|
| Year | Yes | Year of study | Year 1 |
| Semester | Yes | Semester within the year | Semester 1 |
| Section | Yes | Section name | Section A |
| Subject Code (Subject Name) | Yes | Subject code followed by name | SUB101 Subject Name 1 |
| Staff Employee ID (Staff Name) | Yes | Employee ID followed by name | EMP001 Staff Name 1 |

### Format Guidelines

- **Subject Code (Subject Name)**: Combine code and name with a space (e.g., `SUB101 Introduction to Physics`)
- **Staff Employee ID (Staff Name)**: Combine ID and name with a space (e.g., `EMP001 John Doe`)

### Validation Rules

1. **Year/Semester/Section**: Must match existing academic structure
2. **Subject Code**: Must match an existing subject code
3. **Staff Employee ID**: Must match an existing staff member

### Constraints

- **Maximum file size**: 30 MB
- **One mapping per row**: Each row assigns one staff to one subject in one section

---

## 6. Student Import

Bulk invite students along with their parent/guardian details. Each Excel file contains students for a **specific section**.

### File Naming Convention

Name your Excel file based on the target section path:

**Format**: `Academic Year-Year-Semester-Section.xlsx`

**Example**: `2025-2026-First Year-Semester 2-Section A.xlsx`

| Level | Value |
|-------|-------|
| Academic Year | 2025-2026 |
| Year | First Year |
| Semester | Semester 2 |
| Section | Section A |

Create separate Excel files for each section.

### Sample File

[student_import_sample.xlsx](./student_import_sample.xlsx)

### Column Reference

| Column | Required | Format | Description | Example |
|--------|----------|--------|-------------|---------|
| Student Name | Yes | Text | Full name of the student | John Doe |
| Student Email | Yes | Valid email | Student's email address | john@school.edu |
| Student Phone | No | 10 digits (no country code) | Student's mobile number | 9876543210 |
| Student ID | No | Text | Roll number or admission ID | STU2024001 |
| Parent Name | Yes | Text | Parent/Guardian full name | Richard Doe |
| Parent Phone | Yes | 10 digits (no country code) | Parent's mobile number | 9876543200 |
| Parent Relation | Yes | Enum (see below) | Relationship to student | Father |
| Parent Email | No | Valid email | Parent's email address | richard@email.com |

### Parent Relation Values

Only the following values are accepted (case-sensitive):

- `Father`
- `Mother`
- `Guardian`
- `Other`

### Validation Rules

1. **Email format**: Must be a valid email address (e.g., `name@domain.com`)
2. **Phone format**: Exactly 10 digits, no spaces or special characters
3. **No duplicate emails**: Each student email must be unique within the import
4. **Parent relation**: Must match one of the allowed values exactly

### Constraints

- **Maximum file size**: 30 MB
- **Maximum rows**: 1,000 students per import
- **One section per file**: Create separate Excel files for each section
