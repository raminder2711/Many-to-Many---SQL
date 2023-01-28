# Many-to-Many---SQL

Create a new Database rev

    CREATE DATABASE revs;
    
  ![DB](https://user-images.githubusercontent.com/119749518/215277864-28df7ddc-9656-474e-a07f-dc388de6da26.png)


Create 3 tables

    CREATE TABLE reviewers (
        id INT PRIMARY KEY AUTO_INCREMENT,
        first_name VARCHAR(50) NOT NULL,
        last_name VARCHAR(50) NOT NULL
    );
 
    CREATE TABLE series (
        id INT PRIMARY KEY AUTO_INCREMENT,
        title VARCHAR(100),
        released_year YEAR,
        genre VARCHAR(100)
    );

    CREATE TABLE reviews (
        id INT PRIMARY KEY AUTO_INCREMENT,
        rating DECIMAL(2 , 1 ),
        series_id INT,
        reviewer_id INT,
        FOREIGN KEY (series_id)             #adding Foreign key Constrain
            REFERENCES series (id),         #referencing to series table, id column  
        FOREIGN KEY (reviewer_id)           #adding Foreign key Constrain
            REFERENCES reviewers (id)       #referencing to series table, id column
    );

![table creation 1](https://user-images.githubusercontent.com/119749518/215277900-a704ef23-3f91-47b6-8414-446c5d6bc70b.png)
![table creation 2](https://user-images.githubusercontent.com/119749518/215277908-12e08f65-17d2-4a88-9aed-66736b34cf02.png)


Insert data in 3 tables

    INSERT INTO series (title, released_year, genre) VALUES
        ('Archer', 2009, 'Animation'),
        ('Arrested Development', 2003, 'Comedy'),
        ("Bob's Burgers", 2011, 'Animation'),
        ('Bojack Horseman', 2014, 'Animation'),
        ("Breaking Bad", 2008, 'Drama'),
        ('Curb Your Enthusiasm', 2000, 'Comedy'),
        ("Fargo", 2014, 'Drama'),
        ('Freaks and Geeks', 1999, 'Comedy'),
        ('General Hospital', 1963, 'Drama'),
        ('Halt and Catch Fire', 2014, 'Drama'),
        ('Malcolm In The Middle', 2000, 'Comedy'),
        ('Pushing Daisies', 2007, 'Comedy'),
        ('Seinfeld', 1989, 'Comedy'),
        ('Stranger Things', 2016, 'Drama');


    INSERT INTO reviewers (first_name, last_name) VALUES
        ('Thomas', 'Stoneman'),
        ('Wyatt', 'Skaggs'),
        ('Kimbra', 'Masters'),
        ('Domingo', 'Cortes'),
        ('Colt', 'Steele'),
        ('Pinkie', 'Petit'),
        ('Marlon', 'Crafford');


    INSERT INTO reviews(series_id, reviewer_id, rating) VALUES
        (1,1,8.0),(1,2,7.5),(1,3,8.5),(1,4,7.7),(1,5,8.9),
        (2,1,8.1),(2,4,6.0),(2,3,8.0),(2,6,8.4),(2,5,9.9),
        (3,1,7.0),(3,6,7.5),(3,4,8.0),(3,3,7.1),(3,5,8.0),
        (4,1,7.5),(4,3,7.8),(4,4,8.3),(4,2,7.6),(4,5,8.5),
        (5,1,9.5),(5,3,9.0),(5,4,9.1),(5,2,9.3),(5,5,9.9),
        (6,2,6.5),(6,3,7.8),(6,4,8.8),(6,2,8.4),(6,5,9.1),
        (7,2,9.1),(7,5,9.7),
        (8,4,8.5),(8,2,7.8),(8,6,8.8),(8,5,9.3),
        (9,2,5.5),(9,3,6.8),(9,4,5.8),(9,6,4.3),(9,5,4.5),
        (10,5,9.9),
        (13,3,8.0),(13,4,7.2),
        (14,2,8.5),(14,3,8.9),(14,4,8.9);
        
![insert values 1](https://user-images.githubusercontent.com/119749518/215277919-9cc9977e-0b7d-4968-9d26-5669c1ded2d9.png)


Show Tables

    SHOW TABLES;

![show tables](https://user-images.githubusercontent.com/119749518/215277936-34e85e8a-0536-4e64-aa92-51286a63212c.png)

    
checking structures of tables

    DESC reviewers;
    
    DESC reviews;
    
    DESC series;

![Str(reviewers)](https://user-images.githubusercontent.com/119749518/215277951-5a405a5a-f8ef-4f00-bc52-550be54349b7.png)
![str(reviews)](https://user-images.githubusercontent.com/119749518/215277953-9e274ef7-a780-4419-adfb-4bc6b730eb4b.png)
![str(series)](https://user-images.githubusercontent.com/119749518/215277954-78dbd376-b1ed-4c1e-85e9-001660866ed8.png)
 
Let's check the data as well

    SELECT * FROM reviewers;

    SELECT * FROM reviews;
    
    SELECT * FROM series;
    
 ![reviewers table data](https://user-images.githubusercontent.com/119749518/215277986-1ec58eaa-351d-4ca7-ab2d-d10cbee48340.png)

 ![reviews table data](https://user-images.githubusercontent.com/119749518/215277997-56dac8c3-83a0-443b-8cac-d7fe184c375a.png)

 ![series table data](https://user-images.githubusercontent.com/119749518/215278006-fc36c5f8-ebb1-4516-89b1-ae7c820d9356.png)



nOW LETSS PLAY

find avg rating of all titles and sorted by lowest to highest

    SELECT
        title,
        AVG(rating) AS Average_rating
    FROM
        series
    JOIN reviews ON series.id = reviews.series_id
    GROUP BY
        title
    ORDER BY
        Average_rating;
    
![image](https://user-images.githubusercontent.com/119749518/215279026-959493f9-d27f-4c54-97f0-e8785f47c1a5.png)

We can round the rating by using Round

    SELECT
        title,
        ROUND(AVG(rating), 2) AS Average_rating     
    FROM
        series
    JOIN reviews ON series.id = reviews.series_id
    GROUP BY
        title
    ORDER BY
        Average_rating;
    
![image](https://user-images.githubusercontent.com/119749518/215279250-543637df-afd9-4a27-8eaf-abbe47c1cd16.png)
   
    
 now join reviewer with reviews 
 
     SELECT
        CONCAT(first_name, ' ', last_name) AS 'Name of Reviewer',
        rating
    FROM
        reviewers
    JOIN reviews ON reviewers.id = reviews.reviewer_id;
 
 ![image](https://user-images.githubusercontent.com/119749518/215279522-9a4638da-72ff-4c18-9fb8-da562d757753.png)

 
 
 
 
 
 
 
 
    
