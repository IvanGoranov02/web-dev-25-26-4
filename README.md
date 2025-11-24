# Student-University Management System

A full-stack web application for managing students, universities, and their relationships. Built with Angular (frontend) and Node.js/Express with TypeORM (backend).

## Project Structure

```
web-dev-25-26-4/
├── web-dev-25-26-2/          # Angular Frontend
│   ├── src/
│   │   └── app/
│   │       ├── students/      # Student management component
│   │       ├── university/    # University management component
│   │       └── services/      # API service
│   └── package.json
│
└── web-dev-25-26-3/           # Node.js Backend
    ├── src/
    │   ├── config/            # Database configuration
    │   ├── entities/          # TypeORM entity schemas
    │   ├── routes/            # Express route handlers
    │   └── server.js          # Main server file
    └── package.json
```

## Features

### Current Implementation

- **Students Management**
  - Create, Read, Update, Delete students
  - Link students to universities
  - Display student information with university details

- **Universities Management**
  - Create, Read, Update, Delete universities
  - View all universities with their locations

### Backend API Endpoints

#### Students
- `POST /api/students` - Create a new student
- `GET /api/students` - Get all students
- `GET /api/students/:id` - Get a student by ID
- `PUT /api/students/:id` - Update a student
- `DELETE /api/students/:id` - Delete a student

#### Universities
- `POST /api/universities` - Create a new university
- `GET /api/universities` - Get all universities
- `GET /api/universities/:id` - Get a university by ID
- `PUT /api/universities/:id` - Update a university
- `DELETE /api/universities/:id` - Delete a university

## Getting Started

### Prerequisites

- Node.js (v14 or higher)
- npm or yarn
- Angular CLI (for frontend development)

### Backend Setup

1. Navigate to the backend directory:
```bash
cd web-dev-25-26-3
```

2. Install dependencies:
```bash
npm install
```

3. Start the server:
```bash
npm start
```

The backend server will run on `http://localhost:3000`

### Frontend Setup

1. Navigate to the frontend directory:
```bash
cd web-dev-25-26-2
```

2. Install dependencies:
```bash
npm install
```

3. Start the development server:
```bash
npm start
```

The frontend application will run on `http://localhost:4200`

## Technology Stack

### Backend
- **Node.js** - Runtime environment
- **Express.js** - Web framework
- **TypeORM** - ORM for database operations
- **SQLite** - Database

### Frontend
- **Angular 20** - Frontend framework
- **PrimeNG** - UI component library
- **RxJS** - Reactive programming
- **TypeScript** - Programming language

## Database Schema

### Students Table
- `id` (Integer, Primary Key, Auto-generated)
- `facultyNumber` (Varchar, Unique, Required)
- `firstName` (Varchar, Required)
- `middleName` (Varchar, Optional)
- `lastName` (Varchar, Required)
- `universityId` (Foreign Key to Universities)

### Universities Table
- `id` (Integer, Primary Key, Auto-generated)
- `name` (Varchar, Required)
- `location` (Varchar, Required)

## Student Tasks

### Task: Implement Student Subjects Feature

Your task is to implement a complete CRUD system for student subjects. This will involve both backend and frontend work.

#### Requirements

1. **Create a Subject Entity** (Backend)
   - Subject should have: `id`, `name`, `code` (unique), `credits`
   - Establish a many-to-many relationship between Students and Subjects
   - Create a join table for the relationship

2. **Create Subject Routes** (Backend)
   - Implement all CRUD operations (POST, GET, GET/:id, PUT, DELETE)
   - Follow the same pattern as existing student and university routes

3. **Create Subject API Service** (Frontend)
   - Add methods to interact with the subject endpoints
   - Follow the existing API service pattern

4. **Create Subject Component** (Frontend)
   - Create a new route `/subjects`
   - Implement form for creating/editing subjects
   - Display subjects in a table
   - Add edit and delete functionality

5. **Update Student Component** (Frontend)
   - Add ability to assign subjects to students
   - Display subjects for each student

#### Guidelines

See the detailed implementation guide in the [STUDENT_TASKS.md](./STUDENT_TASKS.md) file.

#### Skeleton Files Created

The following skeleton files have been created to help you get started:

**Backend:**
- `web-dev-25-26-3/src/entities/Subject.js` - Subject entity skeleton
- `web-dev-25-26-3/src/routes/subjectRoutes.js` - Subject routes skeleton

**Frontend:**
- `web-dev-25-26-2/src/app/services/api.service.ts` - Subject methods (TODO comments)
- Component files to be created by students

#### Steps to Complete

1. **Backend Implementation:**
   - Complete the Subject entity definition
   - Implement all route handlers in `subjectRoutes.js`
   - Register the routes in `server.js`
   - Update `database.js` to include the Subject entity

2. **Frontend Implementation:**
   - Complete the API service methods for subjects
   - Create the Subject component (similar to University component)
   - Add routing for `/subjects`
   - Update Student component to show/manage subjects

3. **Testing:**
   - Test all CRUD operations
   - Verify relationships work correctly
   - Test the frontend integration

## Development Guidelines

### Code Style
- Follow existing code patterns and structure
- Use consistent naming conventions
- Add error handling for all API calls
- Include validation for user inputs

### Best Practices
- Keep components focused and single-purpose
- Use TypeScript types/interfaces
- Handle loading and error states
- Provide user feedback for all actions

## Contributing

This is a learning project. Follow the existing patterns and structure when adding new features.

## License

Educational purposes only.

