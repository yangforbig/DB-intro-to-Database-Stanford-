# SQL

- SQL Movie-Rating Query Exercises Core Set[Post-Deadline Practice]

- SQL Social-Network Query Exercises Core Set[Post-Deadline Practice]

- SQL Movie-Rating Modification Exercises [Post-Deadline Practice]

Q3: For all movies that have an average rating of 4 stars or higher, add 25 to the release year. (Update the existing tuples; don't insert new tuples.) 

update Movie
set year = year + 25
where mID in (select mID
              from Rating
              group by mID
              having Avg(stars) >= 4)

Q4:  Remove all ratings where the movie's year is before 1970 or after 2000, and the rating is fewer than 4 stars. 

delete from Rating
where mID in(select R.mID as mID
             from Rating R join Movie M using (mID)
             where (M.year < 1970 or M.year > 2000) and R.stars < 4);
                          





- SQL Social-Network Modification Exercises [Post-Deadline Practice]
