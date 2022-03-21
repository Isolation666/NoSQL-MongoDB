# NoSQL-MongoDB
This repository is a part of of Homework in 01219231 Database

## Create New Database and Collection

```
> use Exam_Score

> db.createCollection('Students')
```

## Insert Data into Database

```
> db.Students.insertMany([
  {"name":"Ramesh","subject":"maths","marks":87},
  {"name":"Ramesh","subject":"english","marks":59},
  {"name":"Ramesh","subject":"science","marks":77},
  {"name":"Rav","subject":"maths","marks":62},
  {"name":"Rav","subject":"english","marks":83},
  {"name":"Rav","subject":"science","marks":71},
  {"name":"Alison","subject":"maths","marks":84},
  {"name":"Alison","subject":"english","marks":82},
  {"name":"Alison","subject":"science","marks":86},
  {"name":"Steve","subject":"maths","marks":81},
  {"name":"Steve","subject":"english","marks":89},
  {"name":"Steve","subject":"science","marks":77},
  {"name":"Jan","subject":"english","marks":0,"reason":"absent"}  
  ])
```
## Queries

### 1. Find the total marks for each student across all subjects.

```
> db.Students.aggregate([{$group:{_id: '$name', TotalMarks: {$sum: '$marks'}}}])

The Result:

< { _id: 'Steve', TotalMarks: 247 } 
  { _id: 'Rav', TotalMarks: 216 }
  { _id: 'Jan', TotalMarks: 0 }
  { _id: 'Ramesh', TotalMarks: 223 }
  { _id: 'Alison', TotalMarks: 252 }
```
### 2. Find the maximum marks scored in each subject.
```
> db.Students.aggregate([{$group:{_id: '$subject', MaxScore: {$max: '$marks'}}}])

The Result:

< { _id: 'maths', MaxScore: 87 }
  { _id: 'english', MaxScore: 89 }
  { _id: 'science', MaxScore: 86 }
```
### 3. Find the minimum marks scored by each student.

```
> db.Students.aggregate([{$group:{_id: '$name', MinScore: {$min: '$marks'}}}])

The Result:

< { _id: 'Rav', MinScore: 62 }
  { _id: 'Alison', MinScore: 82 }
  { _id: 'Steve', MinScore: 77 }
  { _id: 'Ramesh', MinScore: 59 }
  { _id: 'Jan', MinScore: 0 }
```

### 4. Find the top two subjects based on average marks.

```
> db.Students.aggregate([{$group: {_id: "$subject", AvgScore: {$avg: "$marks"}}, }, {$sort: {AvgScore: -1}}, {$limit: 2}])

The Result:

< { _id: 'maths', AvgScore: 78.5 }
  { _id: 'science', AvgScore: 77.75 }
```
