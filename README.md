# ScholarSure Database Consultation Project

I. Executive Summary

The purpose of this paper is to analyze and upgrade ScholaSure, an insurance company in regards 
to their database management system (DBMS). ScholaSure and its components are constructed 
as a hypothetical business simulation which is a part of the learning experience. In 
this case, ScholaSure is an insurance provider for students who partners with 
educational institutions, while offering a four tier insurance options for students. As 
they partner with various external organizations such as hospitals, clinics, pharmacies as well as 
universities, they have to keep track of an extensive amount of data. In order for ScholaSure to 
fluidly navigate within this structure, we took a comprehensive approach of building a Database 
Management System. ScholaSure’s business model was closely examined and the project scope 
was defined which helped to set the stage for our analysis. Following that, a 
conceptual data model was constructed that yields insight into the relationship between relevant entities and its 
cardinalities. Then, a logical database design was built in order to transform the database into its 
most atomic and innate form so all the relevant information is easily accessible. With the study 
of real-world student insurance companies such as JCB Insurance Solution, possible business 
problems were identified. These are in functional areas such as Marketing/Sales, 
Finance/Budgeting and Customer Service/Support which were resolved using SQL. Collectively, 
ScholaSure’s database is thoroughly analyzed, upgraded, and fine-tuned to enhance its efficiency 
and effectiveness in managing extensive data.

II. Background 

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
has received the necessary services, the provider submits the insurance claims for reimbursement to ScholaSure. 
If the student had obtained the services without the coverage verification or had 
paid for a medical care out of pocket, the student is able to submit the insurance claim for 
reimbursement only if the provider is in-network. Out-of-network provider’s claim applications 
are not accepted by ScholaSure. ScholaSure’s team carefully reviews these claims, and eligible 
expenses are promptly reimbursed to the provider or the student if they paid out of pocket. 
Throughout this process, they maintain open and transparent communication with both students 
and providers. In summary, their business operations focus on efficiently connecting insured students from the 
partnered educational institutions with a vast network of reputable healthcare and pharmacy 
providers.

IV. Project Scope & Objectives

In order to create a proper DBMS we decided to use Microsoft Access. This allowed each 
member to individually create the tables and easily modify them to our needs. Once all data 
tables were created, Access was imported via Excel tool, which allowed easy implementation of 
our database. 

V. Business Rules Relevant to Data Model

a. STUDENT and SCHOOL Relationship

Each SCHOOL must have at least one STUDENT.

Each STUDENT is enrolled in one and only one SCHOOL.

This business rule enforces a one-to-many relationship between the entities SCHOOL and 
STUDENT. It mandates that each SCHOOL entity must have at least one related STUDENT 
entity, ensuring there are no schools without students. Additionally, it specifies that each 
STUDENT can only be enrolled in one school. This is as per ScholaSure’s registration form, 
where students have the option to enroll for insurance under only one school. 

b. STUDENT and INSURANCE Relationship

Each STUDENT must have at least one INSURANCE. 

Each INSURANCE must have one and only one STUDENT. 

Students have only one insurance plan for a given time period (term) however, if they want to, 
there is an option to enroll in upcoming terms. When that happens, a new insurance policy 
number is generated for the student so that’s why there is one to many relationship between 
student and insurance table.

c. INSURANCE and MEDICAL Relationship

Each INSURANCE may have none or many MEDICAL RECORD.

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

d. INSURANCE and PHARMACY Relationship

An INSURANCE may have many Prescription or none.

A Prescription will work with one and only one INSURANCE.

A PHARMACY may file many Prescription or none. 

Each Prescription must have one and only one PHARMACY.

There is a many-to-many relationship between INSURANCE and PHARMACY, which is 
resolved using the Prescription associative entity. Similar to the INSURANCE and MEDICAL 
relationship, the insured students may or may not have a claim with the many pharmacy stores 
that are in Scholasure’s network. 

e. INSURANCE and TIER

Each INSURANCE has one and only one Tier

Each Tier must have at least one Insurance

There is a mandatory one to many relationship between Insurance and Tier. Each insurance plan 
for a student has only one type of tier which may be bronze, silver, gold or platinum. And, each 
tier is at least enrolled by one student as per the ScholaSure, ensuring there is a necessity and 
demand for each tier.

VI. Data Model 

A. ERD

![A-01](https://github.com/llamacorn118/InsuranceProject/assets/153336914/544d2bae-2161-47e9-94cb-046863824f76)

VII. Queries

Marketing & Sales

1. Gender Demographics
   
Description: This shows crucial information about the enrollment in each insurance tier and 
also accounts for the enrollment figures of men and women. This can be helpful demographics 
information for the marketing team to understand the target customer type. 

`SELECT S.GENDER, COUNT (S.GENDER) AS NumberOfStudents, i.insurance_tier AS 
TypeOfInsurance FROM STUDENT S INNER JOIN INSURANCE I ON S.STU_ID = 
I.STU_ID 
GROUP BY S.Gender, I.Insurance_Tier`

![A-02](https://github.com/llamacorn118/InsuranceProject/assets/153336914/3e70e86b-ca13-43bf-8f7b-68130487c7c8)

Finance & Budgeting

2. Total Revenue/Cost
   
Description: The goal of this query is to find the total revenue generated from student 
enrollment into the four tiers which is displayed under the Total_Insurance_Cost. To compare 
those results, the total_patient_cost shows the sum of medical bills that have been captured 
under each tier by all the students. Both of the information together could help the financial 
department to see the difference between the income compared to the potential cost for the 
company in reimbursements. 

`SELECT i.Insurance_Tier,
 SUM(i.Insurance_Cost) AS Total_Insurance_Cost,
 SUM(m.Patient_Cost) AS Total_Patient_Cost,
 SUM(i.Insurance_Cost)-SUM(m.Patient_Cost) AS Difference
FROM Insurance i
INNER JOIN Medical_Record m ON i.Insurance_policy_number = 
m.Insurance_policy_number
GROUP BY i.Insurance_Tier;`

![A-03](https://github.com/llamacorn118/InsuranceProject/assets/153336914/ba991bdb-2f76-4e9a-b295-b62acba1e350)

3. Students whose total medical cost exceeds that of an average student
   
Description: The query takes a look at each insurance policy and calculates the total medical 
cost. A correlated subquery is then used to calculate the average total cost of each policy. This 
allows us to see which students may potentially need higher coverage. 

`SELECT s.STU_ID, s.STU_FN, s.STU_LN, sum(mr.Total_Cost) AS Total_Medical_Cost
FROM MEDICAL_RECORD mr, Insurance i, STUDENT s where s.STU_ID = i.STU_ID
and mr.insurance_policy_number = i.insurance_policy_number and
mr.Total_Cost >= ( select avg(mr.Total_Cost) FROM MEDICAL_RECORD med where 
med.insurance_policy_number = mr.insurance_policy_number GROUP BY 
med.insurance_policy_number)
GROUP BY s.STU_ID, s.STU_FN, s.STU_LN, mr.insurance_policy_number;`

![A-04](https://github.com/llamacorn118/InsuranceProject/assets/153336914/a2303a73-c569-46af-ab7c-9cb0d281945f)

4. Insurance policies that do not have a medical record
   
Description: This query uses a left join to include any insurance policies that do not have a 
medical record to show the list of students who have zero claims. 

`Insurance policies that do not have Medical records.
Select I.Insurance_policy_number, STU_ID, Insurance_Cost, Insurance_Term, Insurance_Tier 
from INSURANCE I
Left Join Medical_Record M
on I.Insurance_policy_number = M.Insurance_policy_number
where Medical_ID is null`

![A-05](https://github.com/llamacorn118/InsuranceProject/assets/153336914/7c058a74-aa18-46a8-8273-b462e83aba73)

Customer Service & Support

5. Premium Insurance-Covered Pharmacies
   
Description: The below query retrieves pharmacy names, city and the insurance tier that were 
used by the students. This identifies pharmacies that have specifically accepted a Gold and 
Platinum type of insurance. From an operational perspective, this would be deemed vital 
information as it shows which type of insurance policies are most accepted by certain pharmacies. 
From the results, it can be observed that CVS is more likely to accept Gold insurance while 
Walgreen has greater tendency to accept Scholasure's Platinum insurance policy. This would help 
direct future operations, especially to assist students, leading to an improved customer service. 

`SELECT
p.pharmacy_name,
p.pharmacy_city,
i.insurance_tier
FROM Pharmacy p, prescription pr, Insurance i
where p.pharmacy_id = pr.pharmacy_id
and pr.Insurance_policy_number = i.Insurance_policy_number
and i.insurance_tier IN ('GOLD', 'PLATINUM')
ORDER BY i.insurance_tier;`

![A-06](https://github.com/llamacorn118/InsuranceProject/assets/153336914/58d5f466-840e-4964-92d5-09d43098b984)

6. Prescriptions that were ordered in the last quarter of the current year
    
Description: This table looks up recent prescriptions refills using the current financial quarter 
as a reference. Joins are used in this query to display the student and pharmacy involved in the 
refill. This allows us to see more recent data on what pharmacy brands are preferred. Students 
demonstrate a preference towards Walgreens in contrast to CVS and Rite Aid.

`SELECT P.Insurance_policy_number, Pharmacy_Name, STU_FN, STU_LN
FROM
PRESCRIPTION P, STUDENT S, INSURANCE I, PHARMACY PH
WHERE P.Pharmacy_ID = PH.Pharmacy_ID
and P.Insurance_policy_number = I.Insurance_policy_number
and I.STU_ID = S.STU_ID and
prescription_date >= 10/01/2023
or prescription_date <= 12/31/2023;`

![A-07](https://github.com/llamacorn118/InsuranceProject/assets/153336914/2a5664d5-7a40-4481-8f79-8fcef9ce8c77)

VIII. Business Recommendation

Enhancing Database Functionality: 

While the database is operational, there are certain elements that can be added to make it more 
effective. 
(i) Adding a column in Medical Record and Prescription tables to specify if claims are 
submitted by students or in-network providers. This will help track student reliance on innetwork providers for claim submissions. 

(ii) Allowing students to submit claims for out-of-network providers and maintaining a list in a 
separate table. Though this is currently unaccepted by ScholaSure, this additional data will 
reveal frequently used out-of-network providers, aiding potential future partnerships for 
network expansion.

(iii) Expanding student table details to include demographics like age, income, education, 
occupation, family size, and ethnicity. This provides richer customer insights for targeted 
marketing campaigns by the marketing team.

- END -
