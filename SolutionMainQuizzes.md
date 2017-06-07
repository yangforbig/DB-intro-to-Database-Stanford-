# SQL

- SQL Movie-Rating Query Exercises Core Set[Post-Deadline Practice]

- SQL Social-Network Query Exercises Core Set[Post-Deadline Practice]

- SQL Movie-Rating Modification Exercises [Post-Deadline Practice]


Q3: For all movies that have an average rating of 4 stars or higher, add 25 to the release year. (Update the existing tuples; don't insert new tuples.) 

```
update Movie
set year = year + 25
where mID in (select mID
              from Rating
              group by mID
              having Avg(stars) >= 4)
```

Q4:  Remove all ratings where the movie's year is before 1970 or after 2000, and the rating is fewer than 4 stars. 

```
delete from rating
where mID in (select mID from movie
              where year <1970 or year > 2000) and stars < 4;
```

- SQL Social-Network Modification Exercises [Post-Deadline Practice]

Q2: If two students A and B are friends, and A likes B but not vice-versa, remove the Likes tuple. 


```
delete from Likes
where ID2 in (select ID2 
              from Friend 
              where Likes.ID1 = ID1) 
      and
      ID2 not in (select Likes.ID2
                  from Likes L 
                  where Likes.ID1 = L.ID2);

```






