# IMDB_Movies Using SQL
 # Project Overview

   
**Project Title**: IMBD_Movies    
**Level**: Intermediate  
**Database**: `imdb_movies`


This project demonstrates the implementation of a IMDB_Movies Management using SQL. It includes creating and managing tables, performing CRUD operations, and executing advanced SQL queries. The goal is to showcase skills in database design, manipulation, and querying.

![IMDB_Movies_project](https://github.com/Sanjeev027/IMDB_Movies/blob/main/Imdb.jpg.png)

## Objectives

1. **Set up the IMDB_Movies Management Database**: Create and populate the database with tables for Actor, Box_office, Director, Genre, Rating, Movies.
2. **CRUD Operations**: Perform Create, Read, Update, and Delete operations on the data.
3. **Filtering & Aggregation and Joints & Relationships.**
4. **Common Table Expressions 'CTE's', Sub Quries & Window funtions.**

## Project Structure

## Tools 
- Sql
- MySQl
## ER_Diagram
![IMDB_Movies_project](https://github.com/Sanjeev027/IMDB_Movies/blob/main/ER_Diagram.png)

## Relationships:
Movies is directed by Directors (One-to-Many: One director can direct many movies, but each movie is directed by one director).

Movies is acted by Actors (Many-to-Many: A movie can have many actors, and an actor can act in many movies).

Movies belongs to Genres (Many-to-Many: A movie can belong to multiple genres, and a genre can have multiple movies).

Movies has Ratings (One-to-One: Each movie has one rating, and each rating belongs to one movie).

Movies has Financials (One-to-One: Each movie has one financial record, and each financial record belongs to one movie).

## Project Structure :

 - **Database Creation** : Created a database named `Movies_db`.
 - **Table Creation** : Created tables for Movies, , Directors, Genre, Actors, Rating, and Financials status. Each table includes relevant columns and relationships.

 ```sql
#Create DataBase.
create database IMDB_Movies;

#Use Datbase.
use IMDB_Movies;

#Show Tables from using DataBase.
show tables;

CREATE TABLE Movies (
    MovieID INT AUTO_INCREMENT PRIMARY KEY,
    Title VARCHAR(255) NOT NULL,
    ReleaseYear INT,
    Runtime INT,
    Overview TEXT,
    Certificate VARCHAR(10)
);
CREATE TABLE Directors (
    DirectorID INT AUTO_INCREMENT PRIMARY KEY,
    Name VARCHAR(255) NOT NULL
);
CREATE TABLE Genres (
    GenreID INT AUTO_INCREMENT PRIMARY KEY,
    GenreName VARCHAR(50) NOT NULL
);
CREATE TABLE Actors (
    ActorID INT AUTO_INCREMENT PRIMARY KEY,
    Name VARCHAR(255) NOT NULL
);
CREATE TABLE Ratings (
    RatingID INT AUTO_INCREMENT PRIMARY KEY,
    MovieID INT,
    IMDB_Rating DECIMAL(3,1),
    MetaScore INT,
    No_of_Votes INT,
    FOREIGN KEY (MovieID) REFERENCES Movies(MovieID)
);
CREATE TABLE Financials (
    FinancialID INT AUTO_INCREMENT PRIMARY KEY,
    MovieID INT,
    Gross BIGINT,
    FOREIGN KEY (MovieID) REFERENCES Movies(MovieID)
);

```

### 2.CRUD Operations

- **Create**: Inserted sample records into the tables.
- **Read**: Retrieved and displayed data from various tables.
- **Update**: Updated records in the `movies` table.
- **Delete**: Removed records from the `genre` table as needed.

**1. Insert data into Created Tables.**
```sql
INSERT INTO Directors (Name) VALUES
('Frank Darabont'), ('Francis Ford Coppola'), ('Christopher Nolan'), ('Sidney Lumet'), ('Peter Jackson'),
('Steven Spielberg'), ('Martin Scorsese'), ('James Cameron'), ('Quentin Tarantino'), ('David Fincher'),
('Ridley Scott'), ('Alfred Hitchcock'), ('Stanley Kubrick'), ('Tim Burton'), ('Clint Eastwood'),
('Robert Zemeckis'), ('Woody Allen'), ('Wes Anderson'), ('Coen Brothers'), ('George Lucas'),
('Michael Bay'), ('Guy Ritchie'), ('Bryan Singer'), ('Denis Villeneuve'), ('Sam Mendes'),
('Paul Thomas Anderson'), ('Alejandro G. Iñárritu'), ('Greta Gerwig'), ('Jordan Peele'), ('M. Night Shyamalan'),
('John Carpenter'), ('Taika Waititi'), ('Baz Luhrmann'), ('Darren Aronofsky'), ('Rian Johnson'),
('Lana Wachowski'), ('Lilly Wachowski'), ('James Wan'), ('Kenneth Branagh'), ('Gareth Edwards'),
('Guillermo del Toro'), ('Spike Lee'), ('Sofia Coppola'), ('Richard Linklater'), ('Terrence Malick'),
('David Lynch'), ('John Hughes'), ('Mel Gibson'), ('Jean-Pierre Jeunet'), ('David O. Russell');

select * from directors;

INSERT INTO Genres (MovieID) VALUES
('Action'), ('Adventure'), ('Animation'), ('Biography'), ('Comedy'),
('Crime'), ('Documentary'), ('Drama'), ('Family'), ('Fantasy'),
('Film-Noir'), ('History'), ('Horror'), ('Music'), ('Musical'),
('Mystery'), ('Romance'), ('Sci-Fi'), ('Sport'), ('Thriller');

select * from Genres;

INSERT INTO Actors (Name) VALUES
('Leonardo DiCaprio'), ('Robert De Niro'), ('Morgan Freeman'), ('Tom Hanks'), ('Meryl Streep'),
('Denzel Washington'), ('Brad Pitt'), ('Johnny Depp'), ('Cate Blanchett'), ('Scarlett Johansson'),
('Al Pacino'), ('Christian Bale'), ('Hugh Jackman'), ('Matt Damon'), ('Nicole Kidman'),
('Anne Hathaway'), ('Emma Stone'), ('Ryan Gosling'), ('Samuel L. Jackson'), ('Harrison Ford'),
('Joaquin Phoenix'), ('Tom Cruise'), ('Natalie Portman'), ('Mark Ruffalo'), ('Keanu Reeves'),
('Charlize Theron'), ('Benedict Cumberbatch'), ('Daniel Day-Lewis'), ('Javier Bardem'), ('Chris Hemsworth');

select * from actors;

INSERT INTO Movies (Title, ReleaseYear, Runtime, Overview, Certificate) VALUES
('The Shawshank Redemption', 1994, 142, 'Two imprisoned men bond over a number of years...', 'A'),
('The Godfather', 1972, 175, 'An organized crime dynasty''s aging patriarch transfers control...', 'A'),
('The Dark Knight', 2008, 152, 'When the menace known as the Joker wreaks havoc...', 'UA'),
('The Godfather: Part II', 1974, 202, 'The early life and career of Vito Corleone...', 'A'),
('12 Angry Men', 1957, 96, 'A jury holdout attempts to prevent a miscarriage of justice...', 'U'),
('Pulp Fiction', 1994, 154, 'The lives of two mob hitmen, a boxer, and a gangster''s wife intertwine...', 'A'),
('Fight Club', 1999, 139, 'An insomniac office worker forms an underground fight club...', 'A'),
('Forrest Gump', 1994, 142, 'The presidencies of Kennedy and Johnson through a man with low IQ...', 'U'),
('Inception', 2010, 148, 'A thief who enters the dreams of others to steal secrets...', 'UA'),
('The Matrix', 1999, 136, 'A computer hacker learns about the true nature of reality...', 'UA');

select * from movies;

INSERT INTO Ratings (MovieID, IMDB_Rating, MetaScore, No_of_Votes) VALUES
(1, 9.3, 80, 2343110),
(2, 9.2, 100, 1620367),
(3, 9.0, 84, 2303232),
(4, 9.0, 90, 1129952),
(5, 9.0, 96, 689845),
(6, 8.9, 94, 1852347),
(7, 8.8, 76, 1974521),
(8, 8.8, 82, 1895432),
(9, 8.7, 74, 2301345),
(10, 8.7, 73, 1684532);

select * from ratings;

INSERT INTO Financials (MovieID, Gross) VALUES
(1, 28341469),
(2, 134966411),
(3, 534858444),
(4, 57300000),
(5, 4360000),
(6, 107928762),
(7, 100853753),
(8, 678000000),
(9, 836848102),
(10, 463517383);

select * from financials;
```


**For UPDATE & DELETE OPERATIONS.**
- Using My_sql to write an command for using the commands like update & Delete.
- 0 for safe mode off, 1 for safe mode on.
```sql 
set sql_safe_updates = 0;
```

**2 : Update an Existing Record From Movies Table.**

```sql
update movies 
set Title = 'The Matrix Part - 1'
where movieID = 10;
```

**3 : Delete a Record From Genre Table.**
```sql
delete from genres
where Genrename = 'comedy';
```

## 📝 Basic Queries.

**1. Retrieve all movie titles and their release years.**

```sql 
select title,ReleaseYear from movies;
 ```
**2.Find all movies that were released after the year 2000.**

```sql
select * from movies
where ReleaseYear > 2000;
```

**3.List all directors in alphabetical order.**
```sql
select * from directors
order by name asc;
```
**4.Show the top 10 movies with the highest IMDb rating.**
``` sql
select m.title,r.IMDB_Rating from ratings r
join movies m
where m.MovieID = r.MovieID
order by IMDB_Rating desc 
limit 10;
```

**5.Find movies with a runtime greater than 150 minutes.**
```sql
select * from movies
where Runtime > 150;
```

## 🔍 Filtering and Aggregation.

**6.List movies that have a certificate of "A" (Adult).**
```sql
select * from movies
where Certificate = 'A';
```
**7.Find the total number of movies in the database.**
```sql
select count(*) as Total_Movies from movies;
```
**8.Get the average IMDb rating of all movies.**
```sql
select avg(IMDB_Rating) as Average_Rating  from ratings;
```
**9.Find the highest-grossing movie.**
```sql
select f.Gross,m.Title from financials f
join movies m
where m.movieid = f. movieid
order by Gross desc
limit 1;
```

## 🔗 Joins & Relationships.


**10.Find all movies directed by "Christopher Nolan.**
```sql
select m.Title,d.name from movies m
join directors d
on m.MovieID = d.DirectorID
where d.name = 'Christopher Nolan'; 
```
**11.Retrieve movies along with their IMDb rating.**
```sql
select m.Title,r.imdb_rating from movies m
join ratings r
on r.movieid = m.MovieID;
```
**12.Get the total box office earnings for each movie.**
```sql
select f.Gross,m.Title from movies m
join financials f
on f.MovieID = m.MovieID
order by gross desc;
```
**13.Find the movie with the most votes.**
```sql
select r.No_of_Votes,m.Title from ratings r
join movies m
on r.MovieID=m.MovieID
order by No_of_Votes desc;
```
**14.Find the average IMDB rating of all movies in the dataset.**
```sql
select avg(IMDB_Rating) from ratings;
```
**15.Calculate the total box office gross of all movies combined from the Financials dataset.**
```sql
SELECT SUM(Gross) AS Total_Box_Office_Gross 
FROM Financials;
```
##  Window Functions().
**16.Rank movies based on their IMDB rating, partitioned by their release year.**

```sql
select m.title,m.releaseyear,r.imdb_rating,
rank() over (partition by m.releaseyear order by r.imdb_rating desc ) as rank_
from ratings r
join movies m 
on m.movieid = r.movieid;
```
**17.Find the cumulative total gross earnings of movies in descending order of release year.**
```sql
SELECT 
    m.title, 
    m.releaseyear, 
    f.gross, 
    SUM(f.gross) OVER (ORDER BY m.releaseyear DESC ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) AS cumulative_gross
FROM movies m
JOIN financials f ON m.movieid = f.movieid
ORDER BY m.releaseyear DESC;
```
**18.Show each movie’s IMDB rating along with the difference between its rating and the average rating across all movies.**
 ```sql
SELECT 
    M.Title, 
    R.IMDB_Rating, 
    R.IMDB_Rating - AVG(R.IMDB_Rating) OVER () AS Rating_Difference
FROM Movies M
JOIN Ratings R ON M.MovieID = R.MovieID;
```
## CTE's & Subquries.
**19.Find the top 3 highest-grossing movies
 Use a CTE to first rank movies based on their total gross earnings, then filter the top 3.**
```sql
WITH RankedMovies AS (
    SELECT 
        m.title, 
        f.gross,
        RANK() OVER (ORDER BY f.gross DESC) AS rank_
    FROM movies m
    JOIN financials f ON m.movieid = f.movieid
)
SELECT title, gross, rank_
FROM RankedMovies
WHERE rank_ <= 3;
```
**20.List movies with a higher IMDB rating than the average rating
Use a CTE to calculate the average IMDB rating, then select movies with ratings above this value.**
```sql
WITH AvgRating AS (
    SELECT AVG(imdb_rating) AS avg_rating FROM ratings
)
SELECT 
    m.title, 
    r.imdb_rating
FROM movies m
JOIN ratings r ON m.movieid = r.movieid
CROSS JOIN AvgRating
WHERE r.imdb_rating > AvgRating.avg_rating;
```

**Subquries**
**21.Find the movie with the highest IMDB rating.**
**without subquery.**
```sql
select * from ratings
order by IMDB_Rating desc
limit 1;
```
**with subquery.**
```sql
select * from ratings
where imdb_rating = (select max(imdb_rating) from ratings);
```
**22.Retrieve the names of movies with an IMDB rating higher than the average rating of all movies.**
```sql
select m.title,r.imdb_rating from movies m 
left join ratings r on r.movieid = m.movieid
where r.imdb_rating > (select avg(imdb_rating) from ratings);
```
**23.List movies that made more revenue than the average gross earnings of all movies.**
```sql
select m.title,f.gross from movies m 
join financials f on m.movieid = f.movieid
where f.gross > (select avg(gross) from financials);
```
 ## Conclusion.
 - This project demonstrates the application of SQL skills in creating and managing a IMDB_Movies. 






