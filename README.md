Esercizio di oggi: nome repo: db-university
Dopo aver creato un nuovo database nel vostro phpMyAdmin e aver importato lo schema allegato, eseguite le query del file allegato.
Cosa consegnare? Nella stessa repo dell'esercizio di ieri, dopo aver testato le vostre query con phpMyAdmin, riportatele in un file txt o nel file README.md e caricatelo nella vostra repo.
Numero push: 1 per ogni query.
Le query 9,10,11 sono da considerarsi bonus


RICHIESTE

1. Selezionare tutti gli studenti nati nel 1990 (160)
2. Selezionare tutti i corsi che valgono più di 10 crediti (479)
3. Selezionare tutti gli studenti che hanno più di 30 anni
4. Selezionare tutti i corsi del primo semestre del primo anno di un qualsiasi corso di
laurea (286)
5. Selezionare tutti gli appelli d'esame che avvengono nel pomeriggio (dopo le 14) del
20/06/2020 (21)
6. Selezionare tutti i corsi di laurea magistrale (38)
7. Da quanti dipartimenti è composta l'università? (12)
8. Quanti sono gli insegnanti che non hanno un numero di telefono? (50)
9. Inserire nella tabella degli studenti un nuovo record con i propri dati (per il campo
degree_id, inserire un valore casuale)
10. Cambiare il numero dell’ufficio del professor Pietro Rizzo in 126
11. Eliminare dalla tabella studenti il record creato precedentemente al punto 9



SOLUZIONI

1. 
SELECT *
FROM `students`
WHERE YEAR(`date_of_birth`) = 1990;

2.
SELECT *
FROM `courses`
WHERE `cfu` > 10;

3.
SELECT *
FROM `students` 
WHERE TIMESTAMPDIFF(YEAR, `date_of_birth`, CURDATE()) > 30;

4.
SELECT * 
FROM `courses` 
WHERE `period` LIKE 'I semestre'
AND `year` = 1;

5.
SELECT * 
FROM `exams`
WHERE  `hour` > '14:00:00'
AND `date` LIKE '2020-06-20';

6.
SELECT * 
FROM `degrees` 
WHERE `level` LIKE 'magistrale';

7.
SELECT COUNT(*) AS `deparments_university`
FROM `departments`;

8.
SELECT COUNT(*) AS `no_phone_number`
FROM `teachers` 
WHERE `phone` IS NULL ; 

9.
INSERT INTO `students`(`degree_id`, `name`, `surname`, `date_of_birth`, `fiscal_code`, `enrolment_date`, `registration_number`, `email`) VALUES (9,'Rivaldo','Gjoni','1998-02-28','GJNRLD98B28Z100O','2024-09-12','7777777','rivaldogjoni1998@gmail.com');

10.
UPDATE `teachers` 
SET `office_number`= 126
WHERE `name` LIKE 'Pietro'
AND `surname` LIKE 'Rizzo'

11.
DELETE FROM `students` 
WHERE `fiscal_code` LIKE 'GJNRLD98B28Z100O';


Ciao a tutti
Utilizzando lo stesso database di ieri, eseguite le query in allegato. Caricate un secondo file nella stessa repo di ieri (db-university) con le query di oggi.
Numero push: uno per ogni query

GROUP BY

1.
SELECT COUNT(*) AS `students_for_year`, YEAR(`enrolment_date`)
FROM `students`
GROUP BY YEAR(`enrolment_date`)

2.
SELECT COUNT(*) AS `office_adress_common`, `office_address`
FROM `teachers`
GROUP BY office_address

3.
SELECT AVG(vote), `exam_id`
FROM `exam_student`
GROUP BY `exam_id`

4.
SELECT COUNT(*) as `course_for_deparments`, `department_id`
FROM `degrees`
GROUP BY `department_id`


JOIN

1.
SELECT `students`.*
FROM `students`
JOIN `degrees` ON `students`.`degree_id`=`degrees`.`id`
WHERE `degrees`.`name` LIKE 'Corso di Laurea in Economia';

2.
SELECT `degrees`.*
FROM `degrees`
JOIN `departments` ON `degrees`.`department_id`=`departments`.`id`
WHERE `degrees`.`level` LIKE 'magistrale'
AND `departments`.`name` LIKE 'Dipartimento di Neuroscienze'

3.
SELECT `courses`.`name` AS 'Flavio_Amato_courses'
FROM `courses`
JOIN `course_teacher`ON `courses`.`id` = `course_teacher`.`course_id`
JOIN `teachers` ON `teachers`.`id` = `course_teacher`.`teacher_id`
WHERE `teachers`.`id` = 44

4.
SELECT `students`.`surname`, `students`.`name`, `departments`.`name` AS name_department, degrees.name AS name_degree
FROM `students`
JOIN `degrees` ON `students`.`degree_id` = `degrees`.`id`
JOIN `departments` ON `degrees`.`department_id` = `departments`.`id`
ORDER BY `students`.`surname`, `students`.`name`

5.
SELECT `degrees`.`name` AS `name_degree`, `courses`.`name` AS `name_course`, `teachers`.`name` AS `name_teacher`, `teachers`.`surname` AS `surname_teacher`
FROM `degrees`
JOIN `courses` ON `courses`.`degree_id` = `degrees`.`id`
JOIN `course_teacher` ON `course_teacher`.`course_id` = `courses`.`id`
JOIN `teachers` ON `course_teacher`.`teacher_id` = `teachers`.`id`
ORDER BY `name_degree`, `name_course`;




