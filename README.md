# Campus Course & Records Manager (CCRM)

A comprehensive console-based Java SE application designed to manage Students, Courses, Enrollments, Grades, Transcripts, and File Utilities (import/export/backup). This project demonstrates core Java language features, OOP principles, Streams API, NIO.2, Date/Time API, interfaces, abstract classes, nested classes, enums, lambda expressions, recursion, and design patterns (Singleton & Builder).

---

## Table of Contents
- [Prerequisites](#prerequisites)
- [How to Run](#how-to-run)
- [Project Structure](#project-structure)
- [Key Features](#key-features)
- [Java Concepts Demonstrated](#java-concepts-demonstrated)
- [Java Platform Overview](#java-platform-overview)
- [Installation Guide](#installation-guide)
- [Using Eclipse IDE](#using-eclipse-ide)
- [CLI Usage Guide](#cli-usage-guide)
- [Screenshots](#screenshots)
- [License](#license)

---

## Prerequisites
- **JDK 17+** installed and available on PATH
- Basic understanding of Java programming
- Command-line familiarity (PowerShell/CMD for Windows)

---

## How to Run

### Compilation

**PowerShell:**
```powershell
mkdir out
javac -d out -encoding UTF-8 $(Get-ChildItem -Recurse src\main\java\*.java | ForEach-Object { $_.FullName })
```

**Command Prompt (CMD):**
```cmd
mkdir out
for /R %f in (src\main\java\*.java) do @set files=%files% "%f"
javac -d out -encoding UTF-8 %files%
```

### Execution
```bash
java -cp out edu.ccrm.cli.Main
```

### Enable Assertions (Optional)
```bash
java -ea -cp out edu.ccrm.cli.Main
```

---

## Project Structure

The application is organized into the following packages:

- **`edu.ccrm.cli`** – Command-line interface, menu system, and input handling
- **`edu.ccrm.domain`** – Core domain models:
  - `Person` (abstract base class)
  - `Student` and `Instructor` (inheritance)
  - `Course` (Builder pattern, nested classes)
  - `Enrollment`, `Grade` (enum), `Semester` (enum)
  - `Name` (immutable value object)
  - `Transcript` (Builder pattern)
- **`edu.ccrm.service`** – Business logic services:
  - `StudentService`, `CourseService`, `EnrollmentService`, `TranscriptService`
  - In-memory implementations
- **`edu.ccrm.io`** – File I/O operations:
  - `ImportExportService` (CSV handling)
  - `BackupService` (NIO.2 backup utilities)
- **`edu.ccrm.util`** – Utility classes:
  - Validators, Comparators (lambda expressions)
  - Recursion utilities
  - Diamond problem demonstration
- **`edu.ccrm.config`** – Configuration management:
  - `AppConfig` (Singleton)
  - `DataStore` (Singleton)

---

## Key Features

### Core Functionality
1. **Student Management** – Add, update, list, and deactivate students
2. **Course Management** – Create and manage courses with department information
3. **Enrollment System** – Enroll/unenroll students, manage credit limits
4. **Grading System** – Record marks, compute GPA, generate transcripts
5. **Import/Export** – CSV-based data import and export
6. **Backup System** – Timestamped backups with recursive directory operations
7. **Reporting** – GPA distribution, top students, course statistics

### Demo Workflow
1. AppConfig (Singleton) initializes configuration and ensures required folders exist (data/export/backup)
2. Navigate through CLI menu: Students, Courses, Enrollment/Grades, Import/Export, Backup, Reports, Exit
3. Perform enrollments, record grades, and print transcripts (demonstrating polymorphism)
4. Export data and create backups in timestamped folders using NIO.2
5. View Java platform information and system statistics

---

## Java Concepts Demonstrated

### Object-Oriented Programming (OOP)
- **Encapsulation** – Private fields with public getters/setters
- **Inheritance** – `Person` → `Student`/`Instructor`
- **Abstraction** – Abstract `Person` class with template methods
- **Polymorphism** – Base-type references, overridden `toString()` methods

### Advanced OOP Features
- **Access Modifiers** – private, protected, default, public
- **Constructors** – Use of `super` in subclass constructors
- **Immutability** – `Name` value class with final fields and defensive copying
- **Nested Classes** – Static nested `DepartmentInfo` and inner `Roster` in `Course`

### Interfaces & Functional Programming
- **Interfaces** – Service layer interfaces, functional interfaces (`Predicate`)
- **Lambda Expressions** – Comparators, stream predicates, filtering
- **Default Methods** – Diamond problem resolution with explicit overrides
- **Anonymous Inner Classes** – Callback demonstrations in CLI

### Design Patterns
- **Singleton Pattern** – `AppConfig`, `DataStore`
- **Builder Pattern** – `Course.Builder`, `Transcript.Builder`

### Enumerations
- **`Semester`** – Academic term management
- **`Grade`** – Grade levels with fields, constructors, and grade point calculations

### Exception Handling
- **Checked/Unchecked Exceptions** – try/catch/multi-catch/finally blocks
- **Custom Exceptions** – `DuplicateEnrollmentException`, `MaxCreditLimitExceededException`
- **Assertions** – Runtime invariant validation (non-null IDs, credit bounds)

### File I/O (NIO.2)
- **Path & Files API** – File operations (check/delete/copy/move)
- **Streams** – Line-by-line file processing
- **Directory Operations** – Recursive backup, directory size calculation

### Date/Time API
- **LocalDate** – Date management
- **LocalDateTime** – Timestamping for exports and backups

### Core Language Features
- **Type Casting** – Upcasting, downcasting with `instanceof` checks
- **Method Overriding & Overloading** – Demonstrated across domain models
- **Control Flow** – if/else, switch, while, do-while, for, foreach
- **Jump Controls** – break, continue, labeled break
- **Arrays** – `Arrays.sort()`, `Arrays.binarySearch()`
- **String Operations** – substring, split, join, equals, compareTo

---

## Java Platform Overview

### Evolution of Java
- **1995** – Java 1.0 (Write Once, Run Anywhere)
- **1998–2006** – Java 2 (J2SE/J2EE/J2ME), Collections Framework, Swing
- **2004** – Java 5 (Generics, Enums, Annotations)
- **2011** – Java 7 (NIO.2, Try-with-resources)
- **2014** – Java 8 (Lambda expressions, Streams API, Date/Time API)
- **2017+** – Java 9–17 (Modules, var keyword, Records, Pattern matching)
- **LTS Versions** – 8, 11, 17, 21

### Java Editions

| Edition | Purpose | Use Cases |
|---------|---------|-----------|
| **Java ME** (Micro Edition) | Embedded/mobile devices | IoT, embedded systems, constrained environments |
| **Java SE** (Standard Edition) | Desktop & CLI applications | Core APIs, desktop apps, command-line tools |
| **Java EE/Jakarta EE** (Enterprise Edition) | Enterprise server-side | Web apps, REST APIs, microservices (JPA, Servlets, CDI) |

### JDK vs JRE vs JVM

- **JVM** (Java Virtual Machine) – Runtime engine that executes Java bytecode (platform-specific)
- **JRE** (Java Runtime Environment) – JVM + standard libraries (for running applications)
- **JDK** (Java Development Kit) – JRE + development tools (javac, jar, javadoc)

**Interaction Flow:**
```
Source Code (.java) → javac (JDK) → Bytecode (.class) → JVM (JRE) → Execution
```

---

## Installation Guide

### Windows: Install & Configure Java

1. **Download JDK 17+** from:
   - Oracle: https://www.oracle.com/java/technologies/downloads/
   - Microsoft: https://docs.microsoft.com/java/
   - Adoptium: https://adoptium.net/

2. **Install JDK**
   - Run the installer
   - Note installation path (e.g., `C:\Program Files\Java\jdk-17`)

3. **Configure Environment Variables**
   - Set `JAVA_HOME` to JDK installation path
   - Add `%JAVA_HOME%\bin` to `PATH`

4. **Verify Installation**
   ```cmd
   java -version
   javac -version
   ```

---

## Using Eclipse IDE

1. **Create New Project**
   - File → New → Java Project
   - Project name: `ccrm`
   - JRE: Select JDK 17+

2. **Configure Source Folder**
   - Add `src/main/java` to Build Path
   - Configure as source folder

3. **Create Run Configuration**
   - Run → Run Configurations
   - Main class: `edu.ccrm.cli.Main`

4. **Run Application**
   - Click Run button
   - Capture screenshots for documentation

---

## CLI Usage Guide

### Quick Reference

1. **Import Data**
   - Navigate to Import/Export menu
   - Import Students and Courses from CSV

2. **Manage Students & Courses**
   - Add new records
   - List existing records
   - Update information
   - Deactivate records

3. **Enrollment Operations**
   - Enroll students in courses
   - Unenroll students
   - Record marks and grades
   - Compute GPA

4. **Generate Reports**
   - GPA distribution analysis
   - Top students ranking
   - Course statistics

5. **Backup & Export**
   - Export data to CSV
   - Create timestamped backups
   - View recursive directory size

---

## Screenshots

Include the following screenshots in the `screenshots/` folder:

- `01-java-version.png` – Output of `java -version` command
- `02-eclipse-setup.png` – Eclipse project configuration
- `03-program-running.png` – CLI menu interface
- `04-exports-backups-structure.png` – Folder structure showing exports and backups

---

## Concept Mapping

| Syllabus Topic | Implementation Location |
|----------------|------------------------|
| Encapsulation | `edu.ccrm.domain.*` (private fields + getters/setters) |
| Inheritance/Abstraction | `Person` → `Student`/`Instructor` |
| Polymorphism | Transcript printing, service interfaces |
| Singleton Pattern | `AppConfig`, `DataStore` |
| Builder Pattern | `Course.Builder`, `Transcript.Builder` |
| Enums | `Grade`, `Semester` |
| Exception Handling | `edu.ccrm.service.exceptions.*`, CLI try/catch blocks |
| NIO.2 + Streams | `edu.ccrm.io.*` (import/export/backup) |
| Recursion | `edu.ccrm.util.RecursionUtils` |
| Lambda Expressions | Service filtering, report generation |
| Arrays & Sorting | CLI report demonstrations |
| Assertions | Domain/service constructor validations |

---

## License

This is an educational sample project developed for learning purposes.

---

**Note:** This project is designed to comprehensively demonstrate Java SE concepts and best practices for academic and professional development.