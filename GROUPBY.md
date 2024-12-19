### 1. Contare quanti iscritti ci sono stati ogni anno

```SQL
SELECT
    YEAR(`enrolment_date`) AS `enrolment_year`,
    COUNT(*) AS `student_count`
FROM `db-university`.`students`
GROUP BY YEAR(`enrolment_date`)
ORDER BY `enrolment_year`;
```

### 2. Contare gli insegnanti che hanno l'ufficio nello stesso edificio

```SQL
SELECT COUNT(*) AS `teacher_count`, `teachers`.`office_number`
FROM `db-university`.`teachers`
GROUP BY `office_number`;
```

### 3. Calcolare la media dei voti di ogni appello d'esame

```SQL
SELECT `e`.`date`, `e`.`hour`, `e`.`location`,`e`.`address`, AVG(`vote`) AS `average_vote`
FROM `exams` AS `e`
LEFT JOIN `exam_student`
ON `e`.`id` = `exam_student`.`exam_id`
GROUP BY
    `e`.`date`, `e`.`hour`, `e`.`location`, `e`.`address`;
```

### 4. Contare quanti corsi di laurea ci sono per ogni dipartimento

```SQL
SELECT `d`.`name`, COUNT(*) AS `degrees_number`
FROM `departments` AS `d`
LEFT JOIN `degrees`
ON `d`.`id` = `degrees`.`department_id`
GROUP BY `d`.`name`;
```
