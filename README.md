# InsuranceProject

#I. Executive Summary
##The purpose of this paper is to analyze and upgrade ScholaSure, an insurance company in regards 
to their database management system (DBMS). ScholaSure and its components are constructed 
by our team as a hypothetical business simulation which is a part of our learning experience. In 
this case, we pose that ScholaSure is an insurance provider for students as they partner with 
educational institutions, they offer a four tier insurance options for students to choose from. As 
they partner with various external organizations such as hospitals, clinics, pharmacies as well as 
universities, they have to keep track of an extensive amount of data. In order for ScholaSure to 
fluidly navigate within this structure, we took a comprehensive approach of building a Database 
Management System. ScholaSure’s business model was closely examined and the project scope 
was defined which helped to set the stage for our analysis. Following that, we constructed a 
conceptual data model that yielded insight into the relationship between relevant entities and its 
cardinalities. Then, a logical database design was built in order to transform the database into its 
most atomic and innate form so all the relevant information is easily accessible. With the study 
of real-world student insurance companies such as JCB Insurance Solution, possible business 
problems were identified. These are in functional areas such as Marketing/Sales, 
Finance/Budgeting and Customer Service/Support which were resolved using SQL. Collectively, 
ScholaSure’s database is thoroughly analyzed, upgraded, and fine-tuned to enhance its efficiency 
and effectiveness in managing extensive data.

#II. Background 
##We have created our own business scenario along with the data that resembles an insurance 
company for students. 
ScholaSure is an insurance provider dedicated to partnering with educational institutions across 
the United States. They offer a comprehensive four-tier insurance solution exclusively tailored 
for students, covering the chosen academic terms as follows:
Bronze: This basic insurance plan provides essential medical coverage for illnesses, accidents, 
and preventive care at $388 per academic semester.
Silver: This includes the basic coverage, along with specialist care, prescription drugs, and mental 
health services, at $881 per academic semester. 
Gold: For comprehensive coverage, the Gold plan offers standard care in addition to extensive 
medical, dental, and vision coverage with lower deductibles and copayments, priced at $910 per 
academic semester.
Platinum: For wide coverage, the Platinum plan offers foremost care in addition to extensive 
medical, dental, and vision coverage with lower deductibles and copayments priced at $2158 per 
annum(Yearly).
ScholaSure's business operations are designed to seamlessly connect insured students with a 
network of providers such as medical (hospital & clinics) and pharmacy institutions across the 
country. Their providers are meticulously chosen for their service quality and commitment to 
serving their insured students. When a student is in-need of medical care or pharmacy drugs, the 
student’s coverage is verified by the provider. After the coverage is confirmed and the student 
has received the necessary services, the provider submits the insurance claims for reimbursement to ScholaSure. If the student had obtained the services without the coverage verification or had 
paid for a medical care out of pocket, the student is able to submit the insurance claim for 
reimbursement only if the provider is in-network. Out-of-network provider’s claim applications 
are not accepted by ScholaSure. ScholaSure’s team carefully reviews these claims, and eligible 
expenses are promptly reimbursed to the provider or the student if they paid out of pocket. 
Throughout this process, they maintain open and transparent communication with both students 
and providers.
In summary, their business operations focus on efficiently connecting insured students from the 
partnered educational institutions with a vast network of reputable healthcare and pharmacy 
providers.

#IV. Project Scope & Objectives
##In order to create a proper DBMS we decided to use Microsoft Access. This allowed each 
member to individually create the tables and easily modify them to our needs. Once all data 
tables were created, Access was imported via Excel tool, which allowed easy implementation of 
our database. Per our 3NF tables we have currently we have nine entities with the idea of these 
entities being in the perspective of ScholaSure.
The objective of the DB is to help ScholaSure increase revenue and profit. This is done by 
looking at the students who take advantage of the insurance policy. The queries will show that 
by looking at the students in higher tier plans using the, the overview of the plan, and what 
students are not taking advantage of the plan. Looking through this data we can then come to a 
conclusion of how the company can earn more profit.

#V. Business Rules Relevant to Data Model
##a. STUDENT and SCHOOL Relationship
###Each SCHOOL must have at least one STUDENT.
Each STUDENT is enrolled in one and only one SCHOOL.
This business rule enforces a one-to-many relationship between the entities SCHOOL and 
STUDENT. It mandates that each SCHOOL entity must have at least one related STUDENT 
entity, ensuring there are no schools without students. Additionally, it specifies that each 
STUDENT can only be enrolled in one school. This is as per ScholaSure’s registration form, 
where students have the option to enroll for insurance under only one school. 

##b. STUDENT and INSURANCE Relationship
###Each STUDENT must have at least one INSURANCE. 
Each INSURANCE must have one and only one STUDENT. 
Students have only one insurance plan for a given time period (term) however, if they want to, 
there is an option to enroll in upcoming terms. When that happens, a new insurance policy 
number is generated for the student so that’s why there is one to many relationship between 
student and insurance table.

##c. INSURANCE and MEDICAL Relationship

###Each INSURANCE may have none or many MEDICAL RECORD.
Each MEDICAL RECORD may have one and only one INSURANCE.
Each MEDICAL provider may have many MEDICAL RECORD or none.
Each MEDICAL RECORD may have one and only one MEDICAL.
Here, a many-to-many relationship is resolved using MEDICAL RECORD as an associative 
entity. This relationship exists when the medical provider (hospital, clinic etc) files a claim on 
behalf of the student after receiving the medical services, meaning the application is received 
from the provider and not the student. Each of the scholasure’s insurance may have optional 
many medical claims because not all the students have received medical services from the wide 
database of medical providers that scholasure carries. While some students may have been 
charged by the same or different medical providers more than once. MEDICAL CLAIM helps 
to make sure that each time a claim is charged by the medical provider, it is treated individually. 

##d. INSURANCE and PHARMACY Relationship
###An INSURANCE may have many Prescription or none.
A Prescription will work with one and only one INSURANCE.
A PHARMACY may file many Prescription or none. 
Each Prescription must have one and only one PHARMACY.
There is a many-to-many relationship between INSURANCE and PHARMACY, which is 
resolved using the Prescription associative entity. Similar to the INSURANCE and MEDICAL 
relationship, the insured students may or may not have a claim with the many pharmacy stores 
that are in Scholasure’s network. 

##e. INSURANCE and TIER
###Each INSURANCE has one and only one Tier
Each Tier must have at least one Insurance
There is a mandatory one to many relationship between Insurance and Tier. Each insurance plan 
for a student has only one type of tier which may be bronze, silver, gold or platinum. And, each 
tier is at least enrolled by one student as per the ScholaSure, ensuring there is a necessity and 
demand for each tier.
