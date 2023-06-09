# DIAGRAM

![Diagram](diagram.png)

# Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia

```sql
SELECT `students`.* 
FROM `degrees`
JOIN `students`
ON `degrees`.`id` = `students`.`degree_id`
WHERE `degrees`.`id` = 53;
```

# Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienze

```sql
SELECT `degrees`.*
FROM `degrees`
JOIN `departments` 
ON `departments`.`id` = `degrees`.`department_id`
WHERE `degrees`.`level` = 'magistrale'
AND `departments`.`name` = 'Dipartimento di Neuroscienze';
```

# Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)

```sql
SELECT `courses`.*
FROM `teachers` 
JOIN `course_teacher` 
ON `teachers`.`id` = `course_teacher`.`teacher_id` 
JOIN `courses` ON `course_teacher`.`course_id` = `courses`.`id` 
WHERE `teachers`.`id` = 44; 

```

# Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome

```sql
SELECT `students`.`surname`, `students`.`name`, `degrees`.`name` AS `degree_name`, `departments`.`name` AS `department_name`
FROM `students`
JOIN `degrees` 
ON `students`.`degree_id` = `degrees`.`id`
JOIN `departments` 
ON `degrees`.`department_id` = `departments`.`id`
ORDER BY `students`.`surname`, `students`.`name`;
```

# Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti

```sql
SELECT `degrees`.`name` AS `corso_di_laurea`, `teachers`.`name` AS `nome_insegnante`, `teachers`.`surname` AS `cognome_insegnante`, `courses`.`name` AS `corso`
FROM `degrees` 
JOIN `courses` 
ON `degrees`.`id` = `courses`.`degree_id`
JOIN `course_teacher` 
ON `courses`.`id` = `course_teacher`.`course_id`
JOIN `teachers` 
ON `course_teacher`.`teacher_id` = `teachers`.`id`
ORDER BY `degrees`.`name`, `cognome_insegnante`;
```

# Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54)

```sql
SELECT DISTINCT `teachers`.*
FROM `teachers`
JOIN `course_teacher` 
ON `course_teacher`.`teacher_id` = `teachers`.`id`
JOIN `courses` 
ON `courses`.`id` = `course_teacher`.`course_id`
JOIN `degrees` 
ON `degrees`.`id` = `courses`.`degree_id`
JOIN `departments` 
ON `departments`.`id` = `degrees`.`department_id`
WHERE `departments`.`name` = 'Dipartimento di Matematica';
```