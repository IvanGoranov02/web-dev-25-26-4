# Student Tasks: Implementing Student Subjects Feature

## Overview

Your task is to implement a complete feature for managing student subjects. This involves creating a many-to-many relationship between Students and Subjects, where:
- A student can enroll in multiple subjects
- A subject can be taken by multiple students
- Each enrollment can have additional information (e.g., grade, enrollment date)

## Part 1: Backend Implementation

### Step 1: Create Subject Entity

**File:** `web-dev-25-26-3/src/entities/Subject.js`

You need to complete the Subject entity. The skeleton has been created for you. Here's what you need to implement:

```javascript
const EntitySchema = require("typeorm").EntitySchema;

module.exports = new EntitySchema({
  name: "Subject",
  tableName: "subjects",
  columns: {
    id: {
      // TODO: Define as primary key, integer, auto-generated
    },
    name: {
      // TODO: Define as varchar, required
    },
    code: {
      // TODO: Define as varchar, required, unique
      // Example: "CS101", "MATH201"
    },
    credits: {
      // TODO: Define as integer, required
      // Example: 3, 4, 6
    },
  },
  relations: {
    students: {
      // TODO: Define many-to-many relationship with Student
      // Use type: "many-to-many"
      // Create a join table (e.g., "student_subjects")
      // Set inverseSide to the relation name in Student entity
    },
  },
});
```

**Reference:** Look at `Student.js` and `University.js` to understand the pattern.

### Step 2: Update Student Entity

**File:** `web-dev-25-26-3/src/entities/Student.js`

Add a many-to-many relationship to subjects:

```javascript
relations: {
  university: {
    // ... existing code
  },
  subjects: {
    // TODO: Add many-to-many relationship with Subject
    // This is the inverse side of the relationship
  },
}
```

### Step 3: Update Database Configuration

**File:** `web-dev-25-26-3/src/config/database.js`

Add the Subject entity to the entities array:

```javascript
const Subject = require("../entities/Subject");

const AppDataSource = new DataSource({
  // ... existing config
  entities: [University, Student, Subject], // Add Subject here
});
```

### Step 4: Create Subject Routes

**File:** `web-dev-25-26-3/src/routes/subjectRoutes.js`

The skeleton has been created. You need to implement:

1. **POST /** - Create a new subject
   - Validate: name, code, credits are required
   - Check if code is unique
   - Return created subject

2. **GET /** - Get all subjects
   - Optionally include students relation
   - Return array of subjects

3. **GET /:id** - Get subject by ID
   - Include students relation
   - Return 404 if not found

4. **PUT /:id** - Update subject
   - Validate subject exists
   - Update provided fields
   - Return updated subject

5. **DELETE /:id** - Delete subject
   - Validate subject exists
   - Return 204 on success

**Reference:** Look at `studentRoutes.js` and `universityRoutes.js` for patterns.

### Step 5: Register Routes in Server

**File:** `web-dev-25-26-3/src/server.js`

Add the subject routes:

```javascript
const subjectRoutes = require("./routes/subjectRoutes");

// Add this line with other route registrations
app.use("/api/subjects", subjectRoutes);
```

Update the root endpoint to include subject endpoints in the documentation.

### Step 6: Create Student-Subject Relationship Routes (Optional Enhancement)

You may want to create additional endpoints for managing the relationship:

- `POST /api/students/:studentId/subjects/:subjectId` - Enroll student in subject
- `DELETE /api/students/:studentId/subjects/:subjectId` - Unenroll student from subject
- `GET /api/students/:studentId/subjects` - Get all subjects for a student

## Part 2: Frontend Implementation

### Step 1: Update API Service

**File:** `web-dev-25-26-2/src/app/services/api.service.ts`

Add the Subject interface and methods:

```typescript
export interface Subject {
  id?: number;
  name: string;
  code: string;
  credits: number;
  students?: Student[]; // Optional, for when relation is loaded
}

// Add these methods to ApiService class:
getSubjects(): Observable<Subject[]>
getSubject(id: number): Observable<Subject>
createSubject(subject: Omit<Subject, 'id'>): Observable<Subject>
updateSubject(id: number, subject: Partial<Subject>): Observable<Subject>
deleteSubject(id: number): Observable<void>
```

**Reference:** Look at existing methods for Student and University.

### Step 2: Create Subject Component

**File:** `web-dev-25-26-2/src/app/subjects/subjects.component.ts`

Create a new component similar to `UniversityComponent`:

- Form with fields: name, code, credits
- Table displaying all subjects
- Edit and delete functionality
- Loading and error states

**Reference:** Look at `university.component.ts` for the pattern.

### Step 3: Create Subject Component Template

**File:** `web-dev-25-26-2/src/app/subjects/subjects.component.html`

Create the HTML template with:
- Form for creating/editing subjects
- Table for displaying subjects
- Navigation link back to students page

**Reference:** Look at `university.component.html` for the pattern.

### Step 4: Add Routing

**File:** `web-dev-25-26-2/src/app/app.routes.ts`

Add the subjects route:

```typescript
import { SubjectsComponent } from './subjects/subjects.component';

export const routes: Routes = [
  {
    path: '',
    component: StudentsComponent
  },
  {
    path: 'university',
    component: UniversityComponent
  },
  {
    path: 'subjects',
    component: SubjectsComponent // Add this
  }
];
```

### Step 5: Add Navigation Links

Update the navigation in:
- `students.component.html` - Add link to subjects page
- `university.component.html` - Add link to subjects page
- `subjects.component.html` - Add links to other pages

### Step 6: Enhance Student Component (Optional)

**File:** `web-dev-25-26-2/src/app/students/students.component.ts`

Add functionality to:
- Display subjects for each student in the table
- Add a way to enroll/unenroll students in subjects (could be a modal or separate page)

## Testing Checklist

### Backend Testing

- [ ] Can create a subject via POST
- [ ] Can retrieve all subjects via GET
- [ ] Can retrieve a subject by ID
- [ ] Can update a subject via PUT
- [ ] Can delete a subject via DELETE
- [ ] Subject code must be unique
- [ ] All required fields are validated
- [ ] Relationships work correctly (students can be linked to subjects)

### Frontend Testing

- [ ] Subject form validates required fields
- [ ] Can create a new subject
- [ ] Can view all subjects in table
- [ ] Can edit an existing subject
- [ ] Can delete a subject
- [ ] Loading states work correctly
- [ ] Error messages display properly
- [ ] Navigation between pages works

## Common Pitfalls to Avoid

1. **Forgetting to register routes** - Make sure routes are added to `server.js`
2. **Missing entity registration** - Subject must be in `database.js` entities array
3. **Incorrect relationship definition** - Double-check many-to-many setup
4. **Not handling errors** - Always include error handling in API calls
5. **Missing validation** - Validate all required fields on both frontend and backend
6. **Forgetting to import** - Check all imports are correct

## Helpful Resources

- TypeORM Documentation: https://typeorm.io/
- Express.js Documentation: https://expressjs.com/
- Angular Documentation: https://angular.io/docs
- PrimeNG Documentation: https://primeng.org/

## Submission

Once complete, ensure:
1. All files are properly implemented
2. Code follows existing patterns
3. All tests pass (manual testing)
4. No console errors
5. UI is consistent with existing pages

Good luck! 🚀

