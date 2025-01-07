### Task 1: Add more students to the students collection:
- Add at least 5 new students to the students collection with unique names, roll numbers, and course enrollments.

```js
db.students.insertMany([{"name": "Alice Johnson",
    "roll_number": "CSE202501",
    "courses": ["Data Structures", "Machine Learning", "Software Engineering"]},{ "name": "David Patel",
    "roll_number": "CSE202502",
    "courses": ["Computer Networks", "Cryptography", "Operating Systems"]},{"name": "Sophia Lee",
    "roll_number": "CSE202503",
    "courses": ["Database Systems", "Artificial Intelligence", "Web Development"]},{"name": "Ethan Brown",
    "roll_number": "CSE202504",
    "courses": ["Compiler Design", "Big Data Analytics", "Mobile Application Development"]},{ "name": "Isabella Garcia",
    "roll_number": "CSE202505",
    "courses": ["Human-Computer Interaction", "Cloud Computing", "Cybersecurity"]}]);
```
### Task 2: Insert a new course into the courses collection
```js
db.courses.insertOne({
  "course_code": "CS202",
  "name": "Data Structures",
  "credits": 3,
  "instructor": "Prof. Krishna"
})

```
### Task 3: Fetch a specific student's record by roll number

```js
db.students.findOne({roll_number:"CSE202504"})
```

### Task 4: Query all students who are enrolled in a particular course

```js
db.students.findOne({coursesEnrolled:"Mathematics"})
```


### Task 5: Update a student's courses

```js
db.courses.updateOne({name:"Data Structures"},{$set:{courses_code:"cs1001"}})
```

### Task 6: Remove a course from a student's courses list

```js
db.students.updateOne(
  { name: "Mahir" },  r
  { $pull: { coursesEnrolled: "Mathematics" } }  );
  ```

  ### Task 7: Find all courses with 3 credits

  ```js
  db.courses.findOne({credits:3})
  ```

  ### Task 8: Find students who have enrolled in more than 2 courses
  ```js
  db.students.find({ courses: { $size: { $gt: 2 } } });
```
### Task 9: Use the $in operator to find students enrolled in multiple courses
```js
db.students.find({ courses: { $in: ["CS101", "Mathematics"] } });
```
### Task 10: Fetch all students from a specific department (e.g., CSE)
```js
db.students.findOne({department:"CSE"})
```
### Task 11: Query students who are in their 3rd year
```js
db.students.find({ year: 3 });
```
### Task 12: Query students using a range for their year
```js
db.students.find({ year: { $gte: 2, $lte: 3 } });
```
### Task 13: Count the total number of students in each department
```js
db.students.aggregate([
  { $group: { _id: "$department", total_students: { $sum: 1 } } }
]);
```
### Task 14: Group courses by credits
```js
db.students.aggregate([
  { $group: { _id: "$department", total_students: { $sum: 1 } } }
]);
```
### Task 15: Find the highest credit course
```js
db.courses.aggregate([
  { $sort: { credits: -1 } }, 
  { $limit: 1 }             
]);
```
### Task 16: Use the $and operator for filtering students
```js
db.students.find({
  $and: [
    { department: "CSE" },
    { $expr: { $gt: [{ $size: "$courses" }, 2] } }
  ]
});
```
### Task 17: Add a new field to all documents in the students collection

```js
db.students.updateMany(
  {}, 
  { $set: { activeStatus: true } } 
);
```
### Task 18: Use $rename to rename a field

```js
db.students.updateMany(
  {}, 
  { $rename: { "coursesEnrolled": "enrolledCourses" } } 
);
```
### Task 19: Set default values for new fields in all student documents
```js
db.students.updateMany(
  {}, 
  { $set: { graduationYear: 2025 } } 
);
```
### Task 20: Use the $push operator to add a new course to a student’s course list
```js
db.students.updateOne(
  { name: "Mahir" }, 
  { $push: { coursesEnrolled: "CS303" } } 
);
```
### Task 21: Use $pull to remove a course from a student's courses list
```js
db.students.updateOne(
  { name: "Jenil" }, 
  { $pull: { coursesEnrolled: "CS101" } }
);
```
### Task 22: Remove a student from the students collection
```js
db.students.deleteOne(
  { roll_number: "CS1004" } 
);
```
### Task 23: Find students who are enrolled in both CS101 and MATH202
```js
db.students.find({
  coursesEnrolled: { $all: ["CS101", "MATH202"] }
});
```
### Task 24: Use $regex to search for students whose name starts with "A"
```js
db.students.find({
  name: { $regex: "^A", $options: "i" }
});
```
### Task 25: Use $exists to find students with enrolled courses
```js
db.students.find({
  coursesEnrolled: { $exists: true, $not: { $size: 0 } } 
});
```
#### **Task 26: Add a field to store students' grades for each course**  
- Add a new field `grades` to the `students` collection and store an array of grades for each course.
```js
db.students.updateMany({}, { $set: { grades: [] } });
```
```js
db.students.updateOne(
    { _id: ObjectId("STUDENT_ID") },
    { $push: { grades: { course: "Math", grade: 95 } } }
);
```
```js
db.students.find({}, { name: 1, grades: 1 }).pretty();
```
#### **Task 27: Use `$elemMatch` to query students enrolled in specific courses**  
- Find students enrolled in `CS101` and have the grade `A`.
```js
db.students.find({
    grades: {
        $elemMatch: {
            course: "CS101",
            grade: "A"
        }
    }
});
```
#### **Task 28: Use `$size` operator to query students with exactly 2 courses enrolled**  
- Query students who have enrolled in exactly two courses.
```js
db.students.find({
    grades: { $size: 2 }
});
```
#### **Task 29: Perform a text search for a course title**  
- Use text indexing to search for the course `Digital Electronics` in the `courses` collection.
```js
db.courses.createIndex({ title: "text" });
```
```js
db.courses.find({
    $text: { $search: "Digital Electronics" }
});
```
#### **Task 30: Create a compound index on department and year**  
- Create a compound index on the fields `department` and `year` for better querying performance.
```js
db.studets1.createIndex({ department: 1, year: 1 });
```
```js
db.students1.find({ department: "Computer Science", year: 2 });
```
#### **Task 31: Use `$sort` to order students by their roll number**  
- Sort the students in ascending order of their roll number.
```js
db.students.find().sort({ roll_number: 1 });
```
#### **Task 32: Create a unique index on the roll number**  
- Create a unique index to ensure that the roll numbers in the `students` collection are unique.
```js
db.students.createIndex({ roll_number: 1 }, { unique: true });
```
#### **Task 33: Update the course name in the `courses` collection**  
- Update the name of the course `CS101` to `Intro to Programming`.
```js
db.courses.updateOne(
    { title: "CS101" }, 
    { $set: { title: "Intro to Programming" } } 
);
```
#### **Task 34: Create a backup of the `CodingGitaStudents` database**  
- Use `mongodump` to back up the entire `CodingGitaStudents` database.
```js
mongodump --db CodingGitaStudents --out /path/to/backup/directory
```
#### **Task 35: Restore the `CodingGitaStudents` database from the backup**  
- Use `mongorestore` to restore the database after a backup.
```js
mongorestore --db CodingGitaStudents /path/to/backup/directory/CodingGitaStudents/
```
#### **Task 36: Use `$project` to reshape data in aggregation**  
- Project only the `name` and `department` of students using an aggregation query.
```js
db.students.aggregate([
    {
        $project: {
            name: 1,       
            department: 1   
        }
    }
]);
```
#### **Task 37: Use `$unwind` to deconstruct the courses array**  
- Use `$unwind` to split the `coursesEnrolled` array into individual documents.
```js
db.students.aggregate([
    {
        $unwind: "$coursesEnrolled"
    }
]);
```
#### **Task 38: Use `$limit` to retrieve only the first 3 students**  
- Use `$limit` to limit the result to the first 3 students in the `students` collection.
```js
db.students.aggregate([
    { $limit: 3 }
]);
```
#### **Task 39: Use `$skip` to skip the first 2 students and get the rest**  
- Use `$skip` to fetch all students except the first two.
```js
db.students.aggregate([
    { $skip: 2 }
]);
```
#### **Task 40: Use `$lookup` to join student data with courses**  
- Use `$lookup` to fetch the course information for students.
```js
db.students.aggregate([
    {
        $lookup: {
            from: "courses",          
            localField: "coursesEnrolled.course", 
            foreignField: "title",     
            as: "course_details"      
        }
    }
]);
```