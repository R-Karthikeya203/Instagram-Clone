-- Challenges
-- Challenge 1 - Finding 5 oldest users
select user_name, created_at from users order by created_at limit 5;
-- Challenge 2 - Most Popular Registration Date
select dayname(created_at) as dday, count(*) as total from users group by dday order by total desc limit 2;
-- Challenge 3 - Find the users who have never posted a photo.
select * from photos;
select * from users;
select * from users left join photos on photos.user_id = users.id where image_url is null;
-- Challenge 4 - What is the single most liked photos in our database?
select * from likes;
select user_name, photos.id, image_url, count(*) as likes from photos join likes 
on photos.id = likes.photo_id join users on photos.user_id = users.id group by photo_id order by likes desc limit 1;
-- Challenge 5 - How many times does a average user post?
select (select count(*) from photos) / (select count(*) from users) as avg_post;
-- Challenge 6 - What are the top 5 commoly used hashtags?
select * from tags;
select id, tag_name, count(*) as total from photo_tags join tags on tags.id = photo_tags.tag_id 
group by tags.id order by total desc limit 5;
-- Challenge 7 - Find the users who have liked every photo on the site?
SELECT user_name, Count(*) AS num_likes FROM users INNER JOIN likes 
ON users.id = likes.user_id GROUP  BY likes.user_id HAVING num_likes = (SELECT Count(*) FROM   photos); 
