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
















