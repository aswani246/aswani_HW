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




