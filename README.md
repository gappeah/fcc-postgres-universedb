# Universe Database

This FreeCodeCamp project uses a PostgreSQL database called **Universe**, designed to model a simplified version of a cosmic system, including galaxies, stars, planets, moons, and black holes. The database schema consists of several tables, each representing a different celestial entity, and includes relationships between these entities. The project uses PostgreSQL 12.9, and this README provides an overview of the database structure, the entities involved, and instructions on how to set up and use the database.


## Database Schema
![diagram-export-02-09-2024-15_30_02](https://github.com/user-attachments/assets/386c23b3-0853-4f73-aed7-685289253f12)

The **Universe** database consists of the following tables:

### 1. **Galaxy**
   - **Columns:**
     - `galaxy_id` (Primary Key, `integer`): Unique identifier for each galaxy.
     - `speed` (`integer`): The speed of the galaxy (can be left NULL).
     - `description` (`text`): A description of the galaxy.
     - `name` (`varchar(255)`, Unique): The name of the galaxy.
     - `rotation_speed` (`integer`, Default: 100,000): The rotation speed of the galaxy.

### 2. **Star**
   - **Columns:**
     - `star_id` (Primary Key, `integer`): Unique identifier for each star.
     - `radius` (`integer`): The radius of the star.
     - `color` (`varchar(255)`): The color of the star.
     - `name` (`varchar(255)`, Unique): The name of the star.
     - `galaxy_id` (`integer`, Foreign Key): References the galaxy that the star belongs to.

### 3. **Planet**
   - **Columns:**
     - `planet_id` (Primary Key, `integer`): Unique identifier for each planet.
     - `name` (`varchar(255)`, Unique): The name of the planet.
     - `amount_of_people` (`numeric`): The number of people living on the planet (can be left NULL).
     - `time_travel` (`boolean`, Default: false): Indicates whether time travel is possible on this planet.
     - `star_id` (`integer`, Foreign Key): References the star that the planet orbits.

### 4. **Moon**
   - **Columns:**
     - `moon_id` (Primary Key, `integer`): Unique identifier for each moon.
     - `name` (`varchar(255)`): The name of the moon.
     - `has_water` (`boolean`): Indicates whether the moon has water.
     - `planet_id` (`integer`, Foreign Key): References the planet that the moon orbits.
     - `name_code` (`varchar(255)`, Unique): A unique code representing the name of the moon.

### 5. **Blackhole**
   - **Columns:**
     - `blackhole_id` (Primary Key, `integer`): Unique identifier for each black hole.
     - `gravity` (`integer`): The gravitational force of the black hole (can be left NULL).
     - `galaxy_id` (`integer`): References the galaxy where the black hole is located (can be left NULL).
     - `wormhole` (`boolean`, Default: false): Indicates whether the black hole is also a wormhole.
     - `name` (`varchar(255)`, Unique): The name of the black hole.

## Constraints and Relationships

- **Primary Keys**: All entities have a primary key to ensure each record is unique.
- **Unique Constraints**: The `name` column in the `Galaxy`, `Star`, `Planet`, and `Blackhole` tables, and the `name_code` column in the `Moon` table, are unique to avoid duplicate entries.
- **Foreign Keys**: 
  - `Star` references `Galaxy` via `galaxy_id`.
  - `Planet` references `Star` via `star_id`.
  - `Moon` references `Planet` via `planet_id`.
  - `Blackhole` references `Galaxy` via `galaxy_id` (nullable).

## Data Initialization

The database contains initial data for testing and demonstration purposes. Below are the number of records initialized:

- **Galaxies**: 6 records.
- **Stars**: 6 records.
- **Planets**: 13 records.
- **Moons**: 20 records.
- **Blackholes**: 3 records.

## Setup Instructions

To set up the Universe database on your PostgreSQL server:

1. **Install PostgreSQL**: Ensure you have PostgreSQL 12.9 installed on your system.
2. **Create Database**: Execute the `CREATE DATABASE` command to create the `universe` database.
3. **Execute SQL Dump**: Run the provided SQL dump file to set up the schema and insert the initial data.
   ```bash
   psql -U [username] -d universe -f universe_dump.sql
   ```
4. **Connect to Database**: Connect to the `universe` database to start exploring the data.
   ```bash
   psql -U [username] -d universe
   ```

## Usage

Once the database is set up, you can perform SQL queries to explore and analyze the data. Here are a few example queries:

- **Get all planets in a specific galaxy**:
   ```sql
   SELECT p.name FROM planet p
   JOIN star s ON p.star_id = s.star_id
   JOIN galaxy g ON s.galaxy_id = g.galaxy_id
   WHERE g.name = 'andromeda';
   ```

- **Find moons with water on a specific planet**:
   ```sql
   SELECT m.name FROM moon m
   JOIN planet p ON m.planet_id = p.planet_id
   WHERE p.name = 'earth' AND m.has_water = true;
   ```

- **List all black holes that are also wormholes**:
   ```sql
   SELECT name FROM blackhole WHERE wormhole = true;
   ```

## License

This project is open-source and licensed under the MIT License. Feel free to use, modify, and distribute this code as per the terms of the license.


