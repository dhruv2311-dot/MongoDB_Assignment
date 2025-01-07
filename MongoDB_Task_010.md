#### **Task 1: Add multiple students**
Insert at least **5 students** into the `students` collection with unique roll numbers, names, departments, years, and subjects enrolled.
```json
db.students.insertMany([
  { 
    "name": "Jenil",
    "rollNumber": 101,
    "department": "Computer Science",
    "year": 2,
    "subjectsEnrolled": ["React", "NodeJS", "MongoDB"]
  },
  { 
    "name": "Mahir",
    "rollNumber": 102,
    "department": "Computer Science",
    "year": 2,
    "subjectsEnrolled": ["React", "NodeJS"]
  },
  { 
    "name": "Arjun",
    "rollNumber": 103,
    "department": "Electrical Engineering",
    "year": 3,
    "subjectsEnrolled": ["Circuit Theory", "Electrical Machines"]
  }
]);
```
#### **Task 2: Add multiple subjects**
Insert **4 subjects** into the `subjects` collection, each with 3 to 5 topics.
```json
db.subjects.insertMany([
  { 
    "subjectName": "React",
    "topics": [
      "JSX", 
      "Components", 
      "State", 
      "Props", 
      "Hooks"
    ]
  },
  { 
    "subjectName": "NodeJS", 
    "topics": [
      "Modules", 
      "Express", 
      "File System", 
      "Asynchronous Programming"
    ]
  },
  { 
    "subjectName": "MongoDB", 
    "topics": [
      "Database Design", 
      "CRUD Operations", 
      "Aggregation", 
      "Indexes"
    ]
  }
]);
```
#### **Task 3: Query students based on subject enrollment**
Query the `students` collection to find all students who are enrolled in **NodeJS**.
```json
db.students.find({ "subjectsEnrolled": "NodeJS" });
```
#### **Task 4: Add a new topic to a subject**
Add a new topic to the **NodeJS** subject.
```json
db.subjects.updateOne(
  { "subjectName": "NodeJS" },
  { $push: { "topics": "MongoDB" } }
);
```
    #### **Task 5: Query subjects with multiple topics**
Query the `subjects` collection to find subjects that contain **at least 4 topics**.
```json
db.subjects.find({
  $expr: {
    $gte: [{ $size: "$topics" }, 4]
  }
});
```
#### **Task 6: Update student enrollment**
Add the subject **"React Native"** to **Jenil's** subjects.
```json
db.students.updateOne(
  { "name": "Jenil" },
  { $push: { "subjectsEnrolled": "React Native" } }
);
```
#### **Task 7: Query all students**
Query all students in the database and print out their names and enrolled subjects.
```json
db.students.find({}, { name: 1, enrolledSubjects: 1, _id: 0 });
```
#### **Task 8: Update multiple students' year**
Update the year for all students in the **Computer Science** department to year 3.
```json
db.students.updateMany(
  { department: "Computer Science" }, 
  { $set: { year: 3 } }               
);
```
#### **Task 9: Add new topics to multiple subjects**
Add new topics to **React**, **NodeJS**, and **MongoDB** subjects. Ensure each subject gets at least **one** new topic.

```json
db.subjects.updateOne(
  { name: "React" }, 
  { $addToSet: { topics: "Hooks" } } 
);

db.subjects.updateOne(
  { name: "NodeJS" }, 
  { $addToSet: { topics: "Middleware" } } 
);

db.subjects.updateOne(
  { name: "MongoDB" }, 
  { $addToSet: { topics: "Aggregation" } } 
);
```
#### **Task 10: Remove a topic from a subject**
Remove the topic **"Express"** from the **NodeJS** subject.
```json
db.subjects.updateOne(
  { name: "NodeJS" }, 
  { $pull: { topics: "Express" } }
);
```
#### **Task 11: Query all students in a specific year**
Query and return all students in **year 2** or **year 3**.
```json
db.students1.find({year:{$in:[2,3]}})
```

#### **Task 12: Delete a student by roll number**
Delete a student from the database using their **roll number**.

```json
db.students.deleteOne(
  { rollNumber: 103 } 
);
```
#### **Task 13: Delete all students from a department**
Delete all students who belong to the **Electrical Engineering** department.
```json
db.students.deleteMany({department:"Electrical Engineering"})
```

#### **Task 14: Retrieve all topics for a subject**
Query the **MongoDB** subject and retrieve all topics listed for it.
```json
db.courses1.find(
  { name: "MongoDB" }, 
  { topics: 1, _id: 0 } 
);
```
#### **Task 15: Count the number of subjects in which a student is enrolled**
Write a query that returns the number of subjects each student is enrolled in.
```json
db.students.aggregate([
  {
    $project: {
      name: 1, 
      enrolledSubjectsCount: { $size: { $ifNull: ["$enrolledSubjects", []] } } 
    }
  }
]);
```