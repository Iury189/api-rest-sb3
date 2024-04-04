# API REST application

```
api-rest-sb3
|__ src
    |__ main
    |    |__ java
    |        |__ com.sb3.apirestsb3
    |            |__ DAO
    |            |   |__ CharacterDAO.java
    |            |
    |            |__ Model
    |            |   |__ CharacterModel.java
    |            |
    |            |__ REST
    |            |   |__ CharacterREST.java
    |            |
    |            |__ Service
    |                |__ CharacterService.java
    |__ resources
        |__ application.properties
```

### Application Structure

* ```CharacterModel.java```: Work with informations of database.
* ```CharacterDAO.java```: Interface containing methods for data management.
* ```CharacterService.java```: implementing methods defined in the interface.
* ```CharacterREST.java```: HTTP CRUD (Create, Read, Update, Delete) methods to enable client-server communication.
* ```application.properties```: Application settings file.

## Database

You can use ```PostgreSQL``` or ```MySQL```, so follow the steps:

1 - Go to ```application.properties``` and insert the lines
```
# PostgreSQL
spring.datasource.url=jdbc:postgresql://localhost:5432/database-name
spring.datasource.username=postgres
spring.datasource.password=
spring.datasource.driver-class-name=org.postgresql.Driver

# MySQL
spring.datasource.mysql.url=jdbc:mysql://localhost:3306/database-name
spring.datasource.mysql.username=root
spring.datasource.mysql.password=
spring.datasource.mysql.driver-class-name=com.mysql.cj.jdbc.Driver
```

2 - Create a database with the name that you desire (it needs be the same configured in ```application.properties```)

3 - Create a table called ```characters``` (the table name is configured in ```CharacterModel.java```), then insert this code snippet to speed up the process.

```
-- PostgreSQL
CREATE TABLE characters (
    id SERIAL PRIMARY KEY,
    name VARCHAR(50) NOT NULL,
    race VARCHAR(15) NOT NULL,
    gender VARCHAR(15) NOT NULL,
    type_class VARCHAR(15) NOT NULL,
    age INT NOT NULL,
    height DECIMAL(3,2) NOT NULL,
    element VARCHAR(15) NOT NULL,
    origin VARCHAR(15) NOT NULL,
    weapon VARCHAR(15) NOT NULL,
    alignment VARCHAR(15) NOT NULL,
    alive BOOLEAN NOT NULL
);

-- MySQL
CREATE TABLE characters (
    id PRIMARY KEY NOT NULL AUTO_INCREMENT,
    name VARCHAR(50) NOT NULL,
    race VARCHAR(15) NOT NULL,
    gender VARCHAR(15) NOT NULL,
    type_class VARCHAR(15) NOT NULL,
    age INT NOT NULL,
    height DECIMAL(3,2) NOT NULL,
    element VARCHAR(15) NOT NULL,
    origin VARCHAR(15) NOT NULL,
    weapon VARCHAR(15) NOT NULL,
    alignment VARCHAR(15) NOT NULL,
    alive BOOLEAN NOT NULL
);

-- Insert lines
INSERT INTO characters (name, race, gender, type_class, age, height, element, origin, weapon, alignment, alive) 
VALUES
('Mardek Innanu El-Enkidu', 'Human', 'Male', 'Recruit', 18, 1.78, 'Light', 'Goznor', 'Sword', 'Lawful Good', true),
('Deugan Selmae Eh-Deredu', 'Human', 'Male', 'Recruit', 18, 1.77, 'Earth', 'Goznor', 'Greatsword', 'Neutral Good', true),
('Emela Andra Wu-Jardu', 'Human', 'Female', 'Elemance', 18, 1.75, 'Water', 'Water Temple', 'Rod', 'Lawful Neutral', true),
('Vehrn Juonour El-Ganobyi', 'Human', 'Male', 'Paladin', 25, 1.77, 'Light', 'Belfan', 'Sword', 'Lawful Good', true);
```

## API REST Address 

Go for some API Client tool to perform the API testing, use [POSTMAN](https://www.postman.com/) for example.

**GET: localhost:8080/api/character**
```
// Response
[
  {
    "id": 1,
    "name": "Mardek Innanu El-Enkidu",
    "race": "Human",
    "gender": "Male",
    "type_class": "Recruit",
    "age": 18,
    "height": 1.78,
    "element": "Light",
    "origin": "Goznor",
    "weapon": "Sword",
    "alignment": "Lawful Good",
    "alive": true
  },
  {
    "id": 2,
    "name": "Deugan Selmae Eh-Deredu",
    "race": "Human",
    "gender": "Male",
    "type_class": "Recruit",
    "age": 18,
    "height": 1.77,
    "element": "Earth",
    "origin": "Goznor",
    "weapon": "Greatsword",
    "alignment": "Neutral Good",
    "alive": true
  },
  {
    "id": 3,
    "name": "Emela Andra Wu-Jardu",
    "race": "Human",
    "gender": "Female",
    "type_class": "Elemance",
    "age": 18,
    "height": 1.75,
    "element": "Water",
    "origin": "Water Temple",
    "weapon": "Rod",
    "alignment": "Lawful Neutral",
    "alive": true
  },
  {
    "id": 4,
    "name": "Vehrn Juonour El-Ganobyi",
    "race": "Human",
    "gender": "Male",
    "type_class": "Paladin",
    "age": 25,
    "height": 1.77,
    "element": "Light",
    "origin": "Belfan",
    "weapon": "Sword",
    "alignment": "Lawful Good",
    "alive": true
  }
]
```

**POST: localhost:8080/api/character**
```
// JSON Content
{
  "name": "Elwyen Sirene Wu-Nympha",
  "race": "Human",
  "gender": "Female",
  "type_class": "Youngling",
  "age": 14,
  "height": 1.61,
  "element": "Water",
  "origin": "Canonia",
  "weapon": "Harp",
  "alignment": "Chaotic Neutral",
  "alive": true
}

// Response
{
  "id": 5,
  "name": "Elwyen Sirene Wu-Nympha",
  "race": "Human",
  "gender": "Female",
  "type_class": "Youngling",
  "age": 14,
  "height": 1.61,
  "element": "Water",
  "origin": "Canonia",
  "weapon": "Harp",
  "alignment": "Chaotic Neutral",
  "alive": true
}
```

**GET: localhost:8080/api/character/id**
```
// Response
{
  "id": 5,
  "name": "Elwyen Sirene Wu-Nympha",
  "race": "Human",
  "gender": "Female",
  "type_class": "Youngling",
  "age": 14,
  "height": 1.61,
  "element": "Water",
  "origin": "Canonia",
  "weapon": "Harp",
  "alignment": "Chaotic Neutral",
  "alive": true
}
```

**GET: localhost:8080/api/character/search?name=El-Enkidu**
```
// Response
[
  {
    "id": 1,
    "name": "Mardek Innanu El-Enkidu",
    "race": "Human",
    "gender": "Male",
    "type_class": "Recruit",
    "age": 18,
    "height": 1.78,
    "element": "Light",
    "origin": "Goznor",
    "weapon": "Sword",
    "alignment": "Lawful Good",
    "alive": true
  }
]
```

**PUT: localhost:8080/api/character/id**
```
// JSON Content
{
  "name": "Elwyen Sirene Wu-Nympha",
  "race": "Human",
  "gender": "Female",
  "type_class": "Youngling",
  "age": 14,
  "height": 1.65, // I changed here
  "element": "Water",
  "origin": "Canonia",
  "weapon": "Harp",
  "alignment": "Chaotic Neutral",
  "alive": true
}

// Response
{
  "id": 5,
  "name": "Elwyen Sirene Wu-Nympha",
  "race": "Human",
  "gender": "Female",
  "type_class": "Youngling",
  "age": 14,
  "height": 1.65,
  "element": "Water",
  "origin": "Canonia",
  "weapon": "Harp",
  "alignment": "Chaotic Neutral",
  "alive": true
}
```

**DELETE: localhost:8080/api/character/id**
```
// Response
Elwyen Sirene Wu-Nympha was deleted successfully.
```
### Reference
- **[Mardek](https://figverse.fandom.com/wiki/MARDEK_(Series))**
