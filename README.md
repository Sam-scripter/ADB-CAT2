Data model option: - document store
Database software to use: MongoDB
QUESTION 1: SETUP
Setup instructions
Install on windows 11 operating system
MongoDB version 8.0.12
Download from this link: Install MongoDB Community Kubernetes Operator | MongoDB

Installing steps
-	Double click the installer to initiate the installation process

 ![screenshot](Lab_screenshot_1.jpg)

-	Click next and accept the terms of agreement

 ![screenshot](Lab_screenshot_2.png)

-	Click Next and then select Complete to install the complete package

 ![screenshot](Lab_screenshot_3.png)

Screenshots
 Missed – install as a service, install compass, finish


Launch MongoDB compass, select add new connection

 ![screenshot](Lab_screenshot_4.png)

Specify the following parameters in the window that appears
Uri: mongodb://localhost:27017
Name: mongoDBAssignment
Save&Connect

QUESTION 2: BASIC OPERATIONS

Create database
We will use mongoDB shell (mongosh) to demonstrate CRUD
In the Context of a Recruitment System, we will use recruitmentDB as our database, applicants as the collection and each applicant record as a document, each applicant document will include:
applicantId (Number)
name (String)
gender (String)
position (String)
score (Number)
status (String: "pending", "shortlisted", "rejected")

STEPS

1.	create recruitmentDB database
          
command

use recruitmentDB

expected output
 
 ![screenshot](Lab_screenshot_5.png)

2. CREATE: add sample documents to our recruitment database

a.	command to add a document to applicants’ collection
db.applicants.insertOne({
  applicantId: 111,
  name: "Janet Chebet",
  gender: "Female",
  position: "Procurement Officer",
  score: 87,
  status: "pending"
})

Sample Output

 ![screenshot](Lab_screenshot_6.png)

b.	insert many records(add many documents to applicants collection)

db.applicants.insertMany([
  { applicantId: 101, name: "Grace Wanjiku", gender: "Female", position: "ICT Officer", score: 82, status: "pending" },<br>
  { applicantId: 102, name: "James Otieno", gender: "Male", position: "Clerk", score: 75, status: "pending" },<br>
  { applicantId: 103, name: "Mary Atieno", gender: "Female", position: "Clerk", score: 90, status: "pending" },<br>
  { applicantId: 104, name: "Peter Mwangi", gender: "Male", position: "Accountant", score: 68, status: "rejected" },<br>
  { applicantId: 105, name: "Amina Yusuf", gender: "Female", position: "ICT Officer", score: 88, status: "shortlisted" },<br>
  { applicantId: 106, name: "John Kimani", gender: "Male", position: "Security Officer", score: 72, status: "pending" },<br>
  { applicantId: 107, name: "Susan Nyambura", gender: "Female", position: "Secretary", score: 85, status: "shortlisted" },<br>
  { applicantId: 108, name: "Kevin Onyango", gender: "Male", position: "Driver", score: 65, status: "pending" },<br>
  { applicantId: 109, name: "Lucy Njeri", gender: "Female", position: "Accountant", score: 91, status: "shortlisted" },<br>
  { applicantId: 110, name: "Brian Kiptoo", gender: "Male", position: "ICT Officer", score: 79, status: "pending" }<br>
])<br>


Output
 
 ![screenshot](Lab_screenshot_7.png)


2. READ: Query applicants

a. To retrieve all applicants use the following command
                 db.applicants.find()
This returns all the 11 records inserted
Sample output

![screenshot](Lab_screenshot_8.png)
 

b. use the following command to get all applicants who applied for the Clerk position
     db.applicants.find({ position: "Clerk" })

sample output

 ![screenshot](Lab_screenshot_9.png)

c. To get all applicants with scores above 90, use the following command
     db.applicants.find({ score: { $gte: 90 } })
    Sample output
   ![screenshot](Lab_screenshot_10.png)

3. UPDATE: Modify Applicants Records
a. to shortlist applicant with a score of more than 80 use the following command
db.applicants.updateMany(
  { score: { $gte: 80 } },
  { $set: { status: "shortlisted" } }
)

Output is as follows

![screenshot](Lab_screenshot_11.png)
 
b. to update applicant name by ID use the following command
db.applicants.updateOne(
  { applicantId: 102 },
  { $set: { name: "James O. Otieno" } }
)
Output is as follows

 ![screenshot](Lab_screenshot_12.png)

4. DELETE:- remove applicant records

a.	Delete an applicant   by id

![screenshot](Lab_screenshot_13.png)

Command:

db.applicants.deleteOne({ applicantId: 101 })

output is as follows

 

b.	To delete all rejected applicants

Command:

db.applicants.deleteMany({ status: "rejected" })

output is as follows

 ![screenshot](Lab_screenshot_14.png)

Sample data used in JSON format

[<br>
  {
    "applicantId": 101,
    "name": "Grace Wanjiku",
    "gender": "Female",
    "position": "ICT Officer",
    "score": 82,
    "status": "pending"
  },<br>
  {
    "applicantId": 102,
    "name": "James Otieno",
    "gender": "Male",
    "position": "Clerk",
    "score": 75,
    "status": "pending"
  },<br>
  {
    "applicantId": 103,
    "name": "Mary Atieno",
    "gender": "Female",
    "position": "Clerk",
    "score": 90,
    "status": "pending"
  },<br>
  {
    "applicantId": 104,
    "name": "Peter Mwangi",
    "gender": "Male",
    "position": "Accountant",
    "score": 68,
    "status": "rejected"
  },<br>
  {
    "applicantId": 105,
    "name": "Amina Yusuf",
    "gender": "Female",
    "position": "ICT Officer",
    "score": 88,
    "status": "shortlisted"
  },<br>
  {
    "applicantId": 106,
    "name": "John Kimani",
    "gender": "Male",
    "position": "Security Officer",
    "score": 72,
    "status": "pending"
  },<br>
  {
    "applicantId": 107,
    "name": "Susan Nyambura",
    "gender": "Female",
    "position": "Secretary",
    "score": 85,
    "status": "shortlisted"
  },<br>
  {
    "applicantId": 108,
    "name": "Kevin Onyango",
    "gender": "Male",
    "position": "Driver",
    "score": 65,
    "status": "pending"
  },<br>
  {
    "applicantId": 109,
    "name": "Lucy Njeri",
    "gender": "Female",
    "position": "Accountant",
    "score": 91,
    "status": "shortlisted"
  },<br>
  {
    "applicantId": 110,
    "name": "Brian Kiptoo",
    "gender": "Male",
    "position": "ICT Officer",
    "score": 79,
    "status": "pending"
  }<br>
]<br><br>
QUESTION 3: APPLIED SCENARIO<br>
Public Service Commission normally collects thousands of applicants records for the purposes of recruiting persons to serve in the public organizations. A portal is used to collect this data. Applicants’ profiles are normally varied in a way depending on the job descriptions. The profiles are build based on: personal information, qualifications, work experiences, jobs applied, status of the applications among others. 
MongoDB can be applied in this scenario because of the variance of applicants’ data; it can allow for nesting information when building applicants profile thus allowing the applicants profiles to be stored as self-contained documents. It makes it easy to add new fields like interview dates or remarks without changing the schema. The Document format maps well with the PSC web portal thus also contributing to improvement in responsiveness during high traffic times.<br>
MongoDB database can be used to model this problem by storing each applicant as a document in the applicants collection as shown below: -<br>
{<br>
  "applicantId": 103,
  "name": "Mary Atieno",
  "gender": "Female",
  "position": "Clerk",
  "score": 90,
  "status": "pending",
  "disabilityStatus": "none",
  "contact": {
    "email": "mary.atieno@example.com",
    "phone": "0712345678"
  },<br>
  "workExperience": [<br>
    { "company": "KRA", "years": 2 },
    { "company": "County Office", "years": 1 }<br>
  ]<br>
}<br>
This document format allows for the storage of nested and optional data therefore, eliminating the need for complex joins or rigid table structure 
<br>
Queries can be used to solve the issue of data retrieval as shown below: -
a.	to shortlist all applicants with minimum score of 80%, use<br>
db.applicants.updateMany(<br>
  { score: { $gte: 80 } },
  { $set: { status: "shortlisted" } }
)<br>
b.	to filter by gender and disability use<br>
db.applicants.find({<br>
  gender: "Female",
  disabilityStatus: { $ne: "none" }
})<br>

GROUP CONTRIBUTION SUMMARY:<br>
Name: Samuel Shadiva Tokoye<br>
Student ID: 222072<br>
Responsibilities:<br>
•	MongoDB setup<br>
•	Scenario design<br><br>


Name: Elizabeth [COMPLETE THE NAME]<br>
Student ID: [INSERT_STUDENT_ID]<br>
Responsibilities:<br>
•	CRUD implementation<br>
•	Screenshots and visuals<br>

Name: Catherine [COMPLETE THE NAME]<br>
Student ID: [INSERT_STUDENT_ID]<br>
Responsibilities:<br>
•	Markdown lab documentation


