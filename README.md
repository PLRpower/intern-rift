# Intern Rift - Web4All Platform

Intern Rift is a comprehensive, centralized web platform. Born from the need to streamline the internship search process, this platform bridges the gap between students seeking professional experiences and companies offering valuable opportunities. 

This project was conceived and developed to provide an intuitive, secure, and robust environment for all stakeholders involved in the internship journey.

## Context & Objectives

Finding the right internship can be a daunting process. The goal of "Intern Rift" (internally referred to as the Web4All project) is to eliminate friction by centralizing offers, company data, and student applications in one accessible portal. 

Key objectives include:
- Providing a tailored experience for three distinct user roles: Administrators, Program Coordinators (Pilotes), and Students.
- Enabling seamless management of companies and internship offers.
- Facilitating direct applications with CV and cover letter uploads.
- Offering administrative dashboards to track student progress and platform metrics.

## Technical Stack

The platform is built on a solid, modern, and highly customized technical foundation adhering strictly to OOP and PSR-12 standards:

- **Backend Logic**: PHP 8+ driven by a custom Model-View-Controller (MVC) architecture.
- **Templating Engine**: Twig, ensuring clean separation of logic and presentation.
- **Database & ORM**: MySQL integrated with Illuminate/Database (Eloquent ORM) for expressive and secure database interactions.
- **Frontend**: HTML5, CSS3, and Vanilla JavaScript, ensuring a fully responsive and accessible user interface.
- **Dependency Management**: Composer for autoloading and managing external packages.

## Architectural Overview

The application follows a strict MVC design pattern, entirely custom-built to maximize performance and maintainability.

- **Routing (`index.php`)**: Acts as the single entry point, efficiently dispatching requests to the appropriate controllers based on the URL.
- **Controllers (`src/Controllers`)**: Contain the core business logic. Dedicated controllers manage specific domains such as `OfferController`, `CompaniesController`, and `ApplicationController`.
- **Models (`src/Models`)**: Leverage Eloquent ORM to map directly to database tables. Relationships such as `BelongsTo` and `HasMany` are strictly defined here.
- **Views (`src/Views`)**: Organized into layouts, components, and pages using Twig templates, ensuring reusable and secure rendering.
- **Utils (`src/Utils`)**: Contains centralized helper classes for Authentication, Input Validation, Pagination, and Search logic.

## Key Features

### Role-Based Access Control (RBAC)
The platform dynamically adapts its interface and capabilities based on the authenticated user:
- **Administrators**: Full system oversight.
- **Program Coordinators (Pilotes)**: Can manage students, companies, and internship offers.
- **Students**: Can search for offers, manage their wishlist, and submit applications.

### Company Management
Coordinators and Admins can create, read, update, and delete (CRUD) company profiles. The system also supports a rating and evaluation mechanism, allowing stakeholders to review companies based on past internship experiences.

### Internship Offer Management
Offers are tied to specific companies and include detailed metadata (duration, remuneration, location, required skill level). The platform features a robust search engine allowing users to filter offers and companies seamlessly.

### Application & Wishlist System
Students can curate a personalized wishlist of interesting offers. When ready, they can apply directly through the platform by uploading their CV and writing a customized cover letter. The system tracks the application status ("en attente", "accepté", "refusé").

### Dashboard & Statistics
A dedicated dashboard provides real-time insights into student statuses, giving coordinators immediate visibility into how many students have secured an internship, are currently searching, or have completed their requirements.

## Database Design

The database schema is highly relational and enforced through PHP-based migrations (`database/migrations`). Key tables include:
- `users` (base authentication) linked to `admins`, `teachers` (pilotes), and `students`.
- `companies` linked to `evaluations`.
- `offers` linked to `companies`.
- `applications` acting as a pivot table linking `students` and `offers` with additional metadata (CV paths, cover letters, application status).
- `wishlists` linking `students` to their saved `offers`.

Foreign key constraints and cascade deletions are strictly implemented to guarantee data integrity.

## Security Measures

Security was a non-negotiable constraint during development. The following best practices are enforced:
- **Protection against SQL Injection**: All database queries are executed using Eloquent ORM, which inherently uses prepared statements and parameter binding.
- **Cross-Site Scripting (XSS) Prevention**: All user inputs are sanitized using a custom `InputValidator` (utilizing `htmlspecialchars`, `strip_tags`, and specific filters) before processing or rendering.
- **Role Verification**: Controller methods enforce strict role checking (`Auth::checkRole()`) before executing sensitive actions or rendering administrative views.
- **Secure File Uploads**: CV uploads are securely handled, renamed with unique identifiers (`uniqid()`), and stored safely within the server infrastructure.

## Installation & Setup

1. **Clone the repository:**
   ```bash
   git clone https://github.com/PLRPower/ProjetWeb.git
   ```
2. **Install dependencies:**
   ```bash
   composer install
   ```
3. **Database Configuration:**
   Execute the provided SQL script to create the user and database. Ensure the credentials match those configured in `database/database.php`.
4. **Run Migrations:**
   ```bash
   composer migrate
   ```
5. **Server Configuration:**
   Ensure URL rewriting is enabled on your Apache server and point the document root to the project directory.

## What Was Learned

Building Intern Rift was a profound technical journey. It demanded mastering the complexities of a custom MVC framework from scratch rather than relying on an out-of-the-box solution like Laravel or Symfony. Implementing an ORM independently, building a secure routing system, and ensuring bulletproof input validation provided deep insights into modern web application architecture, security, and the critical importance of clean, maintainable code.

---
*Created by: Martin PHILIP, Jules PLÜSS, Kylian LAMBERT, Paul THOMAS.*