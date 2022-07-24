# Class 4 Notes

## Overview

1. Databases
2. Sequelize & ORM
3. Local DB & SQlite
4. Production DB & Postgres
5. Validation & constraints
6. Association (nee Relationships)
7. Collections

## Domain Modeling

- Data modeling: the pieces of a program specific to business requirements.
- Entities - persisted data (the things that we keep and store). Describe by our models.
  - primitive data store at one time.
- Properties - primitive data types
  - atomic, and only have meaning within an entity
  - Strings, numbers, dates, IPAdress or CIDR
- Association or relationship connected to an entity
  - distinct things in their own right
- All in service of some business requirement

## Constraints & Validation

- We used validation (middleware) in lab02 to check the query string was valid.
- Validation: checking that entities are valid
  - needs to be done before we do calculations
  - middleware is an excellent place to validate.
  - can be done in express middle to protect the server or in sequelize, to protect the database.
- Apply to a single entity
- Constraints: check that all entities are valid with one another.
  - EG id must be unique
  - Name cannot be null
  - protect the database from the data
- In sequelize: provide when defining fields

## Associations

- Used to connect our entities
  - One to One
  - One to Many
  - Many to Many

- one airplane has many plane tickets
- one plane ticket has only one passenger
- One passenger has many plane tickets

How do I know which flight the plane ticket is for?
  - Plane ticket has the flight id as a property

<!-- Flight: (id, plane, ([list of tickets)]); -->
Flight: (id, origin, destination);
Ticket: (flight_id, passenger_id, seat_assignment);
Passenger: (passenger_id, passport_number, name);

In sequelize:
  - ModelA.BelongsTo(ModelB) creates the reference column
    - And the Foreign Key

When querying:
  - Eager vs lazy
  - 


```
const sequelize = require('sequelize)

const Flight = (db) => {
    db.define("flight", {
    origin: sequelize.DataTypes.STRINGS,
    destination: sequelize.DataTypes.STRING,
  });

const Passenger = (db) => {
    db.define("Passenger", {
    name: sequelize.DataTypes.STRING,
    passport_number: sequelize.DataTypes.NUMBER,
  }):

const Ticket = (db) => {
  db.define("Ticket", {
    seat_assignment: sequelize.DataTypes.STRING,
  });

  Ticket.belongsTo(Flight);
  Ticket.belongsTo(Passenger);

  Flight.hasMany(Ticket);
  Passenger.hasOne(Ticket);

  return { Flight, Passenger, Ticket};
};

// Lazy evaluation

const { Flight, Ticket } = MakeModels({});
sync function doStuff(){
  const flights = await Flight.findOne({where: {flightId: '1213'}})
  // Second DB query
  const tickets = await Flight.getTickets();
}

// Eager evaluation - larger request on DB

async function doStuffEager() {
  const flight = await Flight.findOne({
    where" { flightId: '121212'},
    include: Ticket,
  });

  const tickets = flight.tickets;
}

```

- Creates all routes for a model: given a model, create all the routes for it.
  - function Collection(model){
    return {
      '/route-1',
      '/route-2',
    };
    addRoutes(app){
      app.get('...', () => {...})
    }
  }

  - function routeModel(model, app){
    app.get();
    app.delete();
    //..
  };

  - routeModel(Tickets, app);
  - routeModel(Flight, app);
 