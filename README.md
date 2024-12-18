### 1. Selezionare tutti gli studenti nati nel 1990 (160)

```SQL
SELECT *
FROM `students`
WHERE `date_of_birth` LIKE '1990-%-%';
```

### 2. Selezionare tutti i corsi che valgono più di 10 crediti (479)

```SQL
SELECT *
FROM `courses`
WHERE `cfu` > '10';
```

### 3. Selezionare tutti gli studenti che hanno più di 30 anni

```SQL
SELECT *
FROM `students`
WHERE `date_of_birth` < DATE_SUB(CURDATE(), INTERVAL 30 YEAR);
```

### 4. Selezionare tutti i corsi del primo semestre del primo anno di un qualsiasi corso di laurea (286)

Primo semestre del primo anno di un corso di laurea in particolare

```SQL
SELECT *
FROM `courses`
JOIN `degrees` ON `courses`.`degree_id` = `degrees`.`id`
WHERE `period` = 'I semestre'
AND `year` = '1'
AND `degrees`.`name` = 'Corso di Laurea in Biologia';
```

Primo semestre del primo anno di tutti i corsi di laurea

```SQL
SELECT *
FROM `courses`
WHERE `period` = 'I semestre'
AND `year` = '1';
```

### 5. Selezionare tutti gli appelli d'esame che avvengono nel pomeriggio (dopo le 14) del 20/06/2020 (21)

```SQL
SELECT *
FROM `exams`
WHERE `date` = '2020-06-20'
AND `hour` > '14-00-00';
```

### 6. Selezionare tutti i corsi di laurea magistrale (38)

```SQL
SELECT *
FROM `degrees`
WHERE `level` = 'magistrale';
```

### 7. Da quanti dipartimenti è composta l'università? (12)

```SQL
SELECT COUNT(*) AS `departments_number`
FROM `departments`;
```

### 8. Quanti sono gli insegnanti che non hanno un numero di telefono? (50)

```SQL
SELECT COUNT(*) AS `teachers_with_phone`
FROM `teachers`
WHERE `phone` IS NOT NULL;
```

### 9. Inserire nella tabella degli studenti un nuovo record con i propri dati (per il campo degree_id, inserire un valore casuale)

```SQL
INSERT INTO `students`
(`degree_id`, `name`, `surname`, `date_of_birth`, `fiscal_code`, `enrolment_date`, `registration_number`, `email`)
VALUES
(1, 'Gabriele', 'Tuzzo', '1999-05-31', 'TZZGRL99G31E273Z', '2018-06-10', '621033', 'gabriele.tuzzo@gmail.com');
```

### 10. Cambiare il numero dell’ufficio del professor Pietro Rizzo in 126

```SQL
UPDATE `db-university`.`teachers`
SET `office_number` = '126'
WHERE (`name` = 'Pietro')
AND (`surname` = 'Rizzo');
```

### 11. Eliminare dalla tabella studenti il record creato precedentemente al punto 9

```SQL
DELETE FROM `db-university`.`students`
WHERE (`name` = 'Gabriele')
AND (`surname` = 'Tuzzo');
```
