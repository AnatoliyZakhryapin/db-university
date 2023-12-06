1. Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia
    SELECT `students`.`id` as `student_id`, `students`.`name`, `students`.`surname`, `degrees`.`name` as `degree_name`
    FROM `students`
    INNER JOIN `degrees`
    ON `degrees`.`id` = `students`.`degree_id`
    WHERE `degrees`.`name` = 'Corso di Laurea in Economia';
2. Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di
Neuroscienze
    SELECT `degrees`.`id` as `degrees_id`, `degrees`.`name` as `degrees_name`, `degrees`.`level` as `degrees_level`, `departments`.`id` as `departments_id`, `departments`.`name` as `departments_name`
    FROM `degrees`
    INNER JOIN `departments`
    ON `departments`.`id` = `degrees`.`department_id`
    WHERE `degrees`.`level` = 'magistrale'
    AND `departments`.`name` = 'Dipartimento di Neuroscienze';
3. Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)
    SELECT `teachers`.`id` as `teachers_id`, concat(`teachers`.`name`, ' ',`teachers`.`surname`) as `fullname`, `course_teacher`.`course_id` as `course_id`, `courses`.`name` as `course_name`
    FROM `teachers`
    INNER JOIN `course_teacher`
    ON `course_teacher`.`teacher_id` = `teachers`.`id`
    INNER JOIN `courses`
    ON `courses`.`id` = `course_teacher`.`course_id`
    WHERE `teachers`.`name` = 'Fulvio'
    AND `teachers`.`surname` = 'Amato';
4. Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui
sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e
nome
    SELECT `students`.`id` as `student_id`, `students`.`surname`,`students`.`name`, `students`.`degree_id`, `degrees`.`name` as `degree_name`, `departments`.`name` as `department_name`
    FROM `students`
    INNER JOIN `degrees`
    ON `degrees`.`id` = `students`.`degree_id`
    INNER JOIN `departments`
    ON `departments`.`id` = `degrees`.`department_id`
    ORDER BY `students`.`surname`, `students`.`name` ASC;
5. Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti
    SELECT `degrees`.`name` as `degree_name`, `courses`.`name` as `course_name`, `teachers`.`name` as `teacher_name`, `teachers`.`surname` as `teacher_surname`
    FROM `degrees`
    INNER JOIN `courses`
    ON `courses`.`degree_id` = `degrees`.`id`
    INNER JOIN `course_teacher`
    ON `course_teacher`.`course_id` = `courses`.`id`
    INNER JOIN `teachers`
    ON `teachers`.`id` = `course_teacher`.`teacher_id`
    ORDER BY `degree_name`;
6. Selezionare tutti i docenti che insegnano nel Dipartimento di
Matematica (54)
    SELECT DISTINCT `departments`.`name` as `department_name`, `teachers`.`name` as `teacher_name`, `teachers`.`surname` as `teacher_surname`
    FROM `departments`
    INNER JOIN `degrees`
    ON `degrees`.`department_id` = `departments`.`id`
    INNER JOIN `courses`
    ON `courses`.`degree_id` = `degrees`.`id`
    INNER JOIN `course_teacher`
    ON `course_teacher`.`course_id` = `courses`.`id`
    INNER JOIN `teachers`
    ON `teachers`.`id` = `course_teacher`.`teacher_id`
    WHERE `departments`.`name` = 'Dipartimento di Matematica';
7. BONUS: Selezionare per ogni studente il numero di tentativi sostenuti
per ogni esame, stampando anche il voto massimo. Successivamente,
filtrare i tentativi con voto minimo 18.
    SELECT `students`.`id`, `students`.`name`, `students`.`surname`, `courses`.`name` as `course_name`, `courses`.`id` AS `course_id`,
    COUNT(*) AS `numero_tentativi`, MAX(`vote`) AS `max_vote` 
    FROM `students`
    INNER JOIN `exam_student` ON `students`.`id` = `exam_student`.`student_id`
    INNER JOIN `exams` ON `exams`.`id` = `exam_student`.`exam_id`
    INNER JOIN `courses` ON `courses`.`id` = `exams`.`course_id`
    GROUP BY `students`.`id`, `courses`.`id`
    HAVING `max_vote` >= 18
    ORDER BY `students`.`id` ASC;