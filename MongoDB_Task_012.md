### Task 1: Add more students to the students collection:
- Add at least 5 new students to the students collection with unique names, roll numbers, and course enrollments.

```
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
```
db.courses.insertOne({
  "course_code": "CS202",
  "name": "Data Structures",
  "credits": 3,
  "instructor": "Prof. Krishna"
})

```
### Task 3: Fetch a specific student's record by roll number

```
db.students.findOne({roll_number:"CSE202504"})
```

### Task 4: Query all students who are enrolled in a particular course

```
db.students.findOne({coursesEnrolled:"Mathematics"})
```


### Task 5: Update a student's courses

```
db.courses.updateOne({name:"Data Structures"},{$set:{courses_code:"cs1001"}})
```

### Task 6: Remove a course from a student's courses list

```
db.students.updateOne(
  { name: "Mahir" },  r
  { $pull: { coursesEnrolled: "Mathematics" } }  );
  ```

  ### Task 7: Find all courses with 3 credits

  ```
  db.courses.findOne({credits:3})
  ```

  ### Task 8: Find students who have enrolled in more than 2 courses
  ```
  db.students.find({ courses: { $size: { $gt: 2 } } });
```
### Task 9: Use the $in operator to find students enrolled in multiple courses
```
db.students.find({ courses: { $in: ["CS101", "Mathematics"] } });
```
### Task 10: Fetch all students from a specific department (e.g., CSE)
```
db.students.findOne({department:"CSE"})
```
### Task 11: Query students who are in their 3rd year
```
db.students.find({ year: 3 });
```
### Task 12: Query students using a range for their year
```
db.students.find({ year: { $gte: 2, $lte: 3 } });
```
### Task 13: Count the total number of students in each department
```
db.students.aggregate([
  { $group: { _id: "$department", total_students: { $sum: 1 } } }
]);
```
### Task 14: Group courses by credits
```
db.students.aggregate([
  { $group: { _id: "$department", total_students: { $sum: 1 } } }
]);
```
### Task 15: Find the highest credit course
```
db.courses.aggregate([
  { $sort: { credits: -1 } }, 
  { $limit: 1 }             
]);
```
### Task 16: Use the $and operator for filtering students
```
db.students.find({
  $and: [
    { department: "CSE" },
    { $expr: { $gt: [{ $size: "$courses" }, 2] } }
  ]
});
```
### Task 17: Add a new field to all documents in the students collection

```
db.students.updateMany(
  {}, 
  { $set: { activeStatus: true } } 
);
```
### Task 18: Use $rename to rename a field

```
db.students.updateMany(
  {}, 
  { $rename: { "coursesEnrolled": "enrolledCourses" } } 
);
```
### Task 19: Set default values for new fields in all student documents
```
db.students.updateMany(
  {}, 
  { $set: { graduationYear: 2025 } } 
);
```
### Task 20: Use the $push operator to add a new course to a student’s course list
```
db.students.updateOne(
  { name: "Mahir" }, 
  { $push: { coursesEnrolled: "CS303" } } 
);
```
### Task 21: Use $pull to remove a course from a student's courses list
```
db.students.updateOne(
  { name: "Jenil" }, 
  { $pull: { coursesEnrolled: "CS101" } }
);
```
### Task 22: Remove a student from the students collection
```
db.students.deleteOne(
  { roll_number: "CS1004" } 
);
```
### Task 23: Find students who are enrolled in both CS101 and MATH202
```
db.students.find({
  coursesEnrolled: { $all: ["CS101", "MATH202"] }
});
```
### Task 24: Use $regex to search for students whose name starts with "A"
```
db.students.find({
  name: { $regex: "^A", $options: "i" }
});
```
### Task 25: Use $exists to find students with enrolled courses
```
db.students.find({
  coursesEnrolled: { $exists: true, $not: { $size: 0 } } 
});
```