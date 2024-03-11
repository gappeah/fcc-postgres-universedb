#Universe Database

##This is a PostgreSQL database schema dump for a universe simulation. It includes tables for:

    Black Holes
    Galaxies
    Moons
    Planets
    Stars

##Tables

    blackhole
        blackhole_id (integer, primary key)
        gravity (integer)
        galaxy_id (integer, foreign key referencing galaxy.galaxy_id)
        wormhole (boolean)
        name (text, unique)
    galaxy
        galaxy_id (integer, primary key)
        speed (integer)
        description (text)
        name (text, unique)
        rotation_speed (integer)
    moon
        moon_id (integer, primary key)
        name (text, not null)
        has_water (boolean, not null)
        planet_id (integer, foreign key referencing planet.planet_id)
        name_code (text, unique)
    planet
        planet_id (integer, primary key)
        name (text, unique)
        amount_of_people (numeric)
        time_travel (boolean)
        star_id (integer, foreign key referencing star.star_id)
    star
        star_id (integer, primary key)
        radius (integer)
        color (text)
        name (text, unique)
        galaxy_id (integer, foreign key referencing galaxy.galaxy_id)

##Relationships

    Stars can belong to Galaxies (one-to-many)
    Planets can belong to Stars (one-to-many)
    Moons can belong to Planets (one-to-many)

##Additional Notes

    This schema dump includes data for all the tables.
    Some tables have unique constraints on specific columns.

This information can be helpful for anyone who wants to understand the structure of the universe database or who wants to write queries to interact with the data.
