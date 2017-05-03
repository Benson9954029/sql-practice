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

3.查看所選課程包含編號002的學生課程的學生的姓名、選課數量
SELECT student.sname,student.sno
FROM sc JOIN student ON (student.sno = sc.sno) 
WHERE sc.sno <>'s002' AND student.sname 
NOT IN (SELECT student.sname 
        FROM student 
        JOIN sc ON sc.sno = student.sno
        WHERE sc.cno NOT IN 
        (SELECT sc.cno FROM sc WHERE sno = 's002'))
GROUP BY student.sname,student.sno
HAVING COUNT(sc.cno) =(SELECT COUNT(sc.cno)
                      FROM sc 
                      WHERE sno = 's002'
                      GROUP BY sno)

SELECT student.sname,student.sno FROM student,
(SELECT sc.sno,COUNT(*) as samecourse_count FROM sc 
WHERE sc.sno <> 's002' AND cno IN (SELECT cno FROM sc WHERE sno ='s002')
GROUP BY sc.sno) t_others
LEFT JOIN (SELECT
          sc.sno,COUNT(*) as allcourse_count FROM sc
           GROUP BY sno) to_all 
           ON t_others.sno = to_all.sno
           WHERE t_others.sno = to_all.sno
           AND to_all.allcourse_count = t_others.samecourse_count
           AND to_all.allcourse_count = (SELECT COUNT(cno) FROM sc WHERE sno = 's002')
           ;
4查看每門課程的平均分，保留小數點後兩位
SELECT cno,ROUND(AVG(score),2) as Averageofscore FROM sc GROUP BY cno

5統計每名學生各門成績在60～90分的分布情況
SELECT sno,
SUM(CASE WHEN score >=90 THEN 1 ELSE 0 END) AS '>=90',
SUM(CASE WHEN score >=80 AND score <90 THEN 1 ELSE 0 END) AS '80~90',
SUM(CASE WHEN score >=70 AND score <80 THEN 1 ELSE 0 END) AS '70~80',
SUM(CASE WHEN score >=60 AND score <70 THEN 1 ELSE 0 END) AS '60~70',
SUM(CASE WHEN score <60 THEN 1 ELSE 0 END) AS '<60'
FROM sc
GROUP BY sno

6.統計每門課程的選課學生數量 
SELECT COUNT(*)
FROM sc
GROUP BY cno

7.查看只選了一門課的學生編號
SELECT sno
FROM sc
GROUP BY sno
HAVING COUNT(cno) = 1

8.學生性別情況統計 
SELECT ssex,COUNT(ssex)
FROM student
GROUP BY ssex
;

9.重名學生數量
SELECT sname
FROM student
GROUP BY sname
HAVING COUNT(*)>1
;

10統計每門課程平均分並按降序排列 
SELECT AVG(score) as avg_score
FROM sc GROUP BY cno
ORDER BY avg_score DESC

11查詢選了J2SE這門課程得分高於80分的學生姓名及成績
SELECT student.sname,sc.score
FROM sc 
JOIN course ON course.cno = sc.cno
JOIN student ON student.sno = sc.sno
WHERE cname = 'J2SE' AND sc.score >80

12查詢所有學生的得分情況
SELECT student.sname,score,course.cname
FROM sc
JOIN student ON student.sno = sc.sno
JOIN course ON course.cno=sc.cno
;

13-- 查詢每門課程得分最高的兩名學生姓名、得分、學生編號及課程號 
SELECT student.sname,sc_1.score,sc_1.sno,sc_1.cno
FROM sc AS sc_1,student
WHERE
(/*Count 數 小於二者*/
    SELECT COUNT(*)
    FROM sc AS sc_2 
    WHERE sc_1.cno = sc_2.cno
    AND sc_1.score>=sc_2.score
)<=2 AND student.sno = sc_1.sno
ORDER BY sc_1.cno ,sc_1.score DESC

14.-- 查詢每名學生得分在70分以上的課程名稱 
/*-- 查詢每名學生得分在70分以上的課程名稱 */
SELECT student.sname,course.cname
FROM sc,course,student
WHERE sc.sno = student.sno AND sc.cno = course.cno
AND sc.score >=70

15.-- 查詢所有成績都在70分以上的學生 
/*-- 查詢所有成績都在70分以上的學生*/
SELECT DISTINCT sno
FROM sc
WHERE sno NOT IN 
(
    SELECT sno FROM sc 
    WHERE score <70
)

16-- 統計選了c001、c002兩門課程且前者成績高於後者的學生姓名、編號、課程編號及得分
/*-- 統計選了c001、c002兩門課程且前者成績高於後者的學生姓名、編號、課程編號及得分*/
SELECT sname,sc_001.sno,sc_001.cno,sc_001.score,sc_002.score
FROM sc as sc_001,student
JOIN sc as sc_002
WHERE sc_001.cno = 'c001' AND sc_002.cno = 'c002'
AND sc_001.score > sc_002.score AND student.sno = sc_001.sno AND sc_001.sno = sc_002.sno

17-- 統計平均成績在60分以上的學生標號 
/*  統計平均成績在60分以上的學生標號   */
SELECT AVG(score) ,sno
FROM sc
GROUP BY sno
HAVING AVG(score)>60
;

18-- 統計每名學生編號、姓名、選課數量、總分 
/*-- 統計每名學生編號、姓名、選課數量、總分 */
SELECT sc.sno,student.sname,COUNT(cno),SUM(score)
FROM student
LEFT JOIN sc ON student.sno = sc.sno
GROUP BY student.sno
