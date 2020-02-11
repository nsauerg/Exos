

# 1. Afficher le nombre de films dans lesquels à joué l'acteur « JOHNNY LOLLOBRIGIDA », regroupés par catégorie.

```
USE sakila;

SELECT 
	actor.first_name, 
	actor.last_name, 
    count(film.film_id),
    category.name
FROM film

JOIN film_actor
ON film.film_id = film_actor.film_id
JOIN actor
ON film_actor.actor_id = actor.actor_id AND actor.last_name = 'LOLLOBRIGIDA' AND actor.first_name = 'JOHNNY'
JOIN film_category
ON film_actor.film_id = film_category.film_id 
JOIN category
ON film_category.category_id = category.category_id

GROUP BY category.name;
```
