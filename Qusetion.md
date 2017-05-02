1.統計每一門課程的最高分、最低分
select cno, max(score), min(score) 
from sc
group by cno;

2.查看和編號001的學生至少選了同一門課程的學生的姓名
SELECT sname
FROM student 
JOIN sc ON (sc.sno= student.sno)
WHERE sc.sno<>'s001' AND sc.cno IN
(
SELECT cno
FROM sc
WHERE sno = 's001'
)
GROUP BY sname

3.
SELECT sc.sno ,COUNT(cno) 
FROM sc 
JOIN student ON(sc.sno = student.sno) 
WHERE sc.sno<>'s002' AND sc.cno IN
( 
  SELECT cno FROM sc WHERE sno = 's002' 
) 
GROUP BY sc.sno
