Таблица содержит следующие данные:

Название столбца	Тип переменной	Информация

1	country_id	INT	идентификатор страны

2	country_name	TEXT	название страны

3	region	TEXT	название региона

4	world_rank	INT	мировой рейтинг

5	region_rank	INT	рейтинг в регионе

6	score_2022	NUMERIC(3, 1)	баллы в 2022 году

7	property_rights	NUMERIC(4, 1)	право собственности

8	judical_effectiveness	NUMERIC(3, 1)	эффективность судебной системы

9	government_integrity	NUMERIC(3, 1)	честность правительства

10	tax_burden	NUMERIC(4, 1)	налоговая нагрузка

11	gov_spending	NUMERIC(3, 1)	государственные расходы

12	fiscal_health	NUMERIC(3, 1)	финансовое благополучие

13	business_freedom	NUMERIC(3, 1)	свобода бизнеса

14	labor_freedom	NUMERIC(3, 1)	свобода труда

15	monetary_freedom	NUMERIC(3, 1)	денежная свобода

16	trade_freedom	NUMERIC(3, 1)	свобода торговли

17	investment_freedom	INT	свобода инвестиций

18	financial_freedom	INT	финансовая свобода

19	tariff_rate	NUMERIC(3, 1)	ставка налога на импортные товары, %

20	income_tax_rate	NUMERIC(4, 1)	ставка подоходного налога -процент, который вы должны уплатить, исходя из вашего дохода, %

21	corporate_tax_rate	NUMERIC(3, 1)	корпоративный налог — это налог на прибыль организации, %

22	tax_burden_%_of_gdp	NUMERIC(3, 1)	общие налоговые поступления в процентах от ВВП

23	gov_expenditure_of_gdp	NUMERIC(4, 1)	государственные расходы в процентах от ВВП 

24	population_millions	NUMERIC(7, 3)	население, млн

25	gdp_billions_ppp	NUMERIC(6, 1)	валовой внутренний продукт (ВВП) – общий объем производства товаров и услуг с учетом покупательной способности, млрд

26	gdp_growth_rate	NUMERIC(3, 1)	темпы роста ВВП, %

27	gdp_growth_rate_5_year	NUMERIC(3, 1)	среднегодовой рост ВВП за пять лет

28	gdp_per_capita_ppp	NUMERIC(7, 1)	ВВП на душу населения (с поправкой на ППС), разделенный на численность населения, $

29	unemployment	NUMERIC(3, 1)	уровень безработицы, %

30	inflation	NUMERIC(6, 2)	инфляция – годовое процентное изменение цен, %

31	fdi_inflow_millions	INT	приток прямых иностранных инвестиций (ППИ), млн $

32	public_debt_% of_gdp	NUMERIC(3, 1)	государственный долг в % от ВВП


## общее количество стран
SELECT

     count(*)

FROM

     public_freedom.index_2022;
 
          output:

                    count
                    184


## страны, для которых рейтинг отсутствует

SELECT

	country_id,
	country_name,
	score_2022

FROM

	public_freedom.index_2022

WHERE

	 score_2022 IS NULL;

          
          output:

                    country_id	country_name	score_2022

                    1	Afghanistan	NULL
                    77	Iraq	NULL
                    96	Libya	NULL
                    97	Liechtenstein	NULL
                    184	Somalia	NULL
                    159	Syria	NULL
                    181	Yemen	NULL

### то есть для 177 стран Индекс экономической свободы 2022 рассчитан
## пятерка стран с самым высоким рейтингом

SELECT

	world_rank,
	country_id,
	country_name,
	score_2022

FROM

	public_freedom.index_2022

ORDER BY

	world_rank

LIMIT 5;

               output:

                    world_rank	country_id	country_name	score_2022
                         1	147	Singapore	     84.4
                         2	158	Switzerland	84.2
                         3	78	Ireland	     82
                         4	120	New Zealand	80.6
                         5	99	Luxembourg	80.6


## пятерка стран с худшим рейтингом

SELECT 
	world_rank,
	country_id,
	country_name,
	score_2022
FROM
	public_freedom.index_2022
ORDER BY
	score_2022
LIMIT 5;


world_rank	country_id	country_name	score_2022
177	87	Korea, North 	3
176	179	Venezuela	24.8
175	42	Cuba	29.5
174	154	Sudan	32
173	183	Zimbabwe	33.1


## позиция Беларуси в рейтинге
SELECT 
	world_rank,
	country_id,
	country_name,
	score_2022
FROM
	public_freedom.index_2022
WHERE 
	country_name = 'Belarus';


|world_rank|country_id|country_name|score_2022|
|135|14|Belarus|53|




количество уникальных регионов

SELECT 
	DISTINCT region
FROM
	public_freedom.index_2022;


region
Sub-Saharan Africa
Europe
Asia-Pacific
Americas
Middle East and North Africa



оценка экономической свободы Economic Freedom Scores 
Free ● 80–100 свободный
Mostly Free ●70–79.9 в основном свободный
Moderately Free● 60–69.9 умеренно свободный
Mostly Unfree ●50–59.9 в основном несвободный
Repressed ● 0–49.9 подавленный, репрессированный
● Not Graded 

количество стран в в категории свободный

SELECT 
	COUNT(*)
FROM 
	public_freedom.index_2022
WHERE
	score_2022 >= 80;


count
7

страны в категории свободный

SELECT 
	country_name,
	world_rank,
	score_2022,
	'free' AS "category"
FROM 
	public_freedom.index_2022
WHERE
	score_2022 >= 80
ORDER BY
	world_rank;


country_name	world_rank	score_2022	category
Singapore	1	84.4	free
Switzerland	2	84.2	free
Ireland	3	82	free
New Zealand	4	80.6	free
Luxembourg	5	80.6	free
Taiwan 	6	80.1	free
Estonia	7	80	free


количество стран по категориям

SELECT
	count(country_name),
	CASE
	WHEN score_2022 >= 80 THEN 'free'
	WHEN score_2022 < 80 AND score_2022 >= 70 THEN 'mostly_free'
	WHEN score_2022 < 70 AND score_2022 >= 60 THEN 'moderately_free'
	WHEN score_2022 < 60 AND score_2022 >= 50 THEN 'mostly_unfree'
	WHEN score_2022 < 50 THEN 'repressed'
	WHEN score_2022 IS NULL THEN 'not_grated'
	END AS rating 
FROM 
  public_freedom.index_2022
GROUP BY
	2
ORDER BY
	1 DESC;

count	rating
57	mostly_unfree
54	moderately_free
32	repressed
27	mostly_free
7	not_grated
7	free



country_name	score_2022	category
Belarus	53	mostly_unfree

топ 10 стран по количеству населения

SELECT
	region,
	country_name,
	population_millions
FROM 
  public_freedom.index_2022
ORDER BY
	population_millions DESC
limit 10;


region	country_name	population_millions
Asia-Pacific	China	1402.112
Asia-Pacific	India	1380.004
Americas	United States	329.484
Asia-Pacific	Indonesia	273.524
Asia-Pacific	Pakistan	220.892
Americas	Brazil	212.559
Sub-Saharan Africa	Nigeria	206.14
Asia-Pacific	Bangladesh	164.689
Europe	Russia	144.104
Americas	Mexico	128.933


Сортировка по категориям индекса и ВВП на душу населения

SELECT
	ROUND(AVG(gdp_per_capita_ppp),1) AS avg_gdp_per_capita,
	CASE
	WHEN score_2022 >= 80 THEN 'free'
	WHEN score_2022 < 80 AND score_2022 >= 70 THEN 'mostly_free'
	WHEN score_2022 < 70 AND score_2022 >= 60 THEN 'moderately_free'
	WHEN score_2022 < 60 AND score_2022 >= 50 THEN 'mostly_unfree'
	WHEN score_2022 < 50 THEN 'repressed'
	WHEN score_2022 IS NULL THEN 'not_grated'
	END AS rating 
FROM 
  public_freedom.index_2022
GROUP BY
	2
ORDER BY
	1 DESC;


avg_gdp_per_capita,"rating"
73972.9,"free"
42518.7,"mostly_free"
21803.1,"moderately_free"
9916.8,"mostly_unfree"
6873.8,"repressed"
3019.7,"not_grated"

 средний индекс ЕПИ в зависимости от категории страны

 SELECT
	ROUND(AVG(epi_2022),1) AS avg_epi,
	CASE
	WHEN index_2022 >= 80 THEN 'free'
	WHEN index_2022 < 80 AND index_2022 >= 70 THEN 'mostly_free'
	WHEN index_2022 < 70 AND index_2022 >= 60 THEN 'moderately_free'
	WHEN index_2022 < 60 AND index_2022 >= 50 THEN 'mostly_unfree'
	WHEN index_2022 < 50 THEN 'repressed'
	END AS rating 
FROM 
  public_freedom.epi
GROUP BY
	2
ORDER BY
	1 DESC;


avg_epi	rating
58.6	free
58.5	mostly_free
44.8	moderately_free
36.8	mostly_unfree
35.6	repressed
