# 3h-w
10 table  ddl &amp; dml


CREATE TABLE student
(
     Student_id   SERIAL   PRIMARY KEY     NOT NULL,
    name VARCHAR(50) NOT NULL,
    lastname VARCHAR(50) NOT NULL,
    age INT NOT NULL,
    mail VARCHAR(25) );

INSERT INTO student( name, lastname, age, mail)
VALUES ('Sarmat','Tynaibekov',22,null),
 ('Ainazik','Tynaibekova',22,'ff'),
 ('Samara','Maksatova',21, null);

SELECT * FROM  student;
SELECT Student_id, name FROM student WHERE age =22  and mail is   null ;
Delete from student where name='Sarmat';
drop table student;

CREATE TABLE Specialnost(
                           doljnost_id SERIAL PRIMARY KEY NOT NULL ,
                            doljnost varchar(25)  not null);
insert into Specialnost(doljnost_id,doljnost)
/*VALUES (1,'terapevt');*/
/*VALUES (2,'infeksionist');*/
VALUES (3,'terapevt');

 CREATE table Smena(
     smena_id int PRIMARY KEY ,
     start_at time not null,
     end_at time not null
 );
drop table smena;
alter table smena add end_at time;

INSERT INTO Smena
VALUES (1, '08:00', '18:00'),
       (2, '09:00', '22:00');

delete from smena;
select start_at - end_at from Smena where smena_id = 1;
select * from Smena where (Smena.end_at-Smena.start_at) >= interval '8 hours';

CREATE table Vrachi(
                      vrach_id SERIAL PRIMARY KEY not null ,
                       mame VARCHAR(10)not null ,
                       salary int not null ,
                       staj_raboty int ,
                       doljnost_id int,
                       smena_id int ,
                       constraint fk_specialnost
                       foreign key (doljnost_id)
                   references Specialnost(doljnost_id),
                   constraint fk_Smena
                   foreign key(smena_id)
                   references Smena(smena_id));

INSERT INTO Vrachi(vrach_id,mame,salary,staj_raboty,doljnost_id)
  /*VALUES (2,'Uulsana',20000,5,1);*/
  /*VALUES (1,'Kanymgul',30000,10,2);*/
  VALUES (11,'MArk',21000,2,3);
DELETE from Vrachi where staj_raboty <=2;
alter table Vrachi  add age int ;
UPDATE Vrachi SET mame  = 'Aiza' WHERE mame = 'Uulsana';
SELECT * from Vrachi;



CREATE table Obshejitie (
    id_obsh Serial PRIMARY KEY ,
    Name varchar(10),
    Etaj int ,
    kol_komnaty int ,
    student_id int ,
    vrach_id int ,
    constraint  fk_student
     foreign key (student_id)
                        references student(id),
                        constraint fk_Vrachi
                        foreign key (vrach_id)
                        references Vrachi(id)

);

insert into Obshejitie(id_obsh,Name,Etaj,nomer_komnaty,student_id,vrach_id)
VALUES (1,'Ekinchi',4,50,3,2),
       (2,'Uchunchu',5,60,4,1),
       (3,'Birinchi',3,40,5,1);

  SELECT * from Obshejitie
where Etaj<=4 OR student_id=3;

SELECT name from Obshejitie
ORDER BY Name desc ;

drop table Teacher;
CREATE  table  Teacher(
    id_teacher serial PRIMARY KEY ,
    teacher_name varchar(20) not null ,
    birth_day date ,
    staj_raboty int ,
    id_pasporta int unique);

alter table Teacher add check(id_pasporta >= 8);
drop table  Teacher;


 INSERT INTO Teacher(teacher_name, birth_day, staj_raboty, id_pasporta)
 values ('Anna','1997-06-01',3,11113355),
        ('sea','1978-08-01',5, 12121212),
        ('Ella','1989-03-05',5,   23454455  );
select * from Teacher;


 drop  table Pupil;
CREATE  table Pupil
(
    pupil_id   serial,
    pupil_name varchar(25) not null,
    age        int,
    grade      int
 constraint HK_Pupil CHECK (grade<=11 ));
 INSERT INTO Pupil(PUPIL_NAME, AGE, GRADE)
  VALUES ('Aidana', 15,9),
  ( 'Gulu', 8,1 ),
('Kkkk',12,8);

select *from Pupil;


drop table Grade;
Create  table Grade(
    grade_id  serial PRIMARY KEY ,
    grade int);
INSERT INTO Grade(grade)VALUES (1),(2),(3),(4),(5),(6),(7),(8),(9);
CREATE table Books (
                       nomer_knigi serial PRIMARY KEY ,
                       name varchar(50) ,
                       grade_id int ,
                       constraint fk_Grade
                   foreign key (grade_id)
                   references Grade(grade_id));

INSERT INTO Books(NAME, GRADE_ID) VALUES ('Fizika',6),('matematika',7),('Inf',8);


drop  table School;

CREATE  table  School(
    school_id  serial primary key ,
    school_name varchar(15) not null,
    student_id  int ,
    id_teacher int,
    nomer_knigi int ,
  grade_id int,
  constraint fk_student
 foreign key (student_id)
    references student(id),
    constraint fk_teacher
                     foreign key (id_teacher)
                     references Teacher(id_teacher),
                     constraint fk_Books
                     foreign key (nomer_knigi)
                     references Books(nomer_knigi));


INSERT INTO school(school_name, student_id, id_teacher,nomer_knigi,grade_id) VALUES
('Pushking',3,1,3,1),
('Manas',4,2,1,3),
('Kochkonov',5,3,1,2);


SELECT * from school;
Select school_name,id_teacher from  school;
delete  from school where school_name='Manas';
UPDATE school SET id_teacher  = 1 WHERE id_teacher =5;

