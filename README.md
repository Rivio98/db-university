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

4.SELECT * 
FROM `courses` 
WHERE `period` LIKE 'I semestre'
AND `year` = 1;