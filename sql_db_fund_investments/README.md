# SQL: Анализ данных о фондах и инвестициях 
## Tags
SQL, PostgreSQL, Data slicing, Aggregations, JOINs, Subqueries

## Задания

Нужно проанализировать данные о фондах и инвестициях и написать запросы к базе.

### Database scheme
![Database scheme](db_scheme.png)
<details>
<summary>Простейшие запросы (1. - 5.)</summary>

1. Посчитайте, сколько компаний закрылось.

```SQL
SELECT count(*)
FROM company
WHERE status='closed'
```
2. Отобразите количество привлечённых средств для новостных компаний США. Используйте данные из таблицы company. Отсортируйте таблицу по убыванию значений в поле funding_total .

```SQL
SELECT funding_total
FROM company
WHERE country_code='USA'
  AND category_code='news'
ORDER BY funding_total DESC
```

3. Найдите общую сумму сделок по покупке одних компаний другими в долларах. Отберите сделки, которые осуществлялись только за наличные с 2011 по 2013 год включительно.

```SQL
SELECT sum(price_amount)
FROM acquisition
WHERE term_code='cash'
  AND acquired_at BETWEEN '2011-01-01' AND '2013-12-31'
```

4. Отобразите имя, фамилию и названия аккаунтов людей в твиттере, у которых названия аккаунтов начинаются на 'Silver'.

```SQL
SELECT first_name,
       last_name,
       twitter_username
FROM people
WHERE twitter_username like 'Silver%'
```

5. Выведите на экран всю информацию о людях, у которых названия аккаунтов в твиттере содержат подстроку 'money', а фамилия начинается на 'K'.

```SQL
SELECT *
FROM people
WHERE twitter_username like '%money%'
  AND last_name like 'K%'
```

</details>


6. Для каждой страны отобразите общую сумму привлечённых инвестиций, которые получили компании, зарегистрированные в этой стране. Страну, в которой зарегистрирована компания, можно определить по коду страны. Отсортируйте данные по убыванию суммы.

```SQL
SELECT country_code,
    sum(funding_total)
FROM company
GROUP BY country_code
ORDER BY sum(funding_total) DESC
```


7. Составьте таблицу, в которую войдёт дата проведения раунда, а также минимальное и максимальное значения суммы инвестиций, привлечённых в эту дату. Оставьте в итоговой таблице только те записи, в которых минимальное значение суммы инвестиций не равно нулю и не равно максимальному значению.
```SQL

SELECT funded_at,
       min(raised_amount),
       max(raised_amount)
FROM funding_round
GROUP BY funded_at
HAVING min(raised_amount)<>0
AND min(raised_amount)<>max(raised_amount)
```

8. Создайте поле с категориями:
* Для фондов, которые инвестируют в 100 и более компаний, назначьте категорию high_activity
* Для фондов, которые инвестируют в 20 и более компаний до 100, назначьте категорию middle_activity.
* Если количество инвестируемых компаний фонда не достигает 20, назначьте категорию low_activity.
* Отобразите все поля таблицы fund и новое поле с категориями.
```SQL
SELECT *,
       CASE
           WHEN invested_companies >=100 THEN 'high_activity'
           WHEN invested_companies >=20 THEN 'middle_activity'
           ELSE 'low_activity'
       END AS category
FROM fund
```

9. Для каждой из категорий, назначенных в предыдущем задании, посчитайте округлённое до ближайшего целого числа среднее количество инвестиционных раундов, в которых фонд принимал участие. Выведите на экран категории и среднее число инвестиционных раундов. Отсортируйте таблицу по возрастанию среднего.
```SQL
SELECT activity,
       round(avg(investment_rounds)) avg_rounds
FROM
  (SELECT *,
          CASE
              WHEN invested_companies>=100 THEN 'high_activity'
              WHEN invested_companies>=20 THEN 'middle_activity'
              ELSE 'low_activity'
          END AS activity
   FROM fund) AS cat_funds
GROUP BY activity
ORDER BY avg_rounds
```

10. Проанализируйте, в каких странах находятся фонды, которые чаще всего инвестируют в стартапы. 
* Для каждой страны посчитайте минимальное, максимальное и среднее число компаний, в которые инвестировали фонды этой страны, основанные с 2010 по 2012 год включительно. Исключите страны с фондами, у которых минимальное число компаний, получивших инвестиции, равно нулю. 
* Выгрузите десять самых активных стран-инвесторов: отсортируйте таблицу по среднему количеству компаний от большего к меньшему. Затем добавьте сортировку по коду страны в лексикографическом порядке.
```SQL
SELECT country_code,
min(invested_companies),
max(invested_companies),
avg(invested_companies)
FROM fund
WHERE founded_at BETWEEN cast('2010-01-01' AS timestamp) AND cast('2012-12-31' AS timestamp)
GROUP BY country_code
HAVING min(invested_companies)>0
ORDER BY avg(invested_companies) DESC, country_code
LIMIT 10
```

11. Отобразите имя и фамилию всех сотрудников стартапов. Добавьте поле с названием учебного заведения, которое окончил сотрудник, если эта информация известна.
```SQL
SELECT first_name,
       last_name,
       e.instituition
FROM people p
LEFT JOIN education e ON e.person_id=p.id
```

12. Для каждой компании найдите количество учебных заведений, которые окончили её сотрудники. Выведите название компании и число уникальных названий учебных заведений. Составьте топ-5 компаний по количеству университетов.
```SQL
SELECT c.name,
       count(DISTINCT e.instituition)
FROM people p
JOIN company c ON c.id=p.company_id
JOIN education e ON e.person_id=p.id
GROUP BY c.name
ORDER BY count(DISTINCT e.instituition) DESC
LIMIT 5
```

13. Составьте список с уникальными названиями закрытых компаний, для которых первый раунд финансирования оказался последним.
```SQL
SELECT DISTINCT c.name
FROM company c
JOIN funding_round fr ON fr.company_id=c.id
WHERE is_first_round=1
  AND is_last_round=1
  AND c.status='closed'
```

14. Составьте список уникальных номеров сотрудников, которые работают в компаниях, отобранных в предыдущем задании.
```SQL
SELECT DISTINCT id
FROM people
WHERE company_id in
    (SELECT DISTINCT c.id
     FROM company c
     JOIN funding_round fr ON fr.company_id=c.id
     WHERE is_first_round=1
       AND is_last_round=1
       AND c.status='closed')
```

15. Составьте таблицу, куда войдут уникальные пары с номерами сотрудников из предыдущей задачи и учебным заведением, которое окончил сотрудник.
```SQL
SELECT DISTINCT p.id,
                e.instituition
FROM people p
JOIN education e ON e.person_id= p.id
WHERE company_id in
    (SELECT DISTINCT c.id
     FROM company c
     JOIN funding_round fr ON fr.company_id=c.id
     WHERE is_first_round=1
       AND is_last_round=1
       AND c.status='closed')
```

16. Посчитайте количество учебных заведений для каждого сотрудника из предыдущего задания. При подсчёте учитывайте, что некоторые сотрудники могли окончить одно и то же заведение дважды.
```SQL
SELECT DISTINCT p.id,
                count(e.instituition)
FROM people p
JOIN education e ON e.person_id= p.id
WHERE company_id in
    (SELECT DISTINCT c.id
     FROM company c
     JOIN funding_round fr ON fr.company_id=c.id
     WHERE is_first_round=1
       AND is_last_round=1
       AND c.status='closed')
GROUP BY p.id
```

17. Дополните предыдущий запрос и выведите среднее число учебных заведений (всех, не только уникальных), которые окончили сотрудники разных компаний. Нужно вывести только одну запись, группировка здесь не понадобится.
```SQL
SELECT avg(COUNT)
FROM
  (SELECT DISTINCT p.id,
                   count(e.instituition)
   FROM people p
   JOIN education e ON e.person_id= p.id
   WHERE company_id in
       (SELECT DISTINCT c.id
        FROM company c
        JOIN funding_round fr ON fr.company_id=c.id
        WHERE is_first_round=1
          AND is_last_round=1
          AND c.status='closed')
   GROUP BY p.id) DATA
```

18. Напишите похожий запрос: выведите среднее число учебных заведений (всех, не только уникальных), которые окончили сотрудники Facebook*.
*(сервис, запрещённый на территории РФ)
```SQL
SELECT avg(COUNT)
FROM
  (SELECT DISTINCT p.id,
                   count(e.instituition)
   FROM people p
   JOIN education e ON e.person_id= p.id
   WHERE company_id =
       (SELECT id
        FROM company
        WHERE name='Facebook' ) --*(сервис, запрещённый на территории РФ)

   GROUP BY p.id) DATA
```

19. Составьте таблицу из полей:
- name_of_fund — название фонда;
- name_of_company — название компании;
- amount — сумма инвестиций, которую привлекла компания в раунде.

В таблицу войдут данные о компаниях, в истории которых было больше шести важных этапов, а раунды финансирования проходили с 2012 по 2013 год включительно.
```SQL
SELECT f.name name_of_fund,
       c.name name_of_company,
       raised_amount
FROM company c
JOIN investment i ON c.id=i.company_id
JOIN funding_round fr ON fr.id=i.funding_round_id
JOIN fund f ON f.id=i.fund_id
WHERE c.milestones>6
  AND funded_at BETWEEN '2012-01-01' AND '2013-12-31'
```

20. Выгрузите таблицу, в которой будут такие поля:
- название компании-покупателя;
- сумма сделки;
- название компании, которую купили;
- сумма инвестиций, вложенных в купленную компанию;
- доля, которая отображает, во сколько раз сумма покупки превысила сумму вложенных в компанию инвестиций, округлённая до ближайшего целого числа.

Не учитывайте те сделки, в которых сумма покупки равна нулю. Если сумма инвестиций в компанию равна нулю, исключите такую компанию из таблицы. 
Отсортируйте таблицу по сумме сделки от большей к меньшей, а затем по названию купленной компании в лексикографическом порядке. Ограничьте таблицу первыми десятью записями.
```SQL
SELECT cb.name,
       a.price_amount,
       cs.name,
       cs.funding_total,
       round(price_amount/cs.funding_total) rel
FROM acquisition a
JOIN company cb ON a.acquiring_company_id=cb.id
JOIN company cs ON a.acquired_company_id=cs.id
WHERE price_amount<>0
  AND cs.funding_total<>0
ORDER BY a.price_amount DESC,
         cs.name
LIMIT 10
```

21. Выгрузите таблицу, в которую войдут названия компаний из категории social, получившие финансирование с 2010 по 2013 год включительно. Проверьте, что сумма инвестиций не равна нулю. Выведите также номер месяца, в котором проходил раунд финансирования.
```SQL
SELECT c.name,
       extract('month'
               FROM fr.funded_at)
FROM
  (SELECT id,
          name
   FROM company c
   WHERE category_code='social') c
JOIN funding_round fr ON fr.company_id=c.id
WHERE fr.funded_at BETWEEN '2010-01-01' AND '2013-12-31'
  AND fr.raised_amount<>0
```

22. Отберите данные по месяцам с 2010 по 2013 год, когда проходили инвестиционные раунды. Сгруппируйте данные по номеру месяца и получите таблицу, в которой будут поля:
- номер месяца, в котором проходили раунды;
- количество уникальных названий фондов из США, которые инвестировали в этом месяце;
- количество компаний, купленных за этот месяц;
- общая сумма сделок по покупкам в этом месяце.
```SQL
SELECT f_r.month,
       f_r.funds_count,
       acq.acquired_count,
       acq.acquired_sum
FROM
  (SELECT extract('month'
                  FROM fr.funded_at) AS MONTH,
          count(DISTINCT f.name) funds_count
   FROM funding_round fr
   JOIN
     (SELECT f.name,
             i.funding_round_id
      FROM fund f
      JOIN investment i ON i.fund_id=f.id
      WHERE f.country_code='USA') f ON f.funding_round_id=fr.id
   WHERE fr.funded_at BETWEEN '2010-01-01' AND '2013-12-31'
   GROUP BY MONTH) f_r
JOIN
  (SELECT extract('month'
                  FROM a.acquired_at) AS MONTH,
          count(*) acquired_count,
          sum(price_amount) acquired_sum
   FROM acquisition a
   WHERE a.acquired_at BETWEEN '2010-01-01' AND '2013-12-31'
   GROUP BY MONTH) acq ON f_r.month=acq.month
```

23. Составьте сводную таблицу и выведите среднюю сумму инвестиций для стран, в которых есть стартапы, зарегистрированные в 2011, 2012 и 2013 годах. Данные за каждый год должны быть в отдельном поле. Отсортируйте таблицу по среднему значению инвестиций за 2011 год от большего к меньшему.
```SQL
WITH all_data AS
  (SELECT country_code,
          extract('year'
                  FROM founded_at) AS YEAR,
          avg(funding_total) avg_fund
   FROM company
   WHERE country_code in
       (SELECT DISTINCT country_code
        FROM company
        WHERE founded_at BETWEEN '2011-01-01' AND '2013-12-31')
     AND founded_at BETWEEN '2011-01-01' AND '2013-12-31'
   GROUP BY country_code,
            extract('year'
                    FROM founded_at))
SELECT first.country_code,
       avg_2011,
       avg_2012,
       avg_2013
FROM
  (SELECT all_data.country_code,
          avg_fund avg_2011
   FROM all_data
   WHERE YEAR=2011) FIRST
LEFT JOIN
  (SELECT all_data.country_code,
          avg_fund avg_2012
   FROM all_data
   WHERE YEAR=2012) SECOND ON second.country_code=first.country_code
LEFT JOIN
  (SELECT all_data.country_code,
          avg_fund avg_2013
   FROM all_data
   WHERE YEAR=2013) third ON third.country_code=first.country_code
WHERE avg_2011 IS NOT NULL
  AND avg_2012 IS NOT NULL
  AND avg_2013 IS NOT NULL
ORDER BY avg_2011 DESC
```