--=============== МОДУЛЬ 5. РАБОТА С POSTGRESQL =======================================
--= ПОМНИТЕ, ЧТО НЕОБХОДИМО УСТАНОВИТЬ ВЕРНОЕ СОЕДИНЕНИЕ И ВЫБРАТЬ СХЕМУ PUBLIC===========
SET search_path TO public;

--======== ОСНОВНАЯ ЧАСТЬ ==============

--ЗАДАНИЕ №1
--Сделайте запрос к таблице payment и с помощью оконных функций добавьте вычисляемые колонки согласно условиям:
--Пронумеруйте все платежи от 1 до N по дате платежа

select payment_id ,payment_date ,row_number() over ( order by payment_date)
 from payment p 

--Пронумеруйте платежи для каждого покупателя, сортировка платежей должна быть по дате платежа

 select customer_id ,payment_id ,payment_date ,row_number() over (partition by customer_id order by payment_date)
 from payment p 

--Посчитайте нарастающим итогом сумму всех платежей для каждого покупателя, сортировка должна 
  быть сперва по дате платежа, а затем по размеру платежа от наименьшей к большей

select customer_id ,payment_id ,payment_date, amount ,
sum (amount) over (PARTITION BY customer_id ORDER BY payment_date, amount)
as sum 
from payment 


--Пронумеруйте платежи для каждого покупателя по размеру платежа от наибольшего к
  меньшему так, чтобы платежи с одинаковым значением имели одинаковое значение номера.

select customer_id ,payment_id ,payment_date, amount , 
 dense_rank() over (partition by customer_id order by amount desc)
 from payment  
order by customer_id 

--Можно составить на каждый пункт отдельный SQL-запрос, а можно объединить все колонки в одном запросе.





--ЗАДАНИЕ №2
--С помощью оконной функции выведите для каждого покупателя стоимость платежа и стоимость 
--платежа из предыдущей строки со значением по умолчанию 0.0 с сортировкой по дате платежа.

select customer_id, payment_id, payment_date, amount,
lag(amount,1,0.) over (partition by customer_id order by payment_date) as last_amount
from payment 
order by customer_id




--ЗАДАНИЕ №3
--С помощью оконной функции определите, на сколько каждый следующий платеж покупателя больше или меньше текущего.


select customer_id, payment_id, payment_date, amount,
amount - lead(amount,1,0.) over (partition by customer_id  order by payment_date, customer_id) as raznica_plateja
from payment 



--ЗАДАНИЕ №4
--С помощью оконной функции для каждого покупателя выведите данные о его последней оплате аренды.

select distinct customer_id,
    first_value(payment_id) over (partition by customer_id order by payment_date desc),
    first_value(payment_date) over (partition by customer_id order by payment_date desc),
    first_value(amount) over (partition by customer_id order by payment_date desc)
from payment 
order by customer_id



--======== ДОПОЛНИТЕЛЬНАЯ ЧАСТЬ ==============

--ЗАДАНИЕ №1
--С помощью оконной функции выведите для каждого сотрудника сумму продаж за август 2005 года 
--с нарастающим итогом по каждому сотруднику и по каждой дате продажи (без учёта времени) 
--с сортировкой по дате.




--ЗАДАНИЕ №2
--20 августа 2005 года в магазинах проходила акция: покупатель каждого сотого платежа получал
--дополнительную скидку на следующую аренду. С помощью оконной функции выведите всех покупателей,
--которые в день проведения акции получили скидку




--ЗАДАНИЕ №3
--Для каждой страны определите и выведите одним SQL-запросом покупателей, которые попадают под условия:
-- 1. покупатель, арендовавший наибольшее количество фильмов
-- 2. покупатель, арендовавший фильмов на самую большую сумму
-- 3. покупатель, который последним арендовал фильм






