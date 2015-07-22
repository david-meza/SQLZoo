# SQLZoo
Exercises from SQL Zoo

By: David Meza (https://github.com/david-meza)
Nick Sarlo (https://github.com/sicknarlo)

#Solutions

## Select Basics

    SELECT population FROM world
    WHERE name = 'Germany'

    SELECT name, gdp/population FROM world
    WHERE area > 5000000

    SELECT name , continent
    FROM world
    WHERE area < 2000
      AND gdp > 5000000000

    SELECT name, population FROM world
    WHERE name IN ('Finland', 'Norway',
                 'Denmark', 'Sweden')

    SELECT name FROM world
    WHERE name LIKE 'G%'

    SELECT name, area/1000 AS area_in_thousands 
    FROM world
    WHERE area BETWEEN 200000 AND 250000


## Select from World

    SELECT name, continent, population FROM world


    SELECT name FROM world
    WHERE population>200000000

    SELECT name, gdp/population AS per_capita_gdp
    FROM world
    WHERE population > 200000000

    SELECT name, population/1000000 AS pop_in_millions
    FROM world
    WHERE continent = 'South America'

    SELECT name, population
    FROM world
    WHERE name IN ('France', 'Germany', 'Italy')

    SELECT name
    FROM world
    WHERE name LIKE '%united%'

    SELECT name, population, area
    FROM world
    WHERE area > 3000000 or population >250000000


    SELECT name, population, area
    FROM world
    WHERE (area < 3000000 AND population > 250000000)
    OR (area > 3000000 AND population < 250000000)

    SELECT name, ROUND(population/1000000, 2), ROUND(gdp/1000000000, 2)
    FROM world
    WHERE continent = "South America"

    SELECT name, ROUND(gdp/population, -3)
    FROM world
    WHERE gdp >= 1000000000000

    SELECT name,
        CASE WHEN continent='Oceania' THEN 'Australasia'
            ELSE continent END
      FROM world
     WHERE name LIKE 'N%'


    SELECT name,
        CASE WHEN continent = "Europe" THEN "Eurasia"
             WHEN continent = "Asia" THEN "Eurasia"
             WHEN continent = "North America" THEN "America"
             WHEN continent = "South America" THEN "America"
             WHEN continent = "Caribbean" THEN "America"
             ELSE continent END
    FROM world
    WHERE name LIKE 'A%' OR name LIKE 'B%'

    SELECT name, continent,
    CASE WHEN continent = 'Oceania' THEN 'Australasia'
         WHEN (continent = 'Eurasia' OR name = 'Turkey') THEN 'Europe/Asia'
         WHEN continent = 'Caribbean' AND name LIKE 'B%' THEN 'North America'
         WHEN continent = 'Caribbean' AND name NOT LIKE 'B%' THEN 'South America'
    ELSE continent end
    FROM world
    ORDER BY name



## Select from Nobel

    SELECT yr, subject, winner
    FROM nobel
   WHERE yr = 1950

    SELECT winner
    FROM nobel
    WHERE yr = 1962
    AND subject = 'Literature'

    SELECT yr, subject
    FROM nobel
    WHERE winner = 'Albert Einstein'

    SELECT winner
    FROM nobel
    WHERE yr >= 2000 and subject = 'Peace'

    SELECT yr, subject, winner
    FROM nobel
    WHERE yr BETWEEN 1980 AND 1989 AND subject = 'Literature'


    SELECT *
    FROM nobel
    WHERE winner IN ('Theodore Roosevelt', 'Woodrow Wilson', 'Jimmy Carter')


    SELECT winner
    FROM nobel
    WHERE winner LIKE 'John%'


    SELECT *
    FROM nobel
    WHERE (subject = 'Physics' AND yr = 1980) OR (subject = 'Chemistry' AND yr = 1984)


    SELECT *
    FROM nobel
    WHERE subject != 'Chemistry' AND subject != 'Medicine' AND yr = 1980


    SELECT *
    FROM nobel
    WHERE (subject = 'Medicine' AND yr < 1910)
    OR (subject = 'Literature' AND yr >= 2004)


    SELECT *
    FROM nobel
    WHERE winner = 'Peter Grünberg'


    SELECT *
    FROM nobel
    WHERE winner = 'Eugene O\'Neill'


    SELECT winner, yr, subject
    FROM nobel
    WHERE winner LIKE 'Sir%'
    ORDER BY yr DESC, winner ASC


    SELECT winner, subject, subject IN ('Physics','Chemistry')
    FROM nobel
    WHERE yr=1984
    ORDER BY subject IN ('Physics','Chemistry') ASC,subject, winner



## [The JOIN Operation](http://sqlzoo.net/wiki/The_JOIN_operation)


    SELECT matchid, player
    FROM goal 
    WHERE teamid = 'GER'

    SELECT DISTINCT id,stadium,team1,team2
    FROM game JOIN goal ON goal.matchid = game.id
    WHERE id = 1012

    SELECT player,teamid,mdate
    FROM game JOIN goal ON (id=matchid)
    WHERE teamid='GER'

    SELECT team1,team2,player
    FROM game JOIN goal ON (id=matchid)
    WHERE player LIKE 'Mario%'

    SELECT player, teamid, coach, gtime
    FROM goal JOIN eteam ON teamid=id
    WHERE gtime<=10

    SELECT mdate,teamname
    FROM game JOIN eteam ON (team1=eteam.id)
    WHERE coach = 'Fernando Santos'

    SELECT player
    FROM goal JOIN game ON goal.matchid=id
    WHERE stadium = 'National Stadium, Warsaw'

### More difficult Questions

    SELECT DISTINCT(player)
    FROM game JOIN goal ON matchid = id
    WHERE (team1='GER' OR team2='GER') AND teamid != 'GER'


    SELECT teamname, COUNT(*)
    FROM eteam JOIN goal ON id=teamid
    GROUP BY teamname
    ORDER BY teamname


    SELECT stadium, COUNT(*)
    FROM game JOIN goal ON id = matchid
    GROUP BY stadium
    ORDER BY stadium


    SELECT matchid,mdate, COUNT(*)
    FROM game JOIN goal ON matchid = id 
    WHERE (team1 = 'POL' OR team2 = 'POL')
    GROUP BY matchid


    SELECT matchid,mdate, COUNT(*)
    FROM game JOIN goal ON matchid = id 
    WHERE teamid = 'GER'
    GROUP BY matchid


    SELECT DISTINCT mdate, 
    team1,
    SUM(CASE WHEN teamid=team1 THEN 1 ELSE 0 END) score1, 
    team2, 
    SUM(CASE WHEN teamid=team2 THEN 1 ELSE 0 END) score2
    FROM game LEFT JOIN goal ON matchid = id
    GROUP BY id
    ORDER BY mdate,team1,team2


## More JOIN operations

    SELECT id, title
    FROM movie
    WHERE yr=1962


    SELECT yr
    FROM movie
    WHERE title='Citizen Kane'


    SELECT id, title, yr
    FROM movie
    WHERE title LIKE '%Star Trek%'
    ORDER BY yr


    SELECT title
    FROM movie
    WHERE id IN (11768, 11955, 21191)
    ORDER BY title


    SELECT DISTINCT(actor.id)
    FROM movie JOIN casting ON movie.id = casting.movieid 
              JOIN actor ON casting.actorid = actor.id
    WHERE actor.name = 'Glenn Close'

    SELECT id
    FROM movie
    WHERE title='Casablanca'

    SELECT name
    FROM casting JOIN actor ON casting.actorid = actor.id
    WHERE movieid=11768

    SELECT name
    FROM casting JOIN actor ON casting.actorid = actor.id
                 JOIN movie ON casting.movieid = movie.id
    WHERE title='Alien'

    SELECT title
    FROM casting JOIN actor ON casting.actorid=actor.id
                 JOIN movie ON casting.movieid=movie.id
    WHERE actor.name='Harrison Ford'    

    SELECT title
    FROM casting JOIN actor ON casting.actorid=actor.id
                 JOIN movie ON casting.movieid=movie.id
    WHERE actor.name ='Harrison Ford'AND casting.ord > 1


    SELECT title, name
    FROM actor JOIN casting ON casting.actorid = actor.id
               JOIN movie   ON casting.movieid = movie.id
    WHERE ord = 1 AND movie.yr = 1962


    SELECT yr,COUNT(title) FROM
      movie JOIN casting ON movie.id=movieid
             JOIN actor   ON actorid=actor.id
    WHERE name='John Travolta'
    GROUP BY yr
    HAVING COUNT(title)=(SELECT MAX(c) FROM
    (SELECT yr,COUNT(title) AS c FROM
       movie JOIN casting ON movie.id=movieid
             JOIN actor   ON actorid=actor.id
     WHERE name='John Travolta'
     GROUP BY yr) AS t
    )


    SELECT title, actor.name
    FROM casting JOIN movie ON casting.movieid = movie.id
                       JOIN actor ON casting.actorid = actor.id
    WHERE ord = 1 AND movieid IN (SELECT movieid FROM casting
    WHERE actorid IN (
    SELECT id FROM actor
    WHERE name='Julie Andrews'))


    SELECT name
    FROM casting JOIN actor ON casting.actorid=actor.id
                JOIN movie on casting.movieid=movie.id
    WHERE ord = 1
    GROUP BY name
    HAVING SUM(ord) >= 30
    ORDER BY SUM(ord) desc

    -- This one was showing errors

    SELECT title, count(actorid)
    FROM casting JOIN actor ON casting.actorid=actor.id
                JOIN movie on casting.movieid=movie.id
    WHERE yr = 1978
    GROUP BY movie.id
    ORDER BY COUNT(actorid) DESC


    SELECT DISTINCT name
    FROM casting  JOIN actor ON casting.actorid=actor.id
                  JOIN movie on casting.movieid=movie.id
    WHERE movieid IN (SELECT movieid
                      FROM casting JOIN actor ON casting.actorid=actor.id AND actor.name = 'Art Garfunkel'
                      JOIN movie on casting.movieid=movie.id) 
    AND name != 'Art Garfunkel'
    ORDER BY name ASC


## [SUM and COUNT](http://sqlzoo.net/wiki/SUM_and_COUNT)

    SELECT SUM(population)
    FROM world


    SELECT DISTINCT continent
    FROM world


    SELECT SUM(gdp)
    FROM world
    WHERE continent = 'Africa'


    SELECT COUNT(area)
    FROM world
    WHERE area > 1000000



    SELECT SUM(population)
    FROM world
    WHERE name IN ('France','Germany','Spain')


    SELECT continent, COUNT(name)
    FROM world
    GROUP BY continent



    SELECT continent, COUNT(name)
    FROM world
    WHERE population > 10000000
    GROUP BY continent



    SELECT continent
    FROM world
    GROUP BY continent
    HAVING SUM(population) >= 100000000



## [SELECT within SELECT](http://sqlzoo.net/wiki/SELECT_within_SELECT_Tutorial)


    SELECT name FROM world
    WHERE population >
      (SELECT population FROM world
      WHERE name='Russia')


    SELECT name FROM world
    WHERE continent = 'Europe' AND gdp/population >
      (SELECT gdp/population FROM world
      WHERE name='United Kingdom')

      SELECT name, continent
        FROM world
        WHERE continent IN (
          SELECT continent
          FROM world
          WHERE name IN ('Argentina', 'Australia')
              )
        ORDER BY name ASC

        SELECT name, population
        FROM world
        WHERE population > (
            SELECT population
            FROM world
            WHERE name='Canada'
            ) AND population < (
            SELECT population
            FROM world
            WHERE name='Poland'
            )

    SELECT name, CONCAT(ROUND((population / (
    SELECT population
    FROM world
    WHERE name='Germany'
    )) * 100, 0), '%')
    FROM world
    where continent = 'Europe'

    SELECT name
    FROM world
    WHERE gdp > ALL(SELECT gdp
                      FROM world
                         WHERE continent='Europe' AND gdp IS NOT NULL)


    SELECT continent, name FROM world x
      WHERE name <= ALL
        (SELECT name FROM world y
            WHERE y.continent=x.continent
              AND area>0)

    SELECT name, continent, population
    FROM world x
    WHERE 25000000 >= ALL(SELECT population
    FROM world
    WHERE continent= x.continent)

    SELECT name, continent
    FROM world x
    WHERE population / 3 > ALL(SELECT population
    FROM world
    WHERE continent = x.continent AND name != x.name)

    SELECT name
    FROM teacher
    WHERE dept IS NULL

    SELECT teacher.name, dept.name
     FROM teacher LEFT JOIN dept
             ON (teacher.dept=dept.id)

     SELECT teacher.name, dept.name
     FROM teacher RIGHT JOIN dept
           ON (teacher.dept=dept.id)

    SELECT name, COALESCE(mobile, '07986 444 2266')
    FROM teacher

    SELECT teacher.name, COALESCE(dept.name, 'None')
     FROM teacher LEFT JOIN dept
           ON (teacher.dept=dept.id)

    SELECT COUNT(*), COUNT(mobile)
    FROM teacher

    SELECT dept.name, COUNT(teacher.name)
    FROM teacher RIGHT JOIN dept ON teacher.dept=dept.id
    GROUP BY dept.name

    SELECT name,
    CASE WHEN dept = 1 THEN 'Sci'
         WHEN dept = 2 THEN 'Sci'
         ELSE  'Art' END
    FROM teacher

    SELECT name,
    CASE WHEN dept = 1 OR dept = 2 THEN 'Sci'
         WHEN dept = 3 THEN 'Art'
         ELSE 'None' END
    FROM teacher


## [Self JOIN](http://sqlzoo.net/wiki/Self_join)


SELECT COUNT(*)
FROM stops


SELECT id
FROM stops
WHERE name = 'Craiglockhart'


SELECT id, name
FROM route JOIN stops ON stop = id
WHERE company = 'LRT' AND num = 4


SELECT company, num, COUNT(*)
FROM route WHERE stop=149 OR stop=53
GROUP BY company, num
HAVING COUNT(*) = 2


SELECT a.company, a.num, a.stop, b.stop
FROM route a JOIN route b ON
  (a.company=b.company AND a.num=b.num)
WHERE a.stop=53 AND b.stop = 149


SELECT a.company, a.num, stopa.name, stopb.name
FROM route a JOIN route b ON
  (a.company=b.company AND a.num=b.num)
  JOIN stops stopa ON (a.stop=stopa.id)
  JOIN stops stopb ON (b.stop=stopb.id)
WHERE stopa.name='Craiglockhart' AND stopb.name = 'London Road'


SELECT DISTINCT a.company, a.num
FROM route a JOIN route b ON
  (a.company=b.company AND a.num=b.num)
WHERE a.stop=115 AND b.stop = 137


SELECT a.company, a.num
FROM route a JOIN route b ON
  (a.company=b.company AND a.num=b.num)
  JOIN stops stopa ON (a.stop=stopa.id)
  JOIN stops stopb ON (b.stop=stopb.id)
WHERE stopa.name='Craiglockhart' AND stopb.name = 'Tollcross'


SELECT stopb.name, a.company, a.num
FROM route a JOIN route b ON
  (a.company=b.company AND a.num=b.num)
  JOIN stops stopa ON (a.stop=stopa.id)
  JOIN stops stopb ON (b.stop=stopb.id)
WHERE stopa.name='Craiglockhart'


SELECT   a.num, a.company, 
             trans1.name ,  c.num,  c.company
FROM route a JOIN route b
ON (a.company = b.company AND a.num = b.num)
JOIN ( route c JOIN route d ON (c.company = d.company AND c.num= d.num))
JOIN stops start ON (a.stop = start.id)
JOIN stops trans1 ON (b.stop = trans1.id)
JOIN stops trans2 ON (c.stop = trans2.id)
JOIN stops end ON (d.stop =  end.id)
WHERE  start.name = 'Craiglockhart' AND end.name = 'Sighthill'
            AND  trans1.name = trans2.name 
ORDER BY LENGTH(a.num)


