### Выполнил Августовский Андрей
___
### Задание номер 1
```sql
SELECT model ,  speed, hd  FROM pc  WHERE price < 500  
```
### Задание номер 2
```sql
SELECT maker FROM product WHERE product.type = 'printer' group by maker
```

### Задание номер 3
```sql
SELECT model , ram ,  screen FROM laptop WHERE price > 1000  
```

### Задание номер 4
```sql
SELECT * FROM printer WHERE color = 'y'  
```

### Задание номер 5
```sql
SELECT model ,speed , hd  FROM pc WHERE (cd = '12x' or cd = '24x') and price < 600  
Задание номер 6
```sql
SELECT DISTINCT product.maker, laptop.speed FROM product inner join laptop on product.model=laptop.model and laptop.hd>=10
```
### Задание номер 6
```sql
SELECT distinct p.maker as maker, l.speed as speed 
FROM laptop l join product p on l.model = p.model 
WHERE l.hd >= 10;
  
```

### Задание номер 7
```sql
SELECT laptop.model , laptop.price  FROM laptop inner join product on laptop.model = product.model  
WHERE product.maker= 'B' 
union 
SELECT pc.model , pc.price FROM pc inner join product on pc.model = product.model  
WHERE product.maker= 'B' 
union 
SELECT printer.model , printer.price FROM printer inner join product on printer.model = product.model  
WHERE product.maker= 'B' 
```

### Задание номер 8
```sql
SELECT maker from product WHERE type = 'pc' except SELECT maker FROM product 
WHERE type = 'laptop';
  
```

### Задание номер 9
```sql
SELECT maker  FROM pc inner join product on pc.model = product.model WHERE speed >= 450 
group by maker 
```

### Задание номер 10
```sql
SELECT model, price FROM printer WHERE price = (SELECT max(price) FROM printer)  
```

### Задание номер 11
```sql
SELECT avg (speed) FROM pc  
```

### Задание номер 12
```sql
SELECT avg(speed) FROM laptop WHERE price > 1000 
```

### Задание номер 13
```sql
SELECT avg(speed) FROM pc inner join product on pc.model= product.model WHERE maker = 'A'   
group by maker 
```

### Задание номер 14
```sql
SELECT classes.class , name,country FROM classes inner join ships on classes.class = ships.class  
WHERE numguns >= 10  
```

### Задание номер 15
```sql
SELECT hd  FROM pc group by hd having count(model)>1 
```

### Задание номер 16
```sql
SELECT DISTINCT B.model AS model1, A.model AS model1, A.speed, A.ram 
FROM PC AS A, PC B 
WHERE A.speed = B.speed AND A.ram = B.ram and A.model < B.model 
```

### Задание номер 17
```sql
SELECT distinct type,laptop.model,speed FROM laptop inner join product on laptop.model= product.model  
WHERE speed < (SELECT MIN(speed) FROM pc)  
```

### Задание номер 18
```sql
SELECT DISTINCT maker,price  FROM printer inner JOIN product ON printer.model= product.model  
WHERE price = (SELECT min(price)FROM printer WHERE color = 'y' ) and color = 'y'  
```

### Задание номер 19
```sql
SELECT maker ,avg(screen)as Average_screen_size 
FROM laptop inner join product on laptop.model =  product.model group by maker  
```

### Задание номер 20
```sql
SELECT maker , count(model) as Amount_of_Models FROM product WHERE type = 'pc' group by maker 
having count(model) >= 3 
```

### Задание номер 21
```sql
SELECT maker , max(price)as Maximum_price FROM pc inner join product on pc.model= product.model  
group by maker 
```

### Задание номер 22
```sql
SELECT speed , avg(price) as Average_price FROM pc  WHERE speed > 600 group by speed  
```

### Задание номер 23
```sql
SELECT distinct maker  FROM pc inner join product on pc.model = product.model  
WHERE pc.speed >= 750 and maker in (SELECT  maker  
FROM laptop inner join product on laptop.model = product.model WHERE laptop.speed >= 750)  
```

### Задание номер 24
```sql
SELECT model FROM( 
SELECT distinct model, price FROM laptop WHERE laptop.price = (SELECT MAX(price) FROM laptop)  
UNION 
SELECT distinct model, price FROM pc WHERE pc.price = (SELECT MAX(price) FROM pc)  
UNION 
SELECT distinct model, price FROM printer WHERE printer.price = (SELECT MAX(price) FROM printer)  
) as t 
WHERE t.price=(SELECT MAX(price) FROM ( 
SELECT distinct price FROM laptop WHERE laptop.price = (SELECT MAX(price) FROM laptop)  
UNION 
SELECT distinct price FROM pc WHERE pc.price = (SELECT MAX(price) FROM pc)  
UNION 
SELECT distinct price FROM printer WHERE printer.price = (SELECT MAX(price) FROM printer)  
) as t1 )    
```

### Задание номер 25
```sql
SELECT distinct product.maker FROM product WHERE product.type='Printer'  
INTERSECT 
SELECT distinct product.maker FROM product INNER JOIN pc ON pc.model=product.model  
WHERE product.type='PC' AND pc.ram=(SELECT MIN(ram) FROM pc)  
AND pc.speed = (SELECT MAX(speed) FROM (SELECT distinct speed FROM pc 
WHERE pc.ram=(SELECT MIN(ram) FROM pc)) as t) 
```

### Задание номер 26
```sql
SELECT t1.c/t1.d FROM( SELECT SUM(t.a) as c, SUM(t.b) as d FROM(  
SELECT SUM(pc.price) as a, COUNT(pc.code) as b FROM pc 
INNER JOIN product ON pc.model=product.model WHERE product.maker='A'  
UNION 
SELECT SUM(laptop.price) as a, COUNT(laptop.code) as b FROM laptop 
INNER JOIN product ON laptop.model=product.model WHERE product.maker='A') as t) as t1  
```

### Задание номер 27
```sql
SELECT maker,avg(hd)  FROM product inner join pc on product.model=pc.model   
WHERE maker in(SELECT maker  FROM product  WHERE type='printer')  group by maker
```

### Задание номер 28
```sql
SELECT count(*)  FROM ( SELECT maker FROM product group by maker having count(model)=1 ) as Amount
```

### Задание номер 29
```sql
SELECT t.point, t.date, SUM(t.inc), sum(t.out) FROM( SELECT point, date, inc, null as out FROM Income_o  
Union 
SELECT point, date, null as income, Outcome_o.out FROM Outcome_o) as t group by t.point, t.date 
```

### Задание номер 30
```sql
SELECT point, date, SUM(sum_out), SUM(sum_inc) 
FROM( SELECT point, date, SUM(inc) as sum_inc, null as sum_out FROM Income Group by point, date  
Union 
SELECT point, date, null as summarize_incomce, SUM(out) as sum_out FROM Outcome Group by point, date ) as t  
group by point, date order by point
```

### Задание номер 31
```sql
SELECT class , country FROM classes WHERE bore >= 16
```

### Задание номер 32
```sql
SELECT country, cast(avg((power(bore,3)/2)) as numeric(6,2)) as weight_ton 
FROM (SELECT country, classes.class, bore, name FROM classes left join ships on classes.class=ships.class  
union all 
SELECT distinct country, class, bore, ship FROM classes t1 left join outcomes t2 on t1.class=t2.ship  
WHERE ship=class and ship not in (SELECT name FROM ships) ) a  
WHERE name!='null' group by country
```

### Задание номер 33
```sql
SELECT ship FROM outcomes,battles WHERE result= 'sunk' and battle = 'North Atlantic' group by ship
```

### Задание номер 34
```sql
SELECT name  FROM classes,ships WHERE launched>=1922 and displacement > 35000 and type='bb' and ships.class = classes.class
```

### Задание номер 35
```sql
SELECT model, type FROM product 
WHERE model NOT LIKE '%[^0-9]%' OR model NOT LIKE '%[^a-z]%'
```

### Задание номер 36
```sql
SELECT name  FROM ships  WHERE class = name union  
SELECT ship as name_ship FROM classes,outcomes  WHERE classes.class = outcomes.ship
```

### Задание номер 37
```sql
SELECT class  FROM(SELECT name,class FROM ships  
union  
SELECT class as name_ship,class  FROM classes,outcomes  WHERE classes.class=outcomes.ship) A   
group by class  having count(A.name)=1
```

### Задание номер 38
```sql
SELECT distinct country  FROM classes  WHERE type='bb'   
intersect  
SELECT distinct country  FROM classes  WHERE type='bc'
```

### Задание номер 39
```sql
SELECT distinct ccc.sh FROM ( SELECT aaa.ship as sh, aaa.[date] as d1, bbb.[date] as d2 FROM ( 
SELECT ship, [date] FROM outcomes as o inner join battles as b on o.battle=b.name WHERE result = 'damaged') as aaa inner join (SELECT ship,  
[date] FROM outcomes as o inner join battles as b on o.battle=b.name) as bbb on aaa.ship=bbb.ship 
WHERE bbb.date > aaa.date) as ccc
```

### Задание номер 40
```sql
SELECT maker ,type FROM Product 
WHERE maker in ( SELECT maker  
FROM ( SELECT maker,type FROM Product group by maker,type ) x  
group by maker having count(*)=1 )  
group by maker,type having count(*)>1
```

### Задание 41 
```sql
 
with D as
(SELECT model, price FROM PC
union
SELECT model, price FROM Laptop
union
SELECT model, price FROM Printer)
SELECT distinct P.maker,
CASE WHEN MAX(CASE WHEN D.price IS NULL THEN 1 ELSE 0 END) = 0 THEN
MAX(D.price) END
FROM Product P
right join D on P.model=D.model
group by P.maker;

```

### Задание номер 42
```sql
SELECT ship,battle FROM outcomes WHERE result ='sunk'
```

### Задание номер 43
```sql
SELECT name FROM battles WHERE DATEPART(yy, date) not in (SELECT DATEPART(yy, date)  
FROM battles join ships on DATEPART(yy, date)=launched)
```

### Задание номер 44
```sql
SELECT name FROM ships WHERE name like 'R%'   
union   
SELECT name FROM battles WHERE name like 'R%'   
union   
SELECT ship FROM outcomes WHERE ship like 'R%'
```

### Задание номер 45
```sql
SELECT name FROM ships WHERE name like '% % %'  
union   
SELECT ship FROM outcomes WHERE ship like '% % %'
```

### Задание номер 46
```sql
SELECT name as n, displacement as d, numguns as ng FROM ships inner join classes on ships.class=classes.class WHERE name in (SELECT ship FROM outcomes WHERE battle = 'Guadalcanal')   
union 

SELECT ship as n, displacement as d, numguns as ng FROM outcomes inner join classes on outcomes.ship=classes.class WHERE battle = 'Guadalcanal' and ship not in (SELECT name FROM ships)   
union  
SELECT ship as n, null as d, null as ng FROM outcomes WHERE battle = 'Guadalcanal' and ship not in (SELECT name FROM ships) and ship not in  (SELECT class FROM classes)      
```

### Задание номер 47
```sql
WITH out AS (SELECT *
FROM outcomes JOIN (SELECT ships.name s_name, classes.class s_class, classes.country s_country
FROM ships FULL JOIN classes
ON ships.class = classes.class
) u
ON outcomes.ship=u.s_class
UNION 
SELECT *
FROM outcomes JOIN (SELECT ships.name s_name, classes.class s_class, classes.country s_country
FROM ships FULL JOIN classes
ON ships.class = classes.class
) u
ON outcomes.ship=u.s_name)

SELECT fin.country
FROM (
SELECT DISTINCT t.country, COUNT(t.name) AS num_ships
FROM (
SELECT distinct c.country, s.name
FROM classes c
inner join Ships s on s.class= c.class
union
SELECT distinct c.country, o.ship
FROM classes c
inner join Outcomes o on o.ship= c.class) t
GROUP BY t.country

INTERSECT

SELECT out.s_country, COUNT(out.ship) AS num_ships
FROM out
WHERE out.result='sunk'
GROUP BY out.s_country) fin
```

### Задание номер 48
```sql
SELECT class as one FROM ships WHERE name in(SELECT ship FROM outcomes WHERE result='sunk')   
union  
SELECT ship as one FROM outcomes  
WHERE ship not in(SELECT name FROM ships) and ship in(SELECT class FROM classes) and result='sunk'
```

### Задание номер 49
```sql
SELECT name FROM ships WHERE class in( SELECT class FROM classes WHERE bore=16)   
union  
SELECT ship FROM outcomes WHERE ship in( SELECT class FROM classes WHERE bore=16)    
```

### Задание номер 50
```sql
SELECT distinct battle FROM Classes  inner JOIN Ships  ON ships.class = classes.class   
inner JOIN Outcomes  ON Classes.class=Outcomes.ship or Ships.name=Outcomes.ship   
WHERE classes.class = 'Kongo'
```

### Задание номер 51
```sql
SELECT NAME FROM(SELECT name as NAME, displacement, numguns  
FROM ships inner join classes on ships.class = classes.class 
union 
SELECT ship as ship_name, displacement, numguns FROM outcomes inner join classes on outcomes.ship= classes.class) as d1 inner join (SELECT displacement, max(numGuns) as numguns FROM ( SELECT displacement, numguns FROM ships inner join classes on ships.class = classes.class  
union 
SELECT displacement, numguns  FROM outcomes inner join classes on outcomes.ship= classes.class) as f 
group by displacement) as d2 on d1.displacement=d2.displacement and d1.numguns =d2.numguns
```

### Задание номер 52
```sql
SELECT distinct name FROM ships  inner join classes cl on ships.class=cl.class 
WHERE (numGuns>=9 or numguns is NULL) and (bore<19 or bore is NULL) and (displacement<=65000 or displacement is NULL) and type='bb' and country='japan'
```

### Задание номер 53
```sql
SELECT cast(avg(numguns*1.0) as numeric(4,2)) as Avg_numGuns  FROM classes WHERE type='bb'
```

### Задание номер 54
```sql
SELECT CAST(AVG(numguns*1.0) AS NUMERIC (4,2)) as AVG_nmg 
FROM (SELECT ship, type, numguns   FROM Outcomes LEFT JOIN Classes ON ship = class  
UNION  
SELECT name, type, numguns FROM Ships as S INNER JOIN  Classes as C ON c.class = s.class ) AS T 
WHERE type = 'bb'
```

### Задание номер 55
```sql
SELECT C.class, min(launched)  FROM ships as S right join classes as C on s.class=c.class group by C.class
```

### Задание номер 56
```sql
SELECT c.class, COUNT(s.ship)
FROM classes c
  LEFT JOIN
    (
       SELECT o.ship, sh.class
       FROM outcomes o
       LEFT JOIN ships sh ON sh.name = o.ship
       WHERE o.result = 'sunk'
    ) AS s ON s.class = c.class OR s.ship = c.class
GROUP BY c.class
```

### Задание номер 57
```sql
SELECT class as cls, count(class) as sunked FROM( 
SELECT C.class, O.ship FROM classes as C join outcomes as O on C.class=O.ship WHERE O.result='sunk' 
union 
SELECT S.class, O.ship FROM outcomes as O join ships as S on S.name=O.ship WHERE O.result='sunk') as T 
WHERE class in ( SELECT distinct X.class FROM  (SELECT C.class, O.ship FROM classes as C join outcomes as O on C.class=O.ship 
union 
SELECT C.class, S.name FROM classes as C join ships as S on C.class=S.class) as X group by X.class 
having count(X.class)>=3 )  group by class
```

### Задание номер 58
```sql
SELECT main_maker ,main_type ,CONVERT(NUMERIC(6,2),((sub_num*100.00)/(total_num*100.00)*100.00))  
FROM (SELECT count(p5.model) total_num ,p5.maker main_maker 
FROM product p5 group by p5.maker) p6 JOIN (SELECT p3.maker sub_maker ,p3.type main_type ,count(p4.model) sub_num 
FROM (SELECT p1.maker maker, p2.type type FROM product p1 cross join product p2 group by p1.maker, p2.type) p3 left join product p4 on p3.maker = p4.maker and p3.type = p4.type group by  p3.maker,p3.type) p7 ON p7.sub_maker = p6.main_maker
```

### Задание номер 59
```sql
SELECT a.point, case when o is null then i else i-o end remain FROM  (SELECT point, sum(inc) as i 
FROM Income_o group by point) as A left join (SELECT point, sum(out) as o FROM Outcome_o group by point) as B on A.point=B.point
```

### Задание номер 60
```sql
SELECT a.point,  case when o is null  then i else i-o end remain FROM (SELECT point, sum(inc) as i 
FROM Income_o WHERE '20010415' > date group by point) as A left join (SELECT point, sum(out) as o 
FROM Outcome_o  WHERE '20010415' > date group by point) as B on A.point=B.point
```

### Задание номер 61
```sql
SELECT sum(i) FROM
(SELECT point, sum(inc) as i FROM
income_o
group by point

UNION

SELECT point, -sum(out) as i FROM
outcome_o
group by point
) as t
```

### Задание номер 62
```sql
SELECT
(SELECT sum(inc) FROM Income_o WHERE date<'2001-04-15')
-
(SELECT sum(out) FROM Outcome_o WHERE date<'2001-04-15')
AS remain
```

### Задание номер 63
```sql
SELECT name FROM Passenger
WHERE ID_psg in
(SELECT ID_psg FROM Pass_in_trip
GROUP BY place, ID_psg
HAVING count(*)>1)
```

### Задание номер 64
```sql
SELECT i1.point, i1.date, 'inc', sum(inc) FROM Income,
(SELECT point, date FROM Income
EXCEPT
SELECT Income.point, Income.date FROM Income
JOIN Outcome ON (Income.point=Outcome.point) AND
(Income.date=Outcome.date)
) AS i1
WHERE i1.point=Income.point AND i1.date=Income.date
GROUP BY i1.point, i1.date
UNION
SELECT o1.point, o1.date, 'out', sum(out) FROM Outcome,
(SELECT point, date FROM Outcome
EXCEPT
SELECT Income.point, Income.date FROM Income
JOIN Outcome ON (Income.point=Outcome.point) AND
(Income.date=Outcome.date)
) AS o1
WHERE o1.point=Outcome.point AND o1.date=Outcome.date
GROUP BY o1.point, o1.date
```

### Задание номер 65
```sql
SELECT
  row_number() over(order by maker) as num
  ,CASE WHEN mnum=1 THEN maker
    ELSE ''
  END as maker
  ,type
  FROM (
    SELECT
    row_number() over(partition by maker order by maker, ord) as mnum
    ,maker
    ,type
    FROM (
    SELECT
      distinct maker, type
      ,CASE WHEN LOWER(type)='pc' then 1
            WHEN LOWER(type)='laptop' then 2
            ELSE 3
      END as ord
      FROM product
    ) as mto
  ) as mtn
```

### Задание номер 66
```sql
SELECT date, max(c) FROM
(SELECT date,count(*) AS c FROM Trip,
(SELECT trip_no,date FROM Pass_in_trip WHERE date>='2003-04-01' AND date<='2003-04-07' GROUP BY trip_no, date) AS t1
WHERE Trip.trip_no=t1.trip_no AND town_FROM='Rostov'
GROUP BY date
UNION ALL
SELECT '2003-04-01',0
UNION ALL
SELECT '2003-04-02',0
UNION ALL
SELECT '2003-04-03',0
UNION ALL
SELECT '2003-04-04',0
UNION ALL
SELECT '2003-04-05',0
UNION ALL
SELECT '2003-04-06',0
UNION ALL
SELECT '2003-04-07',0) AS t2
GROUP BY date
```

### Задание номер 67
```sql
SELECT count(*) FROM
(SELECT TOP 1 WITH TIES count(*) c, town_FROM, town_to FROM trip
group by town_FROM, town_to
order by c desc) as t
```

### Задание номер 68
```sql
SELECT count(*) FROM (
SELECT TOP 1 WITH TIES sum(c) cc, c1, c2 FROM (
SELECT count(*) c, town_FROM c1, town_to c2 FROM trip
WHERE town_FROM>=town_to
group by town_FROM, town_to
union all
SELECT count(*) c,town_to, town_FROM FROM trip
WHERE town_to>town_FROM
group by town_FROM, town_to
) as t
group by c1,c2
order by cc desc
) as tt
```

### Задание номер 69
```sql
with q as (
  SELECT
    isnull(i.point, o.point) point
    , isnull(i.date, o.date) date
    , coalesce(sum(i.inc), 0) - coalesce(sum(o.out), 0) balance
    FROM income i
    full join outcome o
      on i.point=o.point and i.date=o.date and i.code=o.code
    group by isnull(i.point, o.point), isnull(i.date, o.date)
)
SELECT
  point
  , convert(varchar, date, 103) day
  , sum(balance) over(partition by point order by date RANGE UNBOUNDED PRECEDING) as rem
  FROM q
order by point,date
```

### Задание номер 70
```sql
SELECT DISTINCT o.battle
FROM outcomes o
LEFT JOIN ships s ON s.name = o.ship
LEFT JOIN classes c ON o.ship = c.class OR s.class = c.class
WHERE c.country IS NOT NULL
GROUP BY c.country, o.battle
HAVING COUNT(o.ship) >= 3
```

### Задание номер 71
```sql
SELECT p.maker
FROM product p
LEFT JOIN pc ON pc.model = p.model
WHERE p.type = 'PC'
GROUP BY p.maker
HAVING COUNT(p.model) = COUNT(pc.model)
```

### Задание номер 72
```sql
SELECT TOP 1 WITH TIES name, c3 FROM passenger
join
(SELECT c1, max(c3) c3 FROM
(
SELECT pass_in_trip.ID_psg c1, Trip.ID_comp c2, count(*) c3 FROM pass_in_trip
join trip on trip.trip_no=pass_in_trip.trip_no
group by pass_in_trip.ID_psg, Trip.ID_comp
) as t
group by c1
having count(*)=1) as tt
on ID_psg=c1
order by c3 desc
```

### Задание номер 73
```sql
SELECT country, name as battle FROM classes, battles
except
SELECT country, battle
FROM (
  SELECT class, name as ship_name FROM ships
  union
  SELECT ship, ship FROM outcomes
) as sh
join Classes c on sh.class=c.class
join Outcomes o on o.ship=sh.ship_name
```

### Задание номер 74
```sql
SELECT c.country, c.class
FROM classes c
WHERE UPPER(c.country) = 'RUSSIA' AND EXISTS (
SELECT c.country, c.class
FROM classes c
WHERE UPPER(c.country) = 'RUSSIA' )
UNION ALL
SELECT c.country, c.class
FROM classes c
WHERE NOT EXISTS (SELECT c.country, c.class
FROM classes c
WHERE UPPER(c.country) = 'RUSSIA' )
```

### Задание номер 75
```sql
SELECT maker,
max(l.price) as laptop,
max(pc.price) as pc,
max(pr.price) as printer
FROM laptop l right join product p on l.model = p.model left join pc on pc.model = p.model left join printer pr on p.model = pr.model
WHERE maker in (
SELECT maker FROM product WHERE model in (
SELECT model FROM pc WHERE price is not null union all
SELECT model FROM printer WHERE price is not null union all
SELECT model FROM laptop WHERE price is not null)
) group by maker order by maker;
```

### Задание номер 76
```sql
WITH cte AS
(SELECT ROW_NUMBER() OVER (PARTITION BY ps.ID_psg,pit.place ORDER BY pit.date) AS rowNumber
,DATEDIFF (minute, time_out, DATEADD(DAY,IIF(time_in<time_out,1,0),time_in)) AS timeFlight, ps.Id_psg, ps.name
FROM Pass_in_trip pit LEFT JOIN trip tr ON pit.trip_no = tr.trip_no
LEFT JOIN Passenger ps ON ps.ID_psg = pit.ID_psg -- Все рейсы
)
SELECT MAX(cte.name),SUM(timeFlight) FROM cte
GROUP BY cte.ID_psg
HAVING MAX(rowNumber) = 1
```

### Задание номер 77
```sql
with q as (
SELECT
  count(distinct t.trip_no) as trip_count
  , pt.date
FROM trip t, pass_in_trip pt
WHERE t.trip_no=pt.trip_no
      and town_FROM='Rostov'
group by date
)
SELECT
  trip_count, date
  FROM q
  WHERE trip_count=(SELECT max(trip_count) FROM q)
;

### Задание номер 78
```sql
SELECT name, REPLACE(CONVERT(CHAR(12), DATEADD(m, DATEDIFF(m,0,date),0), 102),'.','-') AS first_day,
             REPLACE(CONVERT(CHAR(12), DATEADD(s,-1,DATEADD(m, DATEDIFF(m,0,date)+1,0)), 102),'.','-') AS last_day
FROM Battles
```

### Задание номер 79
```sql
SELECT Passenger.name, A.minutes
FROM (SELECT P.ID_psg,
      SUM((DATEDIFF(minute, time_out, time_in) + 1440)%1440) AS minutes,
      MAX(SUM((DATEDIFF(minute, time_out, time_in) + 1440)%1440)) OVER() AS MaxMinutes
      FROM Pass_in_trip P JOIN
       Trip AS T ON P.trip_no = T.trip_no
      GROUP BY P.ID_psg
      ) AS A JOIN
 Passenger ON Passenger.ID_psg = A.ID_psg
WHERE A.minutes = A.MaxMinutes
```

### Задание номер 80
```sql
SELECT DISTINCT maker
FROM product
WHERE maker NOT IN (
     SELECT maker
     FROM product
     WHERE type='PC' AND model NOT IN (
          SELECT model
          FROM PC))
```

### Задание номер 81
```sql
SELECT O.*
FROM outcome O
INNER JOIN
(
SELECT TOP 1 WITH TIES YEAR(date) AS Y, MONTH(date) AS M, SUM(out) AS ALL_TOTAL
FROM outcome
GROUP BY YEAR(date), MONTH(date)
ORDER BY ALL_TOTAL DESC
) R ON YEAR(O.date) = R.Y AND MONTH(O.date) = R.M
```

### Задание номер 82
```sql
WITH CTE(code,price,number)
AS
(
SELECT PC.code,PC.price, number= ROW_NUMBER() OVER (ORDER BY PC.code)
FROM PC
)
SELECT CTE.code, AVG(C.price)
FROM CTE
JOIN CTE C ON (C.number-CTE.number)<6 AND (C.number-CTE.number)> =0
GROUP BY CTE.number,CTE.code
HAVING COUNT(CTE.number)=6
```

### Задание номер 83
```sql
SELECT name
FROM Ships AS s JOIN Classes AS cl1 ON s.class = cl1.class
WHERE
CASE WHEN numGuns = 8 THEN 1 ELSE 0 END +
CASE WHEN bore = 15 THEN 1 ELSE 0 END +
CASE WHEN displacement = 32000 THEN 1 ELSE 0 END +
CASE WHEN type = 'bb' THEN 1 ELSE 0 END +
CASE WHEN launched = 1915 THEN 1 ELSE 0 END +
CASE WHEN s.class = 'Kongo' THEN 1 ELSE 0 END +
CASE WHEN country = 'USA' THEN 1 ELSE 0 END > = 4
```

### Задание номер 84
```sql
SELECT C.name, A.N_1_10, A.N_11_21, A.N_21_30
FROM (SELECT T.ID_comp,
       SUM(CASE WHEN DAY(P.date) < 11 THEN 1 ELSE 0 END) AS N_1_10,
       SUM(CASE WHEN (DAY(P.date) > 10 AND DAY(P.date) < 21) THEN 1 ELSE 0 END) AS N_11_21,


       SUM(CASE WHEN DAY(P.date) > 20 THEN 1 ELSE 0 END) AS N_21_30
      FROM Trip AS T JOIN
       Pass_in_trip AS P ON T.trip_no = P.trip_no AND CONVERT(char(6), P.date, 112) = '200304'
      GROUP BY T.ID_comp
      ) AS A JOIN
 Company AS C ON A.ID_comp = C.ID_comp
```

### Задание номер 85
```sql
SELECT maker 
FROM Product 
GROUP BY maker 
HAVING count(distinct type) = 1 AND (
	min(type) = 'printer' OR (min(type) = 'pc' AND count(model) >= 3)
)
```


### Задание номер 86
```sql
SELECT maker,
       CASE count(distinct type) when 2 then MIN(type) + '/' + MAX(type)
                                 when 1 then MAX(type)
                                 when 3 then 'Laptop/PC/Printer' END
FROM Product
GROUP BY maker
```

### Задание номер 87
```sql
SELECT DISTINCT name, COUNT(town_to) Qty
FROM Trip tr JOIN Pass_in_trip pit ON tr.trip_no = pit.trip_no JOIN
         Passenger psg ON pit.ID_psg = psg.ID_psg
WHERE town_to = 'Moscow' AND pit.ID_psg NOT IN(SELECT DISTINCT ID_psg
FROM Trip tr JOIN Pass_in_trip pit ON tr.trip_no = pit.trip_no
WHERE date+time_out = (SELECT MIN (date+time_out)
                       FROM Trip tr1 JOIN Pass_in_trip pit1 ON tr1.trip_no = pit1.trip_no
                       WHERE pit.ID_psg = pit1.ID_psg)
AND town_FROM = 'Moscow')
GROUP BY pit.ID_psg, name
HAVING COUNT(town_to) > 1
```

### Задание номер 88
```sql
SELECT
 (SELECT name FROM Passenger WHERE ID_psg = B.ID_psg) AS name,
 B.trip_Qty,
 (SELECT name FROM Company WHERE ID_comp = B.ID_comp) AS Company
FROM (SELECT P.ID_psg, MIN(T.ID_comp) AS ID_comp, COUNT(*) AS trip_Qty, MAX(COUNT(*)) OVER() AS Max_Qty
      FROM Pass_in_trip AS P JOIN
       Trip AS T ON P.trip_no = T.trip_no
      GROUP BY P.ID_psg
      HAVING MIN(T.ID_comp) = MAX(T.ID_comp)
      ) AS B
WHERE B.trip_Qty = B.Max_Qty
```

### Задание номер 89
```sql
SELECT Maker , count(distinct model) Qty FROM Product
group by maker
having count(distinct model) > = ALL
(SELECT count(distinct model) FROM Product
group by maker)
or
count(distinct model) <= ALL
(SELECT count(distinct model) FROM Product
group by maker)
```

### Задание номер 90
```sql
SELECT maker, model, type FROM
(
	SELECT maker, model, type,
	row_number() over(ORDER BY model) first,
	row_number() over(ORDER BY model DESC) second
	FROM Product
) R
WHERE first > 3 AND second > 3
```

### Задание номер 91
```sql
SELECT CAST(sum(T.s)/count (T.s) AS NUMERIC(12,2)) FROM
(SELECT distinct q.Q_NAME, SUM (cast(ISNULL(B_VOL,0) as FLOAT)) as s FROM utQ q
LEFT JOIN utB B on q.Q_ID=B.B_Q_ID
group by q.Q_NAME) T
```


### Задание номер 92
```sql
SELECT Q_NAME
FROM utQ
WHERE Q_ID IN (SELECT DISTINCT B.B_Q_ID
                FROM (SELECT B_Q_ID
                        FROM utB
                        GROUP BY B_Q_ID
                        HAVING SUM(B_VOL) = 765) AS B
                WHERE B.B_Q_ID NOT IN (SELECT B_Q_ID
                                        FROM utB
                                        WHERE B_V_ID IN (SELECT B_V_ID
                                                          FROM utB
                                                          GROUP BY B_V_ID
                                                          HAVING SUM(B_VOL) < 255)))
```

### Задание номер 93
```sql
SELECT c.name, sum(vr.vr)
FROM
(SELECT distinct t.id_comp, pt.trip_no, pt.date,t.time_out,t.time_in,--pt.id_psg,
case
     when DATEDIFF(mi, t.time_out,t.time_in)> 0 then DATEDIFF(mi, t.time_out,t.time_in)
     when DATEDIFF(mi, t.time_out,t.time_in)<=0 then DATEDIFF(mi, t.time_out,t.time_in+1)
end vr
FROM pass_in_trip pt left join trip t on pt.trip_no=t.trip_no
) vr left join company c on vr.id_comp=c.id_comp
group by c.name
```

### Задание номер 94
```sql
SELECT DATEADD(day, S.Num, D.date) AS Dt,
       (SELECT COUNT(DISTINCT P.trip_no)
        FROM Pass_in_trip P
               JOIN Trip T
                 ON P.trip_no = T.trip_no
                    AND T.town_FROM = 'Rostov'
                    AND P.date = DATEADD(day, S.Num, D.date)) AS Qty
FROM (SELECT (3 * ( x - 1 ) + y - 1) AS Num
        FROM (SELECT 1 AS x UNION ALL SELECT 2 UNION ALL SELECT 3) AS N1
               CROSS JOIN (SELECT 1 AS y UNION ALL SELECT 2 UNION ALL SELECT 3) AS N2
        WHERE (3 * ( x - 1 ) + y ) < 8) AS S,
       (SELECT MIN(A.date) AS date
        FROM (SELECT P.date,
                       COUNT(DISTINCT P.trip_no) AS Qty,
                       MAX(COUNT(DISTINCT P.trip_no)) OVER() AS M_Qty
                FROM Pass_in_trip AS P
                       JOIN Trip AS T
                         ON P.trip_no = T.trip_no
                            AND T.town_FROM = 'Rostov'
                GROUP BY P.date) AS A
        WHERE A.Qty = A.M_Qty) AS D
```

### Задание номер 95
```sql
SELECT name,
    COUNT(DISTINCT CONVERT(CHAR(24),date)+CONVERT(CHAR(4),Trip.trip_no)),
    COUNT(DISTINCT plane),
    COUNT(DISTINCT ID_psg),
    COUNT(*)
FROM Company,Pass_in_trip,Trip
WHERE Company.ID_comp=Trip.ID_comp and Trip.trip_no=Pass_in_trip.trip_no
GROUP BY Company.ID_comp,name
```

### Задание номер 96
```sql
with r as (SELECT v.v_name,
       v.v_id,
       count(case when v_color = 'R' then 1 end) over(partition by v_id) cnt_r,
       count(case when v_color = 'B' then 1 end) over(partition by b_q_id) cnt_b
  FROM utV v join utB b on v.v_id = b.b_v_id)
SELECT v_name
  FROM r
WHERE cnt_r > 1
  and cnt_b > 0
group by v_name
```

### Задание номер 97
```sql
SELECT code, speed, ram, price, screen
FROM laptop WHERE exists (
  SELECT 1 x
  FROM (
    SELECT v, rank()over(order by v) rn
    FROM ( SELECT cast(speed as float) sp, cast(ram as float) rm,
                  cast(price as float) pr, cast(screen as float) sc
    )l unpivot(v for c in (sp, rm, pr, sc))u
  )l pivot(max(v) for rn in ([1],[2],[3],[4]))p
  WHERE [1]*2 <= [2] and [2]*2 <= [3] and [3]*2 <= [4]
)
```


### Задание номер 98
```sql
with CTE AS
(SELECT
1 n, cast (0 as varchar(16)) bit_or,
code, speed, ram FROM PC
UNION ALL
SELECT n*2,
cast (convert(bit,(speed|ram)&n) as varchar(1))+cast(bit_or as varchar(15))
, code, speed, ram
FROM CTE WHERE n < 65536
)
SELECT code, speed, ram FROM CTE
WHERE n = 65536
and CHARINDEX('1111', bit_or )> 0
```

### Задание номер 99
```sql
with data as (SELECT point, date, case when out is null then date else dateadd(dd, case when datename(dw,dateadd(dd, 1, date))='sunday' then 2 else 1 end, date) end date2 FROM (SELECT a.*, b.out FROM income_o a left join outcome_o b on a.point=b.point and a.date=b.date)aa)
SELECT data.point, data.date, data.date2 FROM data
except
SELECT data.point, data.date, data.date2 FROM data,outcome_o WHERE outcome_o.point=data.point and data.date2=outcome_o.date
union
SELECT data.point,data.date, (SELECT dateadd(dd,case when datename(dw,min(date))='saturday' then 2 else 1 end,min(date)) FROM (SELECT point, date FROM outcome_o WHERE concat(point, ' ',dateadd(dd,case when datename(dw,date)='saturday' then 2 else 1 end,date)) not in (SELECT concat (point,' ',date) FROM outcome_o))nn WHERE date>=data.date2 and point=data.point) FROM data,outcome_o WHERE outcome_o.point=data.point and data.date2=outcome_o.date
```

### Задание номер 100
```sql
with data1 as (SELECT row_number() over (partition by date order by date,code) row,code,point,date, inc FROM income),
data2 as (SELECT row_number() over (partition by date order by date,code) row,code,point,date, out FROM outcome)

SELECT date,row_number() over (partition by date order by date,code1,code2) row, incpoint, inc, outpoint, out FROM (SELECT coalesce (data1.date,data2.date) date,data1.code code1,data1.point incpoint,data1.inc,data2.code code2,data2.point outpoint,data2.out FROM data1 full join data2 on data1.row=data2.row and data1.date=data2.date)aa order by date,row
```

