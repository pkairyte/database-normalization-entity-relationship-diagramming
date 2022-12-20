# Data Normalization and Entity-Relationship Diagramming

## Inital Data and problems
The initial data provided for this excercise follows 1NF as looks as follows:

### Original table
| assignment_id | student_id | due_date | professor | assignment_topic                | classroom | grade | relevant_reading    | professor_email   |
| :------------ | :--------- | :------- | :-------- | :------------------------------ | :-------- | :---- | :------------------ | :---------------- |
| 1             | 1          | 23.02.21 | Melvin    | Data normalization              | WWH 101   | 80    | Deumlich Chapter 3  | l.melvin@foo.edu  |
| 2             | 7          | 18.11.21 | Logston   | Single table queries            | 60FA 314  | 25    | Dümmlers Chapter 11 | e.logston@foo.edu |
| 1             | 4          | 23.02.21 | Melvin    | Data normalization              | WWH 101   | 75    | Deumlich Chapter 3  | l.melvin@foo.edu  |
| 5             | 2          | 05.05.21 | Logston   | Python and pandas               | 60FA 314  | 92    | Dümmlers Chapter 14 | e.logston@foo.edu |
| 4             | 2          | 04.07.21 | Nevarez   | Spreadsheet aggregate functions | WWH 201   | 65    | Zehnder Page 87     | i.nevarez@foo.edu |
| ...           | ...        | ...      | ...       | ...                             | ...       | ...   | ...                 | ...               |

The initial dataset does not meet the 4NF and has many problems embeded. First of all, although it does satisfy the 2NF it does not meet the requirements for 3NF due to the following issues:
- Grades depend of student_id, while each student_id has different grades.
- Due_date, assignment_topic, relevant_reading depend on assignment_id, while each assignment_id has different data.
- Classroom, professor_email depend on professor, while each professor has different classroom and professor_email

## Approach to making the data 4NF compliant
In order to make this data compliant with 4NF, we have fix the above mentioned problems by makeing separate tables with separate id and data that descibes on entities in the table. For that purpose, we will need three tables split by Student, Professor, and Assignment. The tables look like this:

### Student Table

|   id    | student_id | assignment_id | grade |
| :------ | :--------- | :------------ | :---- |
| 1       | 1          | 1             | 80    |
| 2       | 7          | 2             | 25    |
| 3       | 4          | 1             | 75    |
| 4       | 2          | 3             | 92    |
| 5       | 2          | 4             | 65    |
| ...     | ...        | ...           | ...   |

### Professor Table

| professor_id  | professor  |classroom | professor_email   |
| :------------ | :--------  |:-------- | :---------------- |
| 1             | Melvin     | WWH 101  | l.melvin@foo.edu  |
| 2             | Logston    | 60FA 314 | e.logston@foo.edu |
| 3             | Nevarez    | WWH 201  | i.nevarez@foo.edu |
| ...           | ...        | ...      | ...               |

### Assignment Table

| assignment_id   | due_date | assignment_topic                |relevant_reading    | professor_id |
| :-------------- | :--------| :------------------------------ |:------------------ | :----------- |
|    1            | 23.02.21 | Data normalization              |Deumlich Chapter 3  | 1            |
|    2            | 18.11.21 | Single table queries            |Dümmlers Chapter 11 | 2            |
|    3            | 05.05.21 | Python and pandas               |Dümmlers Chapter 14 | 2            |
|    4            | 04.07.21 | Spreadsheet aggregate functions |Zehnder Page 87     | 3            |
|    ...          | ...      | ...                             | ...                | ...          |


As we can see from these three new tables, they are now compliant with 4NF form, since each column that was dependent on different fields is moved to separate tables, making non-key fields dependent on and describing only one entity. By connecting the tables though identical ids for primary keys, we connect the tables together making it easy to access all the information needed. Implementing this approach we have fixed the above mentioned issues with the original data making it compliant to 4NF, by satisfying the requirements of 3NF and making sure that data does not contain more than one independent multi-valued fact about entitiy. More detailed diagram explaining the relationship between entities and data can be seen bellow.

Here is the ER-diagram for tables in 4NF.
![Placeholder E-R Diagram](./images/ER_Diagram.svg)