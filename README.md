# aswani_HW--Q1: Count how many students passed the exam.

select
count(result_status)
from 
day_2_exam
where 
result_status = 'Pass'

--Q2: Find the average score of all students who failed.

select
Avg (total_score)
from
day_2_exam
where result_status = 'Fail'

--Q3: Get the highest score among all students.

select
max (total_score) As highest_score
from
day_2_exam

--Q4: Get the lowest score among passed students.

select
min(total_score) As lowest_passed_score
from
day_2_exam
where result_status = 'Pass'

--Q5: Sum the total marks of all students who scored above 40.

select
sum (total_score) As total_score
from
day_2_exam
where
total_score > 40;

--Q6: Count students by result status for those who scored 35 or more.

select
count (result_status) As student_count
from
day_2_exam
where
total_score >= 35
group by result_status;

--Q7: Find average score grouped by result status for students with scores between 30 and 40.

select
result_status,
Avg (total_score) As Average_score
from
day_2_exam
where
total_score between 30 and 40
group by result_status;

--Q8: Get maximum and minimum scores grouped by result status for students who scored less than 35.

select
result_status,
max (total_score) As max_score,
min (total_score) As min_score
from
day_2_exam
where total_score < 35
group by result_status;

--Q9: Count students grouped by result status for those whose names start with 'A'.

select
count (result_status) As student_count
from
day_2_exam
where student_name like 'A%'
group by result_status;--Q10: Sum total scores grouped by result status for students who scored exactly 35, 40, or 45.

select
result_status,
sum (total_score) As total_score
from
day_2_exam
where
total_score in (35,40,45)
group by result_status;

--Q11: Count students by each score value, ordered by score descending.

select
count (total_score) As student_count
from
day_2_exam
group by total_score
order by total_score desc;

--Q12: Show average score for each result status, ordered by average score.

select
result_status,
avg (total_score) As avg_score
from
day_2_exam
group by result_status
order by avg_score

--Q13: Count how many students got each score, only for scores above 30, ordered by frequency.

select
count (total_score) As frequency
from
day_2_exam
where
total_score > 30
group by total_score
order by frequency desc

--Q14: Get total marks sum for each result status, ordered by sum.

select
result_status,
sum (total_score) As total_score
from
day_2_exam
group by result_status
order by total_score

--Q15: Find minimum score for each result status, ordered by min score.

select
result_status,
min (total_score) As min_score
from
day_2_exam
group by result_status
order by min_score

--Q16: For passed students only, show count, average, max and min scores grouped by whether score is above 40.

select
count (hall_ticket_no) As student_count,
avg (total_score) As avg_score,
max (total_score) As max_score,
min (total_score) As min_score
from
day_2_exam
where result_status = 'Pass'

--Q17: Count and average score for each result status, only for scores not equal to 35.

select
result_status,
count (total_score) As student_count,
avg (total_score) As avg_score
from
day_2_exam
where total_score <> 35
group by result_status

--Q19: For each result status, show count of students with scores greater than 30 and less than 40.

select
result_status,
count( hall_ticket_no) As student_count
from
day_2_exam
where total_score > 30 and total_score < 40
group by result_status

DAY_3_HW
--Find the Average, Maximum, and Minimum marks obtained in the Day 1 Exam to see how the class performed as a whole.
select
AVG (total_score) As avrerage_marks,
MAX (total_score) As maximum_marks,
MIN (total_score) As minimum_marks
from day_1_exam

--List the names of MBA students who scored above 35 on Day 2.

select
t1.full_name,
t1.hall_ticket_no,
t2.total_score
from
"RSVP_New" As t1
join day_2_exam As t2
on t1.hall_ticket_no = t2.hall_ticket_no
where total_score > 35;

--Identify students whose Day 2 score was strictly higher than their Day 1 score.

select
t1.hall_ticket_no,
t1.total_score as day1,
t2.total_score as day2
from
day_1_exam as t1
join day_2_exam as t2
on t1.hall_ticket_no = t2.hall_ticket_no
where t2.total_score > t1.total_score
order by t1.hall_ticket_no;

--Do passing students work faster? Join day_2_exam with qaday2 to find the average 'Total Time' for students who 'Pass' vs those who 'Fail'.

select
case
when t1.total_score >= 30 then 'Pass'
else 'Fail'
end as result_status,
AVG(t2."Total Time") as avg_total_time
from day_2_exam as t1
join qaday2 as t2
on t1.hall_ticket_no = t2.hall_ticket_no
group by
case
when t1.total_score >= 30 then 'Pass'
else 'Fail'
end;

--If a student finished Question 1 (Q1) in under 15 seconds, they are 'Quick to Fall in Love.' If they took over 60 seconds, they are 'Hard to Get.' If they skipped (NULL), they are 'Focusing on their Career'.

select
hall_ticket_no,
Q1
CASE
WHEN Q1 IS NULL THEN 'Focusing on their Career'
WHEN Q1 < 15 THEN 'Quick to Fall in Love'
WHEN Q1 > 60 THEN 'Hard to Get'
ELSE 'Normal Pace'
END AS love_logic
from qaday2

--Get the full details from RSVP_New for the student who got the absolute maximum score on Day 2.(use subquery)

select *
from "RSVP_New"
where hall_ticket_no IN (select hall_ticket_no
from day_2_exam
where total_score = (select MAX(total_score)
from day_2_exam)
);

--Who registered for the class before 'AMENAH AHSAN'?(use subquery)

select
full_name,
created_at
from "RSVP_New"
where created_at < (select created_at
from "RSVP_New"
where full_name = 'AMENAH AHSAN')

--Show the details of students who are among the 5 fastest finishers of the Day 2 exam.

select
t1.hall_ticket_no,
t1.surname,
t1.full_name,
t1.contact_no,
t1.email,
t1.college_name
from "RSVP_New" as t1
where t1.hall_ticket_no in (select hall_ticket_no
from qaday2
order by "Total Time" asc
limit 5)




