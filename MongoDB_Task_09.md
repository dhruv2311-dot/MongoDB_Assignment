**Task 1: Create a "CodingGita Students" database**

Create a new MongoDB database called `CodingGita`. Add two collections:
- `students`: Name, roll number, department, year, courses enrolled.
- `courses`: Course code, name, credits, instructor.

```js
use codinggita
```
```js
db.createCollection("students");
```
```js
db.createCollection("courses");
```
---

**Task 2: Perform CRUD operations**
- Add a few more students and courses to the database.
- Query data based on:
  - Department (e.g., "Computer Science").
  - Year (e.g., "2").
  - Courses enrolled (e.g., "CS101").
- Update the courses for a specific student (e.g., adding a new course).
- Delete a student or course from the database.

```js
db.students.find({ "department": "Computer Science" });
```
```js
db.students.find({ "year": 2 });
```
```js
db.students.find({ "coursesEnrolled": "CS101" });
```
```js
db.students.updateOne(
  { "name": "Arjun" },
  { $push: { "coursesEnrolled": "CS102" } }
);
```
```js
db.students.deleteOne({ "name": "Arjun" });
```