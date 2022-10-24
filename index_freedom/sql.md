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



# Monthly Sales by Segment (Ежемесячные продажи по сегментам)
## общие продажи по сегментам

     \select segment, count(sales) 
     FROM public.orders
     group by segment;\

     segment    |count|
     Consumer   | 5191|
     Corporate  | 3020|
     Home Office| 1783|