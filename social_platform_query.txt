use social_platform;

# 1. Seleziona gli utenti che hanno postato almeno un video
SELECT DISTINCT u.*
FROM users AS u
JOIN medias AS m ON m.user_id = u.id
WHERE m.type LIKE 'video';

# 2. Seleziona tutti i post senza Like (13)
SELECT p.title as 'post senza likes'
FROM posts AS p
LEFT JOIN likes AS l ON l.post_id = p.id
WHERE l.post_id IS NULL;

# 3. Conta il numero di like per ogni post (152)
SELECT p.title AS 'Post', count(*) AS 'like per ogni post'
FROM likes AS l
JOIN posts AS p ON l.post_id = p.id
GROUP BY p.id, p.title;

# 4. Ordina gli utenti per il numero di media caricati (25)
SELECT u.username, count(m.id) AS numero_media
FROM users AS u
LEFT JOIN medias AS m ON m.user_id = u.id
GROUP BY u.username
ORDER BY numero_media;

# 5. Ordina gli utenti per totale di likes ricevuti nei loro posts (25)
SELECT u.username, count(l.post_id) AS numero_likes
FROM users AS u
JOIN posts AS p ON p.user_id = u.id
LEFT JOIN likes AS l ON l.post_id =  p.id
GROUP BY u.username
ORDER BY numero_likes;