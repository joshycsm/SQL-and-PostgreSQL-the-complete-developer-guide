# SQL-and-PostgreSQL-the-complete-developer-guide

<table>
<tr>
<th id="table-of-contents"> Table of Contents </th>
<th> Table of Contents (cont'd) </th>
</tr>
<tr>
<td>

[Section 1: Simple - But Powerful - SQL Statements](##section-1-Simple---But-Powerful---SQL-Statements)

[Section 2: Filtering Records](##section-2-Filtering-Records)

[Section 3: Working with Tables](##section-3-Working-with-Tables)

[Section 4: Relating Records with Joins](##section-4-Relating-Records-with-Joins)

[Section 5: Aggregation of Records](##section-5-Aggregation-of-Records)

[Section 6: Working with Large Datasets](##section-6-Working-with-Large-Datasets)

[Section 7: Sorting Records](##section-7-Sorting-Records)

[Section 8: Unions and Intersections with Sets](##section-8-Unions-and-Intersections-with-Sets)

[Section 9: Assembling Queries with SubQueries](##section-9-Assembling-Queries-with-SubQueries)

[Section 10: Selecting Distinct Records](##section-10-Selecting-Distinct-Records)

[Section 11: Utility Operators, Keywords, and Functions](##section-11-Utility-Operators-Keywords-and-Functions)

[Section 12: Local PostgreSQL Installation](##section-12-Local-PostgreSQL-Installation)

[Section 13: PostgreSQL Complex Datatypes](##section-13-PostgreSQL-Complex-Datatypes)

[Section 14: Database-Side Validation and Constraints](##section-14-Database-Side-Validation-and-Constraints)

[Section 15: Database Structure Design Patterns](##section-15-Database-Structure-Design-Patterns)

[Section 16: How to Build a 'Like' System](##section-16-How-to-Build-a-Like-System)

[Section 17: How to Build a 'Mention' System](##section-17-How-to-Build-a-Mention-System)

[Section 18: How to Build a 'Hashtag' System](##section-18-How-to-Build-a-Hashtag-System)

</td>
<td>

[Section 19: How to Design a 'Follower' System](##section-19-How-to-Design-a-Follower-System)

[Section 20: Implementing Database Design Patterns](##section-20-Implementing-Database-Design-Patterns)

[Section 21: Approaching and Writing Complex Queries](##section-21-Approaching-and-Writing-Complex-Queries)

[Section 22: Understanding the Internals of PostgreSQL](##section-22-Understanding-the-Internals-of-PostgreSQL)

[Section 23: A Look at Indexes for Performance](##section-23-A-Look-at-Indexes-for-Performance)

[Section 24: Basic Query Tuning](##section-24-Basic-Query-Tuning)

[Section 25: Advanced Query Tuning](##section-25-Advanced-Query-Tuning)

[Section 26: Simple Common Table Expressions](##section-26-Simple-Common-Table-Expressions)

[Section 27: Recursive Common Table Expressions](##section-27-Recursive-Common-Table-Expressions)

[Section 28: Simplifying Queries with Views](##section-28-Simplifying-Queries-with-Views)

[Section 29: Optimizing Queries with Materialized Views](##section-29-Optimizing-Queries-with-Materialized-Views)

[Section 30: Handling Concurrency and Reversibility with Transactions](##section-30-Handling-Concurrency-and-Reversibility-with-Transactions)

[Section 31: Managing Database Design with Schema Migrations](##section-31-Managing-Database-Design-with-Schema-Migrations)

[Section 32: Schema vs Data](##section-32-Schema-vs-Data)

[Section 33: Accessing PostgreSQL From API's](##section-33-Accessing-PostgreSQL-From-APIs)

[Section 34: Data Access Pattern - Repositories](##section-34-Data-Access-Pattern---Repositories)

[Section 35: Security Around PostgreSQL](##section-35-Security-Around-PostgreSQL)

[Section 36: Fast Parallel Testing](##section-36-Fast-Parallel-Testing)

[Section 37: Bonus!](##section-37-Bonus!)

</td>
</tr>
</table>

## Section 1: Simple - But Powerful - SQL Statements

## 38min

### [Back to Table of Contents](##table-of-contents)

### 1. Join Our Community!

-

### 2. What is PostgreSQL All About?

- Challenges of Postgres: <br>
  1. Writing efficient queries to retrieve information
  2. Designing the schema, or structure, of the database
  3. Understanding when to use advanced features
  4. Managing the database in a production environment
- #1 is probably the most important thing we need to know how to do.
- #2 can be hard to decide what approach is best and concerns to take into consideration
- #3 Postgres has a lot of special features, sometimes helpful sometimes not
- #4 Scaling the database is important and there are many techniques behind this

### 3. Database Design

- Database Design Process: <br>

  1. What kind of thing are we storing?
  2. What properties does this thing have?
  3. What type of data does each of those properties contain?

  - #1 We should create a table called 'cities'
  - #2 The table should have columns of name, country, population, area
  - #3 Each column should indicate the type of data that it is going to store

- QUIZ 1: Database Terminology <br>
  1. A table stores a list of records, like a list of to do items, a list of photos, or a list of cities

### 4. Creating Tables

- pg-sql.com: Tool to get a free Postgres database + run some queries
-       CREATE TABLE cities (
        name VARCHAR(50),
        country VARCHAR(50),
        population INTEGER,
        area INTEGER
        );

### 5. Analyzing CREATE TABLE

- Identifier - lowercase; Keyword - CAPITAL
- Column Data Types: <br>
  1. VARCHAR(50) - Variable length character. Text! If we put in a string longer than 50 charaters, we'll get an error
  2. INTEGER - Number without a decimal. +/- 2,147,483,647. Anything larger or smaller = error!

### 6. Inserting Data Into a Table

-       INSERT INTO cities (name, country, population, area)
        VALUES ('Tokyo', 'Japan', 28505000, 8223);
- You can insert multiple rows at once
-       INSERT INTO cities (name, country, population, area)
        VALUES
        ('Delhi', 'India', 28125000, 2240),
        ('Shanghai', 'China', 22125000, 4015),
        ('Sao Paulo', 'Brazil', 20935000, 3043);

### 7. Retrieving Data with Select

-       SELECT * FROM cities;

### Coding Exercise 1.: Create, Insert, and Select!

-       CREATE TABLE movies (
            title VARCHAR(60),
            box_office INTEGER
        );
-       INSERT INTO movies (title, box_office)
        VALUES
            ('The Avengers', 1500000000),
            ('Batman v Superman', 873000000);
-       SELECT * FROM movies

### 8. Calculated Columns

- SQL is not just about pulling raw data out of a table
- We can write SQL to _transform_ or _process_ data before we recieve it!
- Math Operators: <br>
  -       |/ - Square Root
          @ Absolute Value
          % Remainder
          ^ Exponent
-       SELECT name, population / area AS               population_density
        FROM cities;

### 9. Calculating Phone Revenue

-       CREATE TABLE phones (
            name VARCHAR(50),
            manufacturer VARCHAR(50),
            price INTEGER,
            units_sold INTEGER,
        );

-       INSERT INTO phones (name, manufacturer, price, units_sold)
        VALUES
            ('N8', 'Nokia', 150, 7543),
            ('Droid', 'Motorola', 150, 8395),
            ('Wave S8500', 'Samsung', 175, 9259);

- Coding Exercies 2: Using Calculated Columns <br>

-     SELECT name, price \* units_sold AS revenue
        FROM phones;

### 10. Exercise Solution

- COMPLETE

### 11. String Operators and Functions

- || -> Join two string (string operator)
- Functions:
  1. CONCAT() -> Join two strings
  2. LOWER() -> Gives a lower case string
  3. UPPER() -> Gives a upper case string
  4. LENGTH() -> Gives number of characters in a string
-       SELECT name || ', ' || country AS location
        FROM cities;
-       SELECT CONCAT(name, ', ', country) AS location
        FROM cities;
-       SELECT
        CONCAT(UPPER(name), ', ', UPPER(country)) AS location
        FROM
        cities;
-       SELECT
            UPPER(CONCAT(name, ', ', country)) AS location
        FROM
            cities;

## Section 2: Filtering Records

## 30min

### [Back to Table of Contents](##table-of-contents)

### 12. Filtering Rows with "Where"

-       SELECT name, area
        FROM cities
        WHERE area > 4000
- First thing that really happens internally is Postgres takes a look at the data source and sees you're trying to pull in all the different rows from the cities table. It then filters to apply the where criteria to remove some rows out of the result set. and then for all the remaining entries, it will select some number of columns.
- FROM first, WHERE second, SELECT third

### 13. More on the "Where" Keyword

- WHERE: allows us to filter down the results we get from our query
- Comparison Math Operators: <br>
  1. IN - Is the value present in a list?
  2. BETWEEN - Is the value between two other values?
  3. NOT IN - Is the value _not_ present in a list
-       SELECT
            name,
            area
        FROM
            cities
        WHERE
            area = 8223;

### 14. Compound "Where" Clauses

-       SELECT
            name,
            area
        FROM
            cities
        WHERE
            area BETWEEN 2000 AND 4000;
-       SELECT
            name,
            area
        FROM
            cities
        WHERE
            name IN('Delhi', 'Shanghai');
-       SELECT
            name,
            area
        FROM
            cities
        WHERE
            area NOT IN(3043, 8223);
-       SELECT
            name,
            area
        FROM
            cities
        WHERE
            area NOT IN(3043, 8223) AND name = 'Delhi';
-       SELECT
            name,
            area
        FROM
            cities
        WHERE
            area NOT IN(3043, 8223)
            OR name = 'Delhi'
            OR name = 'Tokyo';

### 15. A "Where" Exercise Overview

- complete.

- Coding Exercise 3: Practicing Where Statements (complete)

### 16. A "Where" Solution

-       SELECT name, price
        FROM phones
        WHERE units_sold > 5000

### 17. "Where" With Lists

- complete

- Coding Exercise 4: A More Challenging 'Where' (complete)

### 18. A "Where" With Lists Solution

-       SELECT name, manufacturer
        FROM phones
        WHERE manufacturer IN ('Apple', 'Samsumg')

### 19. Calculations in "Where" Clauses

- mathematical operations will run before tesing for inequality
-       SELECT
            name,
            population / area AS population_density
        FROM
          cities
        WHERE
          population / area > 6000

- Coding Exercise 5: Trying Calcluations in Where Clauses (complete)

### 20. Solving Calculations

-       SELECT
            name,
            price * unit sold AS total_revenue
        FROM
            phones
        WHERE
            price * unit sold > 1000000;

### 21. Updating Rows

-       UPDATE cities
        SET population = 39505000
        WHERE name = 'Tokyo' AND country = 'Japan'
-       SELECT * FROM cities
- be cautious when writing WHERE statements. we will come up with fool proof plan for updating statements soon.

### 22. Deleting Rows

-       DELETE FROM cities
        WHERE name = 'Tokyo' AND country = 'Japan'
-       INSERT INTO cities (name, country, population, area)
        VALUES ('Tokyo', 'Japan', 38505000, 8223)
-       SELECT * FROM cities

- Coding Exercise 6: Try Updating Records In a Table! (complete)

### 23. A Solution for Updating Rows

-       UPDATE phones
        SET units_sold = 8543
        WHERE name = 'N8';
-       SELECT * FROM phones;

- Coding Exercise 7: Practice Deleting Records (complete)

### 24. Solution for Deleting Rows

-       DELETE FROM phones
        WHERE manufacturer = 'Samsung';
-       SELECT * FROM phones;

## Section 3: Working with Tables

## 1hr 18min

### [Back to Table of Contents](##table-of-contents)

### 25. The Plan Moving Forward

- One table per database is rare.
- Database For a Photo-Sharing App: users, photos, comments, likes.

### 26. Approaching Database Design

- What Tables Should We Make? <br>
  1. Common features (like authentication, comments, etc) are frequently built with conventional table names and columns
  2. What type of resources exist in your app? Create a separate table for each of these features
  3. Features that seem to indicate a _relationship or ownership_ between two types of resources need to be reflected in our table design

QUIZ 2: Let's Design Some Schema - complete

### 27. One-to-Many and Many-to-Many Relationships

- First 2 Kinds of Relationships <br>
  1. One-to-Many Relationship: A user has many photos (i.e. 'has many' represents a 1:m)
  2. Many-to-One Relationship: A photo has one user (i.e. 'has one' represnets a m:1)
- A photo has many comments
- A comment has one photo.
- a Boat has many crew members, a school has many students, a company has many employees
- A crew member has one boat, a student belongs to one school, a employee has one company
- How to relate different records in our database with a 1:m or m:1? We will learn this next.

QUIZ 3: A 'Has One' or 'Has Many'? - complete

### 28. One-to-Many and Many-to-Many Relationships

- Database containing users, photos, comments, and likes only contains one-to-many and many-to-one relationships

- Two other important relationships, many-to-one and one-to-one.

- One-To-One Relationships:

  - definition: Exactly one record that has a relationship to exactly one another record. Opposite is true for the other record.

  1. Examples: Boats Captains; Company CEO; Capitol Country; Student Desk; Person Driver's License

- Many-To-Many Relationships:

  1. Students Classes; Tasks Engineers; Players Football Matches; Movies Actors / Actresses; Conference Calls Employees (time-based)

QUIZ 4: Identifying One-to-One and Many-to-Many Relationships - complete

### 29. Primary and Foreign Keys

- How to set up some kind of relationship in a table?
- Primary Key - Uniquely identifes this record in this table; identify an indivdual row inside a table
- Foreign Key - Identifies a record (usually in another table) that this row is associated with; foreign used to relate one record with another and set up a relationship
- With photos and users table we can set up a one to many and many to one relationship by inserting a foreign key in the table that belongs to the other table.

### 30. Understanding Foreign Keys

- **Comments have one photo**
- Comments table should get a foreign key column **pointing at the photo** each comment belongs to
- **Comments have one user**
- Comments table should get a foreign key column **pointing at the user** each comment belongs to

- **The 'many side of the relationship gets the foreign key column**
- comments table gets the foreign key column pointing at 'photo'
- comments table gets the foreign key column pointing at 'user'
- foreign key columns will set up all the different relationships we have. It's the only way so have to understand how it works!!! very mechanical process so just learn it correctly one time and makes sense forever.
- Primary Keys:
  1. Each row in every table has one primary key
  2. No other row in the _same table_ can have the same value
  3. 99% of the time called 'id'
  4. Either an integer or a UUID (Universaly Unique ID)
  5. Will never change
- Foreign Keys:
  1. Rows only have this if they _belong to_ another record
  2. Many rows in the same table can have the same foreign key
  3. Name varies, usually called something like 'xyz_id'
  4. Exactly equal to the primary key of the referenced row
  5. Will change if the relationship changes.

QUIZ 5: Foreign Keys: How Do They Work? - complete

### 31. Auto-Generated ID's

- Generate a table of users
- users table needs username column
- helper from postgres, SERIAL datatype ()
- as we add users ids will be generated with the next available unique interger
-       CREATE TABLE users(
            id SERIAL PRIMARY KEY,
            username VARCHAR(50)
        );
-       INSERT INTO users (username)
        VALUES
            ('monahan93'),
            ('pferrer'),
            ('si93onis'),
            ('99stroman');
-       SELECT * FROM users
-       CREATE TABLE photos (
            id SERIAL PRIMARY KEY,
            url VARCHAR(200),
            user_id INTEGER REFERENCES users(id)
        );
-       INSERT INTO photos (url, user_id)
        VALUES
          ('http://one.jpg', 4);
-       SELECT * FROM photos;

### 32. Creating Foreign Key Columns

- included in 31.

### 33. Running Queries on Associated Data

-       INSERT INTO photos (url, user_id)
        VALUES
            ('http://two.jpg', 1),
            ('http://25.jpg', 1),
            ('http://36.jpg', 1),
            ('http://754.jpg', 2),
            ('http://35.jpg', 3),
            ('http://256.jpg', 4);
-       SELECT * FROM photos
- Find all the photos created by user with ID 4
-       SELECT * FROM photos
        WHERE user_id = 4;
- List all photos with details about the associated user for each
-       SELECT url, username FROM photos
        JOIN users ON users.id = photos.user_id
- This is a join. We will go into great detail on it shortly!

### 34. Exercise Overview

- Relate the crew members and boats
- write a query to fetch all the crew members associated with the boat that has an ID of 1
- in certain SQL instances:
-       id INTEGER PRIMARY KEY AUTOINCREMENT
  VS
-       id SERIAL PRIMARY KEY

- Coding Exercise 8: Creating and Using Foreign Keys (complete)

### 35. Foreign Key Creation Solution

- SQL code:
  - Create table called 'boats'
-       CREATE TABLE boats (
            -- Note that this environment doesn't support 'SERIAL' keyowrd
            -- so 'AUTOINCREMENT' is used instead. Postgres always uses 'SERIAL'
            id INTEGER PRIMARY KEY AUTOINCREMENT,
            name VARCHAR
        );

  - Insert two boats

-       INSERT INTO boats (name)
        VALUES ('Rogue Wave'), ('Harbor Master');

  - Create table called 'crew members'

-       CREATE TABLE crew_members (
            id INTEGER PRIMARY KEY AUTOINCREMENT,
            first_name VARCHAR,
            -- todo #1 below
            boat_id INTEGER REFERENCES boats(id)
        );

  - Insert three crew members

-       INSERT INTO crew_members(first_name, boat_id)
        VALUES ('Alex', 1), ('Lucia', 1), ('Ari', 2);

  - Write query here to fetch all columns for all crew_members associated with the boat that has an ID of 1
  - TODO #2 BELOW

-       SELECT * FROM crew_members
        <!-- JOIN boats ON boats.id = crew_members.boat_id -->
        WHERE boat_id = 1

### 36. Foreign Key Constraints Around Insertion

- DATA CONSISTENT: ability of our database to make sure the info we are inserting into it and working with makes sense and all different references between tables line up in some way
- 3 scenarios:
  1. We insert a photo that is tied to a user that exists -> Everthing works OK!
  2. We insert a photo that refers to a user that doesn't exist -> An error! (violates foreign key constraint because it does not exist right now)
  3. We insert a photo that isn't tied to any user -> Put in a value of 'NULL' for the user_id

### 37. Constraints Around Deletion

- When we use a foreign key we can specify some options if we delete a primary key that is referenced in another table: (What happens if you try to delete a user when a photo is still referencing it... on delete options below)
  1. ON DELETE RESTRICT -> Throw an error (violates foreign key constraint)
  2. ON DELETE NO ACTION -> Throw an error
  3. ON DELETE CASCADE -> Delete the photo too!
  4. ON DELETE SET NULL -> Set the 'user_id' of the photo to 'NULL'
  5. ON DELETE SET DEFAULT -> Set the 'user_id' of the photo to a default value, if one is provided

### 38. Commands You'll Need for the Next Video

- The next video will involve creating and deleting the photos table several times.

- To avoid having to retype out the CREATE TABLE and INSERT INTO several times, here are the commands that we are going to run a few times. You should copy-paste these somewhere for just a moment - we will run them several times in the next video.

CREATE TABLE photos (
id SERIAL PRIMARY KEY,
url VARCHAR(200),
user_id INTEGER REFERENCES users(id)
);

INSERT INTO photos (url, user_id)
VALUES
('http:/one.jpg', 4),
('http:/two.jpg', 1),
('http:/25.jpg', 1),
('http:/36.jpg', 1),
('http:/754.jpg', 2),
('http:/35.jpg', 3),
('http:/256.jpg', 4);

### 39. Testing Deletion Constraints

- testing different constraints:
  1.  ON DELETE CASCADE
      -       DROP TABLE photos
      -       SELECT * FROM photos
      - create photos table again with ON DELETE CASCASDE and run below:
  -       DELETE FROM users
          WHERE id = 1
  -       SELECT * FROM photos

### 40. Setting Foreign Keys to Null on Delete

- testing different constraints:

  1.  ON DELETE SET NULL
      -       DROP TABLE photos
      -       SELECT * FROM photos
      - create photos table again and run below:
      -         CREATE TABLE photos (
                    id SERIAL PRIMARY KEY,
                    url VARCHAR(200),
                    user_id INTEGER REFERENCES users(id) ON DELETE SET NULL
                );
      -          INSERT INTO photos (url, user_id)
                VALUES
                    ('http:/one.jpg', 4),
                    ('http:/754.jpg', 2),
                    ('http:/35.jpg', 3),
                    ('http:/256.jpg', 4);

  -       DELETE FROM users
    WHERE id = 4
  -       SELECT * FROM photos

QUIZ 6: What Happens On Delete? - complete

### 41. Adding Some Complexity

- We've seen how to set up relationships between different tables
- We've seen some simple queries
- We've seen how to clean up these relationships
- Lets' add in 'comments' then figure out how to write a few super common queries
- Schema diagram: photos has id (serial), url (varchar(200)), user_id (integer); users has id (serial), username (varchar(40)); comments has id (serial), photo_id (integer), user_id (integer), contents (varchar(240))

## Section 4: Relating Records with Joins

## 1hr 20min

### [Back to Table of Contents](##table-of-contents)

### 42. Adding Some Data

CREATE TABLE users(
id SERIAL PRIMARY KEY,
username VARCHAR(50)
);

CREATE TABLE photos (
id SERIAL PRIMARY KEY,
url VARCHAR(200),
user_id INTEGER REFERENCES users(id) ON DELETE CASCADE
);

CREATE TABLE comments (
id SERIAL PRIMARY KEY,
contents VARCHAR(240),
user_id INTEGER references users(id) ON DELETE CASCADE,
photo_id INTEGER references photos(id) ON DELETE CASCADE
);

INSERT INTO users (username)
VALUES
('Reyna.Marvin'),
('Micah.Cremin'),
('Alfredo66'),
('Gerard_Mitchell42'),
('Frederique_Donnelly');

INSERT INTO photos (url, user_id)
VALUES
('https://santina.net', 3),
('https://alayna.net', 5),
('https://kailyn.name', 3),
('http://marjolaine.name', 1),
('http://chet.net', 5),
('http://jerrold.org', 2),
('https://meredith.net', 4),
('http://isaias.net', 4),
('http://dayne.com', 4),
('http://colten.net', 2),
('https://adelbert.biz', 5),
('http://kolby.org', 1),
('https://deon.biz', 2),
('https://marina.com', 5),
('http://johnson.info', 1),
('https://linda.info', 2),
('https://tyrique.info', 4),
('http://buddy.info', 5),
('https://elinore.name', 2),
('http://sasha.com', 3);

INSERT INTO comments (contents, user_id, photo_id)
VALUES
('Quo velit iusto ducimus quos a incidunt nesciunt facilis.', 2, 4),
('Non est totam.', 5, 5),
('Fuga et iste beatae.', 3, 3),
('Molestias tempore est.', 1, 5),
('Est voluptatum voluptatem voluptatem est ullam quod quia in.', 1, 5),
('Aut et similique porro ullam.', 1, 3),
('Fugiat cupiditate consequatur sit magni at non ad omnis.', 1, 2),
('Accusantium illo maiores et sed maiores quod natus.', 2, 5),
('Perferendis cumque eligendi.', 1, 2),
('Nihil quo voluptatem placeat.', 5, 5),
('Rerum dolor sunt sint.', 5, 2),
('Id corrupti tenetur similique reprehenderit qui sint qui nulla tenetur.', 2, 1),
('Maiores quo quia.', 1, 5),
('Culpa perferendis qui perferendis eligendi officia neque ex.', 1, 4),
('Reprehenderit voluptates rerum qui veritatis ut.', 1, 1),
('Aut ipsum porro deserunt maiores sit.', 5, 3),
('Aut qui eum eos soluta pariatur.', 1, 1),
('Praesentium tempora rerum necessitatibus aut.', 4, 3),
('Magni error voluptas veniam ipsum enim.', 4, 2),
('Et maiores libero quod aliquam sit voluptas.', 2, 3),
('Eius ab occaecati quae eos aut enim rem.', 5, 4),
('Et sit occaecati.', 4, 3),
('Illum omnis et excepturi totam eum omnis.', 1, 5),
('Nemo nihil rerum alias vel.', 5, 1),
('Voluptas ab eius.', 5, 1),
('Dolor soluta quisquam voluptatibus delectus.', 3, 5),
('Consequatur neque beatae.', 4, 5),
('Aliquid vel voluptatem.', 4, 5),
('Maiores nulla ea non autem.', 4, 5),
('Enim doloremque delectus.', 1, 4),
('Facere vel assumenda.', 2, 5),
('Fugiat dignissimos dolorum iusto fugit voluptas et.', 2, 1),
('Sed cumque in et.', 1, 3),
('Doloribus temporibus hic eveniet temporibus corrupti et voluptatem et sint.', 5, 4),
('Quia dolorem officia explicabo quae.', 3, 1),
('Ullam ad laborum totam veniam.', 1, 2),
('Et rerum voluptas et corporis rem in hic.', 2, 3),
('Tempora quas facere.', 3, 1),
('Rem autem corporis earum necessitatibus dolores explicabo iste quo.', 5, 5),
('Animi aperiam repellendus in aut eum consequatur quos.', 1, 2),
('Enim esse magni.', 4, 3),
('Saepe cumque qui pariatur.', 4, 4),
('Sit dolorem ipsam nisi.', 4, 1),
('Dolorem veniam nisi quidem.', 2, 5),
('Porro illum perferendis nemo libero voluptatibus vel.', 3, 3),
('Dicta enim rerum culpa a quo molestiae nam repudiandae at.', 2, 4),
('Consequatur magnam autem voluptas deserunt.', 5, 1),
('Incidunt cum delectus sunt tenetur et.', 4, 3),
('Non vel eveniet sed molestiae tempora.', 2, 1),
('Ad placeat repellat et veniam ea asperiores.', 5, 1),
('Eum aut magni sint.', 3, 1),
('Aperiam voluptates quis velit explicabo ipsam vero eum.', 1, 3),
('Error nesciunt blanditiis quae quis et tempora velit repellat sint.', 2, 4),
('Blanditiis saepe dolorem enim eos sed ea.', 1, 2),
('Ab veritatis est.', 2, 2),
('Vitae voluptatem voluptates vel nam.', 3, 1),
('Neque aspernatur est non ad vitae nisi ut nobis enim.', 4, 3),
('Debitis ut amet.', 4, 2),
('Pariatur beatae nihil cum molestiae provident vel.', 4, 4),
('Aperiam sunt aliquam illum impedit.', 1, 4),
('Aut laudantium necessitatibus harum eaque.', 5, 3),
('Debitis voluptatum nesciunt quisquam voluptatibus fugiat nostrum sed dolore quasi.', 3, 2),
('Praesentium velit voluptatem distinctio ut voluptatum at aut.', 2, 2),
('Voluptates nihil voluptatum quia maiores dolorum molestias occaecati.', 1, 4),
('Quisquam modi labore.', 3, 2),
('Fugit quia perferendis magni doloremque dicta officia dignissimos ut necessitatibus.', 1, 4),
('Tempora ipsam aut placeat ducimus ut exercitationem quis provident.', 5, 3),
('Expedita ducimus cum quibusdam.', 5, 1),
('In voluptates doloribus aut ut libero possimus adipisci iste.', 3, 2),
('Sit qui est sed accusantium quidem id voluptatum id.', 1, 5),
('Libero eius quo consequatur laudantium reiciendis reiciendis aliquid nemo.', 1, 2),
('Officia qui reprehenderit ut accusamus qui voluptatum at.', 2, 2),
('Ad similique quo.', 4, 1),
('Commodi culpa aut nobis qui illum deserunt reiciendis.', 2, 3),
('Tenetur quam aut rerum doloribus est ipsa autem.', 4, 2),
('Est accusamus aut nisi sit aut id non natus assumenda.', 2, 4),
('Et sit et vel quos recusandae quo qui.', 1, 3),
('Velit nihil voluptatem et sed.', 4, 4),
('Sunt vitae expedita fugiat occaecati.', 1, 3),
('Consequatur quod et ipsam in dolorem.', 4, 2),
('Magnam voluptatum molestias vitae voluptatibus beatae nostrum sunt.', 3, 5),
('Alias praesentium ut voluptatem alias praesentium tempora voluptas debitis.', 2, 5),
('Ipsam cumque aut consectetur mollitia vel quod voluptates provident suscipit.', 3, 5),
('Ad dignissimos quia aut commodi vel ut nisi.', 3, 3),
('Fugit ut architecto doloremque neque quis.', 4, 5),
('Repudiandae et voluptas aut in excepturi.', 5, 3),
('Aperiam voluptatem animi.', 5, 1),
('Et mollitia vel soluta fugiat.', 4, 1),
('Ut nemo voluptas voluptatem voluptas.', 5, 2),
('At aut quidem voluptatibus rem.', 5, 1),
('Temporibus voluptates iure fuga alias minus eius.', 2, 3),
('Non autem laboriosam consectetur officiis aut excepturi nobis commodi.', 4, 3),
('Esse voluptatem sed deserunt ipsum eaque maxime rerum qui.', 5, 5),
('Debitis ipsam ut pariatur molestiae ut qui aut reiciendis.', 4, 4),
('Illo atque nihil et quod consequatur neque pariatur delectus.', 3, 3),
('Qui et hic accusantium odio quis necessitatibus et magni.', 4, 2),
('Debitis repellendus inventore omnis est facere aliquam.', 3, 3),
('Occaecati eos possimus deleniti itaque aliquam accusamus.', 3, 4),
('Molestiae officia architecto eius nesciunt.', 5, 4),
('Minima dolorem reiciendis excepturi culpa sapiente eos deserunt ut.', 3, 3);

### 43. Queries with Joins and Aggregrations

- The more tables we have, the more interesting questions we can answer:
  1. Find all the comments for the photo with ID = 3, along with the username of the comment author
  2. Find the **average number of comments** per photo
  3. Find the photo with the **most comments** attached to it
  4. Find the photo with ID = 10 and get the **number of comments** attached to it
  5. Find the user with the most activity (most comments + most photos)
  6. Calculate the **average number of characters** per comment
- We will learn about writing the above queries using joins and aggregration.
- Joins: #1
  - Produces values by merging together rows from different related tables
  - Use a join _most times_ that you're asked to find data that involves multiple resources
- Aggregation: #2-#6
  - Looks at many rows and calculates a single value
  - Words like _'most'_, _'average'_, _'least'_ are a sign that you need to use an aggregration
- We will pose query or question solve it and explain what the query is doing for us in the next sections.

### 44. Joing Data from Different Tables

- **For each comment, show the contents of the comment and the username of the user who wrote the comment**
- relationship between comments and users shows the comments has a user_id. If we can relate the user_id back to the users table, we can solve this problem

        SELECT contents, username
        FROM comments
        JOIN users ON users.id = comments.user_id;

- We are trying to access info in two different tables is a sign we might want to perform a join.
- From does an initial selection of the rows, so take all the different rows from comments.
- when we say join users we want to combine rows from users to match the row from the comments table. It will repeat this iteration for every row inside the 'comments with users' 'imaginary' join table.!!!
- Lots more practice with joins in upcoming sections.

### 45. Another Quick Join

- **For each comment, list the contents of the comment and the URL of the photo the comment was added to**

        SELECT contents, url
        FROM comments
        JOIN photos ON photos.id = comments.photo_id;

### 46. Exercise Overview

- complete

- Coding Exercise 9: Practice Joining Data (complete)

### 47. A Joinful Solution

SELECT title, name
FROM books
JOIN authors ON authors.id = books.author_id;

### 48. Alternate Forms of Syntax

- Notes on Joins:
  - Table order between 'FROM' and 'JOIN' _frequently_ makes a difference (we will discuss this in the next couple sections!)
  - We must give context if column names collide (if you run into a library the confuses showing columns with ambiguity you can use AS keyword to remain the column and show the results; some programs having parsing issues compiling or distinguishing between two columns named identically)
  - Tables can be renamed using the 'AS' keyword (shortened syntax for a table seems to be more common whenever you need to embed alot of different references to your table; you can even drop off AS keyword entirely. but adds alot more clarity that something is going to be renamed)
  - There are a few kinds of joins! (next couple sections we will tackle this)

### 49. Missing Data in Joins

- **SHOW each photo url and the username of the poster**

SELECT url, username
FROM photos
JOIN users ON users.id = photos.user_id;

INSERT INTO photos (url, user_id)
VALUES
('http://banner.jpg', NULL)

- importance of including every photo:
  - might be trying to pull info for all photos to do some sort of data analysis or discover the storage the total photos consume.

### 50. Why Wasn't It Included

- take all the different rows from photos.
- join done to merge all the rows from users where the id matches the user_id from the photos table.
- get user with id null and nothing to match to the row....
- with currrent join if anytin from source table that doesn't match the table from users it does not show up in the final results!!
- good thing we have a couple other join options available that can solve this in upcoming sections!

### 51. Four Kinds of Joins (REFER BACK TO: IMPORTANT!!!)

- TYPES OF JOINS:
  1. Inner Join - joins to tables together in a particular way. INNER JOIN or JOIN; when values that don't match up to rows in other column it will not show up in the final results; we only keep rows that match up to the row in the other table. otherwise they get dropped in the final results.
  2. Left Join - if anything from the photos table does not match up to the users table we will not drop it off or throw it away... we will just put in null values for other columns. left outer join do not throw away from source table!
  3. Right Join - exact opposite of left outer join. All rows that are not matched from non-source will not be dropped and the source table will just go through matching process and leave null rows when combined to non source.
  4. Full Join - just give us everything just try to merge if possible and include all the others.. best to match everything up and also include user with non matching photo and null will be filled for other fields in that row.
- These joins will be useful based on the type of query we are trying to perform.
- If we wanted to show each photo url and the username of the poster, a left join would accomplish this even if photos had no associated users.

### 52. Each Join in Practice

- **Show each photo url and the username of the poster**
- Left Join:
  SELECT url, username
  FROM photos
  LEFT JOIN users ON users.id = photos.user_id;
- Right Join:
  SELECT url, username
  FROM photos
  RIGHT JOIN users ON users.id = photos.user_id
- Full Join:
  SELECT url, username
  FROM photos
  FULL JOIN users ON users.id = photos.user_id

### 53. Does Order Matter?

- whatever happens to not have a relationship to the other table will show up in the source row with null for the extra columns with no association in the given source row.
- there is a difference between right and left join. Still scenarios where you want to massage the order of join whenever using an inner or outer join...especially when you're joining multiple tables together.

QUIZ 7: Test your Joining Knowledge (complete)

### 54. Exercise Overview

- complete

- Coding Exercise 10: Joins, Joins, Join! (complete)

### 55. Two Possible Solutions

-       SELECT title, name
        FROM authors
        LEFT JOIN books ON books.author_id = authors.id
-       SELECT title, name
        FROM books
        RIGHT JOIN authors ON authors.id = books.author_id

### 56. Where with Join

- **Users can comment on photos that they posted. List the url and contents for every photo/comment where this occured**
-       SELECT contents, url
        FROM comments
        JOIN photos ON photos.id = comments.photo_id
        WHERE comments.user_id = photos.user_id

### 57. Three Way Joins

-       SELECT contents, url
        FROM comments
        JOIN photos ON photos.id = comments.photo_id
        JOIN users ON photos.user_id = users.id AND users.id = comments.user_id

### 58. A Bit of Practice

SELECT title, name, rating
FROM reviews
JOIN books ON books.id = reviews.book_id
JOIN authors ON authors.id = reviews.reviewer_id AND authors.id = books.author_id

- Coding Exercise 11: Three Way Exercise (complete)

### 59. Exercise Solution

-       SELECT title, name, rating
        FROM reviews
        JOIN books ON books.id = reviews.book_id
        JOIN authors ON authors.id = reviews.reviewer_id AND authors.id = books.author_id

## Section 5: Aggregation of Records

## 46min

### [Back to Table of Contents](##table-of-contents)

### 60. Aggregrating and Grouping

-

### 60. Aggregrating and Grouping

-

QUIZ 8: Selecting Columns After Grouping

### 60. Aggregrating and Grouping

-

### 61. Picturing Group By

-

- Quiz 8: Selecting Columns After Grouping

### 62. Aggregate Functions

-

### 63. Combining Groups By and Aggregates

-

### 64. A Gotcha With Count

-

### 65. Visualizing More Grouping

-

### 66. Exercise Overview

-

- Coding Exercise 12: Practice For Grouping and Aggregating (complete)

### 67. Grouping Solution

-

### 68. Adding a Layer of Difficulty

-

- Coding Exercise 13: Grouping With a Join!

### 69. Solution

-

### 70. Filtering Groups with Having

-

### 71. Having in Action

-

### 72. More on Having!

-

### 73. A Having Exercise Overview

-

- Coding Exercise 14: Practice Yourself Some Having (complete)

### 74. A Quick Solution

-

## Section 6: Working With Large Datasets

## 20min

### [Back to Table of Contents](##table-of-contents)

### 75. A New Dataset

-

### 80. Of Course You Remember!

-

## Section 7: Sorting Records

## 13min

### [Back to Table of Contents](##table-of-contents)

### 81. The Basics of Sorting

-

### 85. Exercise Solution

-

## Section 8: Unions and Intersections with Sets

## 22min

### [Back to Table of Contents](##table-of-contents)

### 86. Handling Sets with Union

-

### 91. Exercise Solution

-

## Section 9: Assembling Queries with SubQueries

## 1hr 52min

### [Back to Table of Contents](##table-of-contents)

### 92. What's a Subquery?

-

Quiz 9: What's the Data Look Like? -

Quiz 10: Is It A VAlid Subquery? -

### 116. Exercise Solution

-

## Section 10: Selecting Distinct Records

## 5min

### [Back to Table of Contents](##table-of-contents)

### 117. Selecting Distinct Values

-

### 118. Exercise Overview

-

Coding Exercise 24: Some Practice with Distinct

### 119. A Distinct Solution

-

## Section 11: Utility Operators, Keywords, and Functions

## 10min

### [Back to Table of Contents](##table-of-contents)

### 120. The Greatest Value in a List

-

### 121. And the Least Value in a List!

-

### 122. The Case Keyword

-

## Section 12: Local PostgreSQL Installation

## 15min

### [Back to Table of Contents](##table-of-contents)

### 123. PostgreSQL Installion on MacOS

-

### 124. PGAdmin Setup on macOS

-

### 125. Postgres Installion on Windows

-

## Section 13 PostgreSQL Complex Datatypes

## 38min

### [Back to Table of Contents](##table-of-contents)

### 126. What'd We Just Do?

-

### 133. Really Awesome Intervals

-

## Section 14: Database-Side Validation and Constraints

## 49min

### [Back to Table of Contents](##table-of-contents)

### 134. Thinking About Validation

-

Quiz 11: Creating NULL Constraints

QUIZ 12: Is It Unique?

QUIZ 13: Does It Pass a Check?

### 143. So Where Are We applying Validation?

-

## Section 15: Database Structure Design Patterns

## 26min

### [Back to Table of Contents](##table-of-contents)

### 144. Approaching More Complicated Designs

-

### 148. Rebuilding Some Schema

-

## Section 16: How to Build a 'Like' System

## 35 min

### [Back to Table of Contents](##table-of-contents)

### 149. Requirements of a Like System

-

QUIZ 14: Building a Similar System -

QUIZ 15: Polymorphic Associations -

### 156. So Which Approach?

-

## Section 17: How to Build a 'Mention' System

## 27min

### [Back to Table of Contents](##table-of-contents)

### 157. Additional Features Around Posts

-

### 161. Update For Tags

-

## Section 18: How to Build a 'Hashtag' System

## 25min

### [Back to Table of Contents](##table-of-contents)

### 162. Designing a Hashtag System

- We only have to model resources in the DB if we expect to query for them at some point! So only keep tables for things you expect to query!!!
- hashtag only used for search bar primarily to query and make use of the hashtag!
- only one kind of resource... a post. comments and users do not make use of the #hashtag!!!
- search for posts that contain a hashtag are somehow modeled inside our database. because we want to eventually search for this type of hashtag to look up posts! only relationship we really care about
- Can't search for comments or users with a hashtag - implies they are not modeled! (or that we don't have to)...probably for data analysis purpose internally but not externally for users of the IG app.

### 166. Why No Number of Followers or Posts

- What about # posts, followers, following?
- increment post count value by one or subtract.
- when follow button and following just increment or decrement counter by one when button clicked.
- users table posts table followers table
- simple posts and followers query.
- Can be calculated by running a query on data that already exists in our DB
- We call this 'derived data' We genearlly dont want to store derived data unless a very good performance benefit or writing query to calculate derived data is difficult but that calculation is usually very easy.

## Section 19: How to Design a 'Follower' System

## 6min

### [Back to Table of Contents](##table-of-contents)

### 167. Designing a Follower System

- sets up relationship between one user and another. one leader, one follower essentially.
- only big rule is can only follow another user one time and cannot follow ourselves. Relationship to model this should be fairly straight forward.
- CHECK (leader_id <> follower_id)
- UNIQUE(leader_id, follower_id)
- USE DBDIAGRAM.IO/d

## Section 20 Implementing Database Design Patterns

## 44min

### [Back to Table of Contents](##table-of-contents)

### 168. Back to Postgres

- 1. Create a new db using PGAdmin
  2. Convert our design to a series of CREATE TABLE statements
  3. Insert data into the database
  4. Write some queries
  5. Realize that a few things could have been designed better! Make some changes

### 174. Creating Hashtags, Hashtag Posts, and Followers

-       CREATE TABLE hashtags_posts (
          id SERIAL PRIMARY KEY,
          hashtag_id INTEGER NOT NULL REFERENCES hastags(id) ON DELETE CASCADE,
          post_id INTEGER NOT NULL REFERENCES posts(id) ON DELETE CASCADE,
          UNIQUE(hashtag_id, post_id)
          <!-- created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
          title VARCHAR(20) NOT NULL UNIQUE -->
          );
-       CREATE TABLE followers (
          id SERIAL PRIMARY KEY,
          created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
          leader_id INTEGER NOT NULL REFERENCES users(id) ON DELETE CASCADE,
          follower_id INTEGER NOT NULL REFERENCES users(id) ON DELETE CASCADE,
          UNIQUE(leader_id, follower_id)
  )

## Section 21: Approaching and Writing Complex Queries

## 17min

### [Back to Table of Contents](##table-of-contents)

### 175. Quick Note About Adding Some Data

- DOWNLOAD FILE

### 183. Solutions for Likes per User

- Show each username and the number of 'likes' that they have created
- Join users and likes together, then group by the username. You can then 'count' the number of rows in each group
-       SELECT username, COUNT(*)
        FROM usess
        JOIN likes ON likes.user_id = user.id
        GROUP BY username

## Section 22 Understanding the Internals of PostgreSQL

## 48min

### [Back to Table of Contents](##table-of-contents)

### 184. Thinking About Performance

- Exciting! Diving into really deep stuff actually PG vs SQL.
- If you want good performance have to actually understand what PG is actually doing to really understand the performance of your database.
- how data is stored on hd and accessed. look at indexes, understand internals of indexes and how they improve data access performance, put two things together to see how queries are interpreted and accessed by the data base. extremely deep and detailed section here! very deep and low level. very long confusing boring. come back at end of course where it might make more sense!

### 185. Where does Postgres Store Data?

- we can run different queries in pgadmin to see what the identifiers are all about. internal identifiers are numbers but pgadmin can be used to discover what that database actually is.
-

### 186. Heaps, Blocks, and Tuples

- Heap or Heap File: very different from data structure terminology for a heap! File that contains all the data(rows) of our table
- Tuple or Item: Individual row from the table
- Block or Page: The heap file is divided into many different 'blocks' or 'pages'. Each page/block stores some number of rows. each block or page is 8kb large.

QUIZ 16: Terminiology Check -

### 187. Block Data Layout

-

### 188. Heap File Layout

- FREE TIME! DO NOT WATCH XD We are going to map out how PG stroes data at the binary level

## Section 23: A Look at Indexes for Performance

## 1hr 6min

### [Back to Table of Contents](##table-of-contents)

### 189. Full Table Scans

- posgres cant examine file in place while it is in a heap file. need to load it up into memory!!! then we can do filter querying of the data.
- loading hd to memory has a pretty high performance cost. minimize data going from hd to memory. will spend alot of time to limit how much is being taken from a heap file and loaded into memory.
- PG has to load many (or all) rows from the heap file to memory... Frequently (nut not always) poor performance
- We will look at a alternative to search data without performing a full table scan. We always want to investigate a more efficient way to execute/run a query without performing a full table scan.

QUIZ 17: `UNIQUE` keyword check on a specific column will create an index for that column automatically!

### 197. Behind the Scenes of Indexes

- very low level of how indexes are stored on your hd and how they are actually used by PG! FREE TIME!
-

## Section 24: Basic Query Tuning

## 19min

### [Back to Table of Contents](##table-of-contents)

### 198. The Query Processing Pipeline

- what makes a good and bad query? and when to use an index.
- a query will go through:
- 1. Parser: gonna make sure what is written in query is valid sql.
  - it will build a query tree. we can see references to all parts in the query. breaks apart entire query into logical steps that can be understood by a computer program
  2. Rewrite: Decomose views into underylying table references
  3. Planner: important what we really want to look at..
  - look at username index then get users? or fetch all users and search through them? will choose best plan to run!
  4. Execute: runs! gives a number of rows. will use this to see what makes a fast and slow query.

QUIZ 18: `EXPLAIN` shows a query plan without executing it vs `EXPLAIN ANALYZE` shows a query plan, executes it, and shows statistics about the execution

### 200. Solving an Explain Mystery

- a query node is what the arrows are.. all the rows with an arrow. top is also a query node even tho no small arrow is there.
- imagine it is trying to access our data and pass that data up, remit it to the nearest parent up.
- besides telling indiviual steps shows more numbers for the small arrow row.
- how does postgresql know how many rows and width guesses to execute steps before actually executing.. but really keeps very detailed steps....
- stats table is how that query plan can make guess about the cost or outcome of the steps without having do the processing of the steps ahead of time.

## Section 25: Advanced Query Timing

## 41min

### [Back to Table of Contents](##table-of-contents)

### 201. Developing an Intuitive Understanding of Cost

- Learn what cost is all about.
- Working definition of 'cost': amount of time (seconds? Milliseconds?) to execute some part of our query plan. _Not super accurate but good enough for now_
- how heapfiles work and indexes helpful!
- Fetch all users and search through them?
- OR Look at users username index then get users?
- for the lefthand side, fetching two random pages from the hard drive
- for the righthand side, fetching however pages are in the user heap file...!
- Performance penatly associated with randomly selecting data off hard drive!
- Loading data from random spots off a hard drive usually takes more time than loading data sequentially (one piece after another)
- Index approach fetching just a couple random pages becomes intuitively quicker then loading a hundred sequentially even if load time is slower when taking random spots off a hard drive in this case.

QUIZ 19: COST = (5*1)+ (0*4) + (100*.01) + (0*.005) + (0\*.0025) = 6 <BR>
QUIZ 19: COST = (0*1)+ (4*4) +(20*4) + (0*.01) + (75*.005) + (214*.005) + (0\*.0025) = 6

### 206. Use My Index!

- ONE MORE THING ABOUT INDEXES:
-       SELECT *
        FROM likes
        WHERE created_at < '2013-01-01';
-       EXPLAIN SELECT *
        FROM likes
        WHERE created_at < '2013-01-01';
        CREATE INDEX likes_created_at_idx ON likes (create_at); comment: create auto creates index for you but for clarity we include it.
-       SELECT COUNT(*)
        FROM likes
        WHERE created_at > '2013-01-01';
        CREATE INDEX likes_created_at_idx ON likes (create_at);
- SEQUENTIAL SCAN COMPLETED WHEN REMOVE COUNT...
- tremedous number of records fetched... when using index..visiting too many leaf nodes... opening heap files and blocks paying penaltry and postgres realizes instead of going through index it's easier if we just open heap file directly and go through sequentially!!!!
- even with index in place, postresql is smart enough to tell you performance beneift is not beneficial! get best performance out of your database with `EXPLAIN`
- YOU DONT WANT TO FORCE POSTGRESQL TO run an index since it evaluates the best option anyway.

## Section 26: Simple Common Table Expressions

## 10min

### [Back to Table of Contents](##table-of-contents)

### 207. Common Table Expression

- Show the username of users who were tagged in a caption or photo before January 7, 2010. Also show the date they were tagged
- union keyword allows us take the results of two different queries and join them together temporarily into one big set of rows. to solve easy to a union between caption and photo tags, join two sets of rows to a temporary tags table.
-

### 209. So What's a CTE?

- run a subquery to get some rows and columns and can refer to tags which is the result of what is inside the subquery.
- 1. Define with a 'with' keyword before the main query
  2. Produces a table that we can refer to anywhere else
  3. Two forms!
  4. Simple form used to make a query easier to understand
  5. Recursive form used to write queires that are otherwise imposssible to write...express with just SQL by itself! write some very powerful queries that would be impossible to express with just normal SQl
- with a simple CTE not modifying the existing query in anyway. Same steps being executed. Just easier for us to read.

## Section 27: Recursive Common Table Expressions 36min

### 210. Recursive CTE's

- very very different from simple CTE's
- Useful aytime you have a tree or graph-type data structure
- Must usa a 'union' keyword - simple CTE's don't have to use a union!
- This is super, super advanced, I don't expect you to be able to write your own recursive CTE's - just understand that they exist and if it might be good to use one in certain cases!
- `WITH RECURSIVE` countdown(val) `AS` (
  `SELECT` 3 `AS` val
  `UNION`
  `SELECT` val - 1 `FROM` countdown `WHERE` val > 1
  )
-       SELECT *
        FROM countdown

### 214. Walking Through Recursion

- STEPS:
- 1. Define the results and working tables
  2. Run the initial non-recursive statement, put the results into the results table and working table
  3. Run the recursive statement replacing the table name 'suggestions' with a reference to the working table
  4. If recursive statement returns some rows, append them to the results table and run recursion again
  5. If recursive statement returns no rows stop recursion

## Section 28: Simplifying Queries With Views

## 21min

### [Back to Table of Contents](##table-of-contents)

### 215. Most Popular Users

- `SELECT`
- `FROM`
- `JOIN` (`SELECT` user_id `FROM` photo_tags `UNION ALL` `SELECT` user_id `FROM` caption_tags) `AS` tags `ON` tags.user_id = users.id `GROUP BY` username `ORDER BY COUNT`(\*) `DESC`
- mistake in design. two separate tables whenshould of just been one....
-

### 219. Deleting and Changing Views

- change configuration of a view
- `CREATE OR REPLACE VIEW` recent\_ posts AS (`SELECT` \* `FROM` posts `ORDER BY` create_at `DESC` `LIMIT` 15);
- `SELECT` \* `FROM` recent_posts
- `DROP VIEW` recent_posts;

## Section 29: Optimizing Queries with Materialized Views

## 27min

### [Back to Table of Contents](##table-of-contents)

### 220. Materialized Views

- Variation on a view. Views, Query that gets executed every time you refer to it!
- Materialized Views: Query that gets executed only at very specific times, but the results are saved and can be referenced without rerunning the query.
- We want to do this whenever we have a very expensive query
- With Simple Common Table Expression to make it simple, convenience tools...
- Recursive Common Table Expression to add major functionality! to do somthing we plain wouldnt normally be able to do.

### 224. Creating and Refreshing Materialized Views

- take some query and write right before the query...
- `CREATE MATERIALIZED VIEW` weekly_likes `AS`(query) WITH `DATA`
- `SELECT` \* `FROM` weekly_likes; cut down on exectuon speed or results of query to handful of millisecs from 2-3 secs.
- one downside of materialized view is if we modify underlying data... not gonna modify cached results.. gonna need to update materialized view.
- `REFRESH MATERIALIZED VIEW` weekly_likes;
- `DELETE FROM` posts `WHERE` created_at < 'date';
- in general you want to use a materialized view when the results of the query change only once a day week month etc. not when you have to rerun the query and change results frequently....

## Section 30: Handling Concurrency and Reversibility with Transactions

## 22min

### [Back to Table of Contents](##table-of-contents)

### 225. What are Transactions Used For?

- example for transactions is very effective.
- new table in our instagram database just to understanding what they are all about, how to use them, what they're for.
- Transfer 50 from one account to another.
- 1 step `update` accounts table `set` balance to subtract 50 `where` name is one account
- same thing except add 50 ot other account
- could run into crash issue so 50 is never added for half executed step... no accounting whatsoever to add to another account or main account doesn't have 50 anymore either.
- Use transaction to run updates in series so all are executed or none are. rollback all changes made if not everything is executed.

### 229. Closing Aborted Transactions

- `BEGIN`
- `SELECT` \* `FROM` accounts;
- ERROR: current transaction is aborted, commands ignored until end of trancation block
- require `ROLLBACK`
- everything work as expected!!!!

## Section 31: Managing Database Design with Schema

## 51min

### [Back to Table of Contents](##table-of-contents)

### 230. A Story on Migrations

- Schema Migrations are exceptionally important when you start working with other engineers.
- Making very careful and well planned changes to the structure of your database. adding removing changing name of column to a table. add remove table so on.
- Busy day managing the database at instagram
- need to make some changes to the database.
- big issues will happen if you make changes directly to the database.
- in charge of the comments table.
- 2 copies of postrges hosted on your machine and one hosted on AWS.
- development environment is on your computer, then you make changes to the production database hosted on AWS.
- `ALTER TABLE` comments
- `RENAME COLUMN` contents `TO` body;
- connecting to production database using pgAdmin will get you into trouble quickly.
- you didn't make changes to API Server... still refererencing contents instead of boy. invalid SQL statement..... not good.

1. Big Lesson #1: Anytime changes to the DB strucure and changes to clients need to be made at precisely the same time.

- All clients such as API need to be changed at the same time.
- Make change to the new deployment of your API.
- Usually changes will be made to the database deploying new changes to application code when an announcement is made about "downtime" for an application.
- How to minimize scheduled downtime important
- one engineer dedicated to maintaining the database and one engineer dedicated to deployment.

2. Now in charge of the entire series of actions for making the mistake. the comments table plus related changes to the API accessing the DB.

- Now you will make these changes locally, test them and confirm everything works. Time for a review so you can actually deploy this stuff!
- You create a request for a code review on GitHub, etc.- It contains all the changed code for the API.

3. Big lesson #2: When working with other engineers, we need a really easy way to tie the structure of our database to our code.

4. Schema Migrations can solve these two big issues!

### 238. Generating and Applying a Second Migration

- Change the structure of your database! change datatype of your column? hmm. Can use this migration process for zero downtime change? change structue of our database without any downtime or server issues?

## Section 32: Schema vs Data Migrations

## 4min

### [Back to Table of Contents](##table-of-contents)

### 239. Schema vs Data Migrations

- We've written 2 migrations. Need to write one more
- column with a data type of point stores two values (x,y) which can store the values of lat and lng
- Write 4th migration with two rows combined into one.
- Might merge columns into a single location column actually.
- add column loc, copy lat/lng to loc, drop columns lat/lng
- looks easy but harder.
- schema migration: add remove columns, changing strucure of data base
- data migration: moving data around, moving values between different columns... very controversial topic in database community.....!!!

### 251. Dropping the Last Columns

- `ALTER TABLE` <table>
- `DROP COLUMN` lat numeric lng numeric

## Section 33: Accessing PostgreSQL from API's

## 28min

### [Back to Table of Contents](##table-of-contents)

### 252. Section Goal

- Interact from a Node API. Interact with a database from a real application!!!!
-

### 258. Query and Close

- The goal of close, is to close out the pool.

## Section 34: Data Access Pattern - Repositories

## 32min

### [Back to Table of Contents](##table-of-contents)

### 259. The Repository Pattern

- User Repository can have as many functions tied to it as we want to interact with the user table!
- function: find, findById, insert, update, delete
- goal: return, find, add, update, delete

1. Just remember, one central point for accessing a type of resource inside the database.
2. Can be implemented as an object with plain functions, as an instance of a class, as a class with static methods, anything!!!!...

### 264. Finding particular Users

-

## Section 35: Security Around PostgreSQL

## 38min

### [Back to Table of Contents](##table-of-contents)

### 265. SQL Injection Exploits

- We will modify request just a little bit.
- i.e. `http://localhost:3005/users/1;DROP TABLE users;`
- creates a drastic change to our database.
- any arbitrary user could modify the url and destroy the database...
-

### 271. And, Finally, Delete

-

## Section 36: Fast Parallel Testing

## 1hr 27min

### [Back to Table of Contents](##table-of-contents)

### 272. A Note on Testing

- Really to learn about two additional PostgreSQL features
- Jest Test Runner
- Program that will execute 3 test files at the same time
- usually ran sequentially
- jest runs tests in parallel to save a little time.
- big challenge: all tests connecting to social networking database at the same time.
- create a user get most recently created user see if it has attributes, if another user is created however...
- some test may fail erroneously... so will need to learn additional PostgreSQL features

### 288. Finally... Parallel Tests!

- all tests running seperately in their own schemas and then cleaned up afterwards.
- after every indiviual test might want to delete all data in that database (i.e. drop all records in a table) to operate on a clean fresh slate
- slightly faster approach: add in another method reset()
- will delete from users. maybe posts comments images etc.
- add beforeEach() with context.reset()
- run as many test files in parralel and isolation. one test does not interfere another. and tests run really quick. great setup.

## Section 37: Bonus!

## 1min

### [Back to Table of Contents](##table-of-contents)

### 289. Bonus!

- Microservises with NodeJS and React looks great.
- what is infrastructure deployment?
