<h1>Data model option: - document store</h1>

Database software to use: MongoDB <br>
This lab provides a practical introduction to the Document Store data model, one of the most widely used approaches in the NoSQL database family. Using MongoDB, you will install, configure, and interact with a document store environment from scratch.<br>
In approximately 30–60 minutes, you will:<br>
-Set up a MongoDB instance a direct local installation.<br>
-Perform essential CRUD (Create, Read, Update, Delete) operations.<br>
-Apply your skills to a realistic recruitment system scenario, demonstrating why document stores are ideal for flexible and evolving data structures.<br>


<h3>QUESTION 1: SETUP</h3>
Setup instructions<br>
Install on windows 11 Operating System<br>
MongoDB version 8.0.12
Download from this link: https://www.mongodb.com/try/download/community<br>

Installation steps<br>
-	Double click the installer to initiate the installation process

 ![screenshot](Lab_screenshot_1.jpg)

-	Click **Next** and accept the End-User License Agreement

 ![screenshot](Lab_screenshot_2.png)

-	Click **Next** and then select Complete to install the complete package

 ![screenshot](Lab_screenshot_3.png)

Service Configuration<br>
![screenshot](Lab_screenshot_15.png)<br>

Install MongoDB Compass<br>
![screenshot](Lab_screenshot_16.png)<br>

Install Mongo Server<br>
![screenshot](Lab_screenshot_17.png)<br>

Installation Process<br>
![screenshot](Lab_screenshot_18.png)<br>

Launch MongoDB compass, select add new connection

 ![screenshot](Lab_screenshot_4.png)

Specify the following parameters in the window that appears
Uri: **mongodb://localhost:27017**<br>
Name: **mongoDBAssignment**<br>
**Save&Connect**<br>

You have successfully installed MondoDB server, you can now interact with it is by performiing(Create, Read, Update, Delete) operations.<br>

<h3>QUESTION 2: BASIC OPERATIONS</h3>

Create database
We will use mongoDB shell (mongosh) to demonstrate CRUD<br>
The database instance in this case is that of a Recruitment system where applicants will be the collection and each applicant record stored as a document. Each applicant record will include the following:<br>
applicantId (Number)<br>
name (String)<br>
gender (String)<br>
position (String)<br>
score (Number)<br>
status (String: "pending", "shortlisted", "rejected")<br>

**STEPS**

1.	Create recruitmentDB database
          
Use this command: **use recruitmentDB**

Expected output
 
 ![screenshot](Lab_screenshot_5.png)

2. **CREATE**: We implement this operation to add sample documents to our recruitment database

a.	Command to add a document to applicants’ collection<br>
db.applicants.insertOne({<br>
  applicantId: 111,<br>
  name: "Janet Chebet",<br>
  gender: "Female",<br>
  position: "Procurement Officer",<br>
  score: 87,<br>
  status: "pending"<br>
})<br>

Sample Output

 ![screenshot](Lab_screenshot_6.png)

b.	Insert many records(add many documents to applicants collection)

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


2. **READ**: We implement this operation to query applicants

a. To retrieve all applicants use the following command
                 db.applicants.find()
This returns all the 11 records inserted
Sample output

![screenshot](Lab_screenshot_8.png)
 

b. Use the following command to get all applicants who applied for the Clerk position
     db.applicants.find({ position: "Clerk" })

Sample output

 ![screenshot](Lab_screenshot_9.png)

c. To get all applicants with scores above 90, use the following command
     db.applicants.find({ score: { $gte: 90 } })
Sample output
![screenshot](Lab_screenshot_10.png)

3.**UPDATE:** Modify Applicants Records<br>
a. To shortlist applicant with a score of more than 80 use the following command<br>
db.applicants.updateMany(<br>
  { score: { $gte: 80 } },<br>
  { $set: { status: "shortlisted" } }<br>
)<br>

Output is as follows

![screenshot](Lab_screenshot_11.png)
 
b. To update applicant name by ID use the following command<br>
db.applicants.updateOne(<br>
  { applicantId: 102 },<br>
  { $set: { name: "James O. Otieno" } }<br>
)<br>
Output is as follows

![screenshot](Lab_screenshot_12.png)

4. **DELETE:** remove applicant records<br>

a.	Delete an applicant   by id<br>

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

**<h3>QUESTION 3: APPLIED SCENARIO</h3><br>**
Public Service Commission normally collects thousands of applicants records for the purposes of recruiting persons to serve in the public organizations. A portal is used to collect this data. Applicants’ profiles are normally varied in a way depending on the job descriptions. The profiles are build based on: personal information,academic qualifications, professional qualifications, work experiences, membership to professional bodies,jobs applied, status of the applications among others.<br> <br>

<h3>Problem</h3><br>

Retrieval of applicants records using table joins is very slow especially when it comes to working with large datasets that requires data from multiple tables.<br>
This happens during shortlisting and interviews. During shortlisting only applicants that meet certain criterias are retrived. And during interviews complete applicant profiles are needed. For example:-<br>

a) To return a list of all applicants who have met certain criterias for shortlisting purposes table joins are used as shown below.

SELECT * FROM applicants <br>
LEFT JOIN academic_qualifications ON applicants.id = academic_qualifications.applicant_id <br> 
LEFT JOIN professional_qualifications ON applicants.id = professional_qualifications.applicant_id  <br>
LEFT JOIN membership_bodies ON applicants.id = membership_bodies.applicant_id <br>
WHERE  professional_qualifications IN('CCNA', 'CISM') AND membership_bodies IN('IEEE', 'ISACA'); <br>

b) To retrieve an applicant profile, joins of all required tables is performed as shown below:-<br>

SELECT * FROM applicants  <br>
LEFT JOIN academic_qualifications ON applicants.id = academic_qualifications.applicant_id  <br>
LEFT JOIN professional_qualifications ON applicants.id = professional_qualifications.applicant_id  <br>
LEFT JOIN membership_bodies ON applicants.id = membership_bodies.applicant_id where applicants.id = 112; br>

c) How the database can be used to model this problem.<br>
MongoDB’s document model can allow for clean and nested representation of this data within a single applicant record without normalization. 
For instance, the sample applicant data below demonstrates how the MongoDB database can model this problem. We can have applicants with different profiles, for instance applicant 103 and applicant 112 have totally different profiles, their additional data are nested under their profiles. This data can be retrieved using the queries below without performing any joins thus improving query performance.

applicant 103
<br>
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
  
  
applicant 112<br>

{<br>
  "applicantId": 112,
  "name": "Josephine Naliaka",
  "gender": "Female",
  "position": "ICT Officer",
  "score": 86,
  "status": "pending",
  "academicQualifications": [
    {
      "level": "Diploma",
      "field": "Information Technology",
      "institution": "Technical University of Kenya",
      "year": 2018
    },<br>
    {
      "level": "Degree",
      "field": "Computer Science",
      "institution": "Jomo Kenyatta University of Agriculture and Technology",
      "year": 2021
    }
  ],<br>
  "professionalCertifications": [
    {
      "name": "CCNA",
      "institution": "Cisco",
      "year": 2022
    },
    {
      "name": "CISM",
      "institution": "ISACA",
      "year": 2023
    }
  ],<br>
  "professionalMemberships": [
    {
      "organization": "ISACA",
      "membershipNumber": "IS567890",
      "since": 2023
    }
  ]
}<br>

<h3>How the model resolves the problem of table joins</h3>

a) To return a list of all applicants who have met certain criterias for shortlisting purposes, the following query is used without performing complex table joins<br>

db.applicants.find({<br>
  "professionalCertifications.name": { $in: ["CCNA", "CISM"] },<br>
  "membership_bodies.organization": { $in: ["IEEE", "ISACA"] }<br>
})<br>


b) To retrieve an entire applicant profile during interview without table joining only one query is used as shown below for the case of applicant 112. <br>


db.applicants.findOne({ applicant_id: "112" })<br>

<h3>GROUP CONTRIBUTION SUMMARY:</h3><br>

**Name: Samuel Shadiva Tokoye**<br>
Student ID: 222072<br>
Responsibilities:<br>
•	MongoDB setup<br>
•	Scenario design<br><br>

**Name: Elizabeth Sikuku**<br>
Student ID: 096039<br>
Responsibilities:<br>
•	CRUD implementation<br>
•	Screenshots and visuals<br>

**Name: Catherine Anyango**<br>
Student ID: 223933<br>
Responsibilities:<br>
•	Markdown lab documentation


