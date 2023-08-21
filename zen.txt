
  //users
  {
    "id": "user_1",
    "name": "saravana",
    "age": 23,
    "attendance": {
      "present": [
        { "date": new Date("2020-10-20") },
        { "date":new Date("2020-10-21")}
      ],
      "absent": [
        { "date": new Date("2020-10-22") },
        { "date":new Date("2020-10-23")}
      ]
    },
    "tasks": {
      "submitted": [
        { "date": new Date("2020-10-10") },
        { "date": new Date("2020-10-09") }
      ],
      "not-submitted": [
        { "date": new Date("2020-10-20") },
        { "date": new Date("2020-10-22")}
      ]
    },
    "codekata":{
      "problems_solved":30,
      "problemId":"problem_1",
      "problem_name":"binary search"
    }
  }
  //topics
  {  "topics":{
    "topic_id":"topic_1",
    "topic_name":"mongoDB",
    "taughted_date":new Date("2020-10-22")
  }}
  
  //company_drives
  db.insertOne(
  {"company_drives":{
  "company_name":"xyz private limited",
  "company_id":"company_2",
  "drive_date":new Date("2020-10-12"),
  "students_appeared":{
  "user_id":"user_1",
  "user_id":"user_2"
    }
  }})
  
  //mentors
   { "mentors":{
    "id":"mentor_1",
    "name":"kumar",
    "email":"mentor1@gmail.com",
    "mentee's_count":20
  
  }}
   
    
    1.Find all the topics and tasks which are thought in the month of October
        
    db.zen.find({topics.taughted_date:{$gt :ISODate("2020-01-01"), $gt :ISODate("2020-01-31")}})
  
    2.Find all the company drives which appeared between 15 oct-2020 and 31-oct-2020
  
    db.zen.find({topics.taughted_date:{$gt :ISODate("2020-01-15"), $gt :ISODate("2020-01-31")}})
  
    3.Find all the company drives and students who are appeared for the placement.
  
    "company_drives.students_appeared.user_id":1,
    _id:0
  
    4.Find the number of problems solved by the user in codekata
    db.zen.aggregate([
      {
        $project: {
          problems_solved: "$codekata.problems_solved",
          _id: 0,
          name: 1
        }
      }
    ]);
  
    5.Find all the mentors with who has the mentee's count more than 15
  
    db.zen.find({mentee_count:{$gt:15}})
  
    6.Find the number of users who are absent and task is not submitted  between 15 oct-2020 and 31-oct-2020
  
    db.zen.find({
      $and: [
        { "attendance.absent.date": { $gt: ISODate('2020-10-15'), $lt: ISODate('2020-10-31') } },
        { "tasks.not-submitted": { $gt: ISODate('2020-10-15'), $lt: ISODate('2020-10-31')  } }
      ]
    })
    
  
  