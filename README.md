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

    


