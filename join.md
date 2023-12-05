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
4. Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui
sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e
nome
5. Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti
6. Selezionare tutti i docenti che insegnano nel Dipartimento di
Matematica (54)
7. BONUS: Selezionare per ogni studente il numero di tentativi sostenuti
per ogni esame, stampando anche il voto massimo. Successivamente,
filtrare i tentativi con voto minimo 18.