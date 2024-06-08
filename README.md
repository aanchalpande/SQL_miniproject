# SQL_miniproject
CREATE DATABASE Student_management;
USE Student_management;

CREATE table Students (
  student_id INT PRIMARY KEY,student_name VARCHAR(100),date_of_birth DATE,email VARCHAR(100),
  major VARCHAR(50));

CREATE table Courses (course_id CHAR(4) PRIMARY KEY,course_name VARCHAR(100),credit_hours INT,
  instructor VARCHAR(100));

INSERT INTO Students (student_id, student_name, date_of_birth, major) 
 VALUES (1, 'John Doe', '1998-07-15',  'Computer Science');
INSERT INTO Students (student_id, student_name, date_of_birth, major) 
VALUES (2, 'Jane Smith', '1999-03-22', 'Mathematics');
INSERT INTO Students (student_id, student_name, date_of_birth, email, major)
 VALUES (3, 'Michael Johnson', '2000-11-08', 'michael.johnson@gmail.com', 'Computer Science');
INSERT INTO Students (student_id, student_name, date_of_birth, email, major)
 VALUES (4, 'Emily Williams', '2001-05-01', 'emily.williams@gmail.com', 'Physics');

INSERT INTO Courses (course_id, course_name, credit_hours, instructor) 
VALUES ('C101', 'Database Management', 3, 'Prof. Brown');
INSERT INTO Courses (course_id, course_name, credit_hours, instructor) 
VALUES ('C102', 'Programming Fundamentals', 4, 'Prof. White');
INSERT INTO Courses (course_id, course_name, credit_hours, instructor) 
VALUES ('C103', 'Calculus I', 4, 'Prof. Smith');
INSERT INTO Courses (course_id, course_name, credit_hours, instructor)
 VALUES ('C104', 'Physics I', 4, 'Prof. Johnson');
 
 select * from students;
 select * from courses;

Select * from students
where major = "Computer Science";


Select * from students
where  date_of_birth < 2000-01-01 ;

select * from courses
where instructor="Prof. White";

select  major, count(student_id) from students
group by major;



SELECT * FROM courses
where credit_hours = (select max(credit_hours) from courses);

SELECT * FROM students
where date_of_birth = (select min(date_of_birth) from students);

SELECT * FROM students
where date_of_birth = (select max(date_of_birth) from students);

INSERT INTO Courses (course_id, course_name, credit_hours, instructor) VALUES ('C105', 
'Python', 5, 'Prof. White');
SELECT * FROM courses;

INSERT INTO Students (student_id, student_name, date_of_birth, email, major) 
VALUES (8, 'Rohit Sharma', '2001-03-12', 'steve.smith@gmail.com', 'Physics');
SELECT * FROM students;

update students
SET email = 'john.doe@yahoo.com'
WHERE student_id = 1;

update students
set email = "noreply@gmail.com"
where email is null;
SELECT * FROM students;


CREATE TABLE enrollments (
  student_id INT,
  course_id CHAR(4)
);

desc enrollments;

ALTER TABLE enrollments ADD PRIMARY KEY (student_id, course_id);

INSERT INTO enrollments (student_id, course_id) values (1,'C101');
INSERT INTO enrollments (student_id, course_id) values (1,'C102');
INSERT INTO enrollments (student_id, course_id) values (1,'C105');
INSERT INTO enrollments (student_id, course_id) values (2,'C103');
INSERT INTO enrollments (student_id, course_id) values (3,'C101');
INSERT INTO enrollments (student_id, course_id) values (3,'C102');
INSERT INTO enrollments (student_id, course_id) values (3,'C105');
INSERT INTO enrollments (student_id, course_id) values (4,'C104');
INSERT INTO enrollments (student_id, course_id) values (5,'C104');

SELECT * FROM enrollments;

1 | John Doe | Computer Science | C101 | Database Management | Prof.Brown
1 | John Doe | Computer Science | C102 | Programming Fundamentals | Prof.White
1 | John Doe | Computer Science | C105 | Python | Prof.White

select s.student_id, s.student_name, s.major, c.course_id, c.course_name, c.instructor
from students s
left join enrollments e
on s.student_id = e.student_id
left join courses c
on e.course_id = c.course_id
where s.major = "Computer Science";

select * from students
where student_id not in (select distinct student_id from enrollments);


SELECT * FROM students
WHERE student_id in (SELECT student_id FROM enrollments 
                      WHERE course_id = 'C103');

SELECT * FROM courses
WHERE course_id IN (SELECT course_id FROM enrollments 
                      GROUP BY course_id
                      HAVING count(*) > 1);
                      
SELECT course_id, count(*) FROM enrollments 
GROUP BY course_id

