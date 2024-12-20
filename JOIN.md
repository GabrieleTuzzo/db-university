### 1. Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia

```SQL
SELECT `students`.* , `d`.`name`
FROM `students`
INNER JOIN `degrees` AS `d`
ON `students`.`degree_id` = `d`.`id`
WHERE `d`.`name` = 'Corso di Laurea in Economia' ;
```

### 2. Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienze

```SQL
SELECT `dep`.`name` AS `department`, `degrees`.*
FROM `departments` AS `dep`
INNER JOIN `degrees`
ON `dep`.`id` = `degrees`.`department_id`
WHERE `dep`.`name` = 'Dipartimento di Neuroscienze'
AND `degrees`.`level` = 'magistrale';
```

### 3. Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)

```SQL
SELECT `teachers`.`name` , `teachers`.`surname`, `courses`.*
FROM `teachers`
INNER JOIN `course_teacher` AS `c_s` ON `teachers`.`id` = `c_s`.`teacher_id`
INNER JOIN `courses` ON `c_s`.`course_id` = `courses`.`id`
WHERE `teachers`.`id` = 44;
```

### 4. Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome

```SQL
SELECT `students`.`surname`, `students`.`name`, `degrees`.* , `departments`.*
FROM `students`
RIGHT JOIN `degrees` ON `students`.`degree_id` = `degrees`.`id`
RIGHT JOIN `departments` ON `degrees`.`department_id` = `departments`.`id`
ORDER BY `students`.`surname`, `students`.`name` ASC;
```

### 5. Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti

```SQL
SELECT `degrees`.`name` AS `degree_name`,
`courses`.`name` AS `course_name`,
`teachers`.`name` AS `teacher_name`,
`teachers`.`surname` AS `teacher_surname`
FROM `degrees`
INNER JOIN `courses` ON `degrees`.`id` = `courses`.`degree_id`
INNER JOIN `course_teacher` ON `courses`.`id` = `course_teacher`.`course_id`
INNER JOIN `teachers` ON `course_teacher`.`teacher_id` = `teachers`.`id`;
```

### 6. Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54)

```SQL
SELECT DISTINCT `teachers`.*
FROM `teachers`
INNER JOIN `course_teacher` AS `c_s` ON `teachers`.`id` = `c_s`.`teacher_id`
INNER JOIN `courses` ON `c_s`.`course_id` = `courses`.`id`
INNER JOIN `degrees` ON `courses`.`degree_id` = `degrees`.`id`
INNER JOIN `departments` ON `degrees`.`department_id` = `departments`.`id`
WHERE `departments`.`name` = 'Dipartimento di Matematica'
ORDER BY `teachers`.`name`;
```

### 7. BONUS: Selezionare per ogni studente il numero di tentativi sostenuti per ogni esame, stampando anche il voto massimo. Successivamente, filtrare i tentativi con voto minimo 18.

```SQL
SELECT
	`students`.`id`,
    `students`.`name`,
    `students`.`surname`,
    `courses`.`id` AS `course_id`,
    `courses`.`name` AS `course_name`,
    COUNT(*) AS `tries_number`,
    MAX(`exam_student`.`vote`) AS `max_vote`
FROM
    `students`
INNER JOIN
    `exam_student` ON `students`.`id` = `exam_student`.`student_id`
INNER JOIN
    `exams` ON `exam_student`.`exam_id` = `exams`.`id`
INNER JOIN
    `courses` ON `exams`.`course_id` = `courses`.`id`
GROUP BY
	`students`.`id`,
    `course_id`
HAVING `max_vote` >= 18
ORDER BY
    `students`.`name`;
```
