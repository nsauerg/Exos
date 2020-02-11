

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

# 2. Ecrire la requête qui affiche les catégories dans les quels « JOHNNY LOLLOBRIGIDA » totalise plus de 3 films.
```
USE sakila;

SELECT 
	category.name,
	count(film.film_id) as nb_film
FROM film

JOIN film_actor
ON film.film_id = film_actor.film_id
JOIN actor
ON film_actor.actor_id = actor.actor_id AND actor.last_name = 'LOLLOBRIGIDA' AND actor.first_name = 'JOHNNY'
JOIN film_category
ON film_actor.film_id = film_category.film_id 
JOIN category
ON film_category.category_id = category.category_id

GROUP BY category.name
HAVING nb_film >= 3;
```

# 3. Afficher la durée moyenne d'emprunt des films par acteurs.
```
USE sakila;

SELECT 
	actor.first_name,
	actor.last_name,
	avg(film.rental_duration)
FROM film

JOIN film_actor
ON film.film_id = film_actor.film_id
JOIN actor
ON film_actor.actor_id = actor.actor_id

GROUP BY actor.actor_id ORDER BY moy_dur desc;
```

# 4. L'argent total dépensé au vidéo club pour chaque client, classé par ordre décroissant.
```
USE sakila;

SELECT 
	customer.first_name,
	customer.last_name,
	sum(payment.amount) as argtot
FROM payment

JOIN customer 
ON payment.customer_id = customer.customer_id
GROUP BY customer.customer_id
ORDER BY argtot desc;
```
