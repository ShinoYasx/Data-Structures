# TP 1

## Exercice 1

> Un garagiste souhaiterait mieux gérer son parc de voitures et sa clientèle. Jusqu'à maintenant, il notait tout dans de gros registres mais bien souvent il ne s'y retrouve plus. Il voudrait avoir un programme informatique pour gérer tout cela.  Ce programme doit permettre d'obtenir les **informations** d'un **client** particulier pour pouvoir le facturer. Il doit aussi permettre d'avoir un **état des lieux des voitures présentes**  au  garage,  leur  **marque**,  **modèle**  et  **immatriculation**,  ainsi  que  leur  **propriétaire**.  Le programme doit aussi permettre de **modifier** les **informations d'un client** particulier et de ressortir la **liste des voitures réparées**.

```plantuml
@startuml
class Client {
    + Client()
    .. Getters ..
    + getPhoneNumber() : String
    + getName() : String
    + getAddress() : String
    .. Setters ..
    + setName(name : String)
    + setAddress(address : String)
    + setPhoneNumber(phone_number : String)
    __
    - m_name : String
    - m_address : String
    - m_phone_number : String
}

enum Status {
    Pending
    Repaired
    Paid
}

class Car {
    + Car()
    .. Getters ..
    + getBrand() : String
    + getModel() : String
    + getMatriculation() : String
    + getOwner() : Client
    + getStatus() : Status
    + getStatusString() : String
    .. Setters ..
    + setBrand(brand : String)
    + setModel(model : String)
    + setMatriculation(matriculation : String)
    + setOwner(owner : Client)
    + setStatus(status : Status)
    __
    - m_brand : String
    - m_model : String
    - m_matriculation : String
    - m_owner : Client
    - m_status : Status
}

class Garage {
    + Garage()
    + ~Garage()
    ..
    + listCar() : Integer
    + listClient() : Integer
    + {static} carStatusEditMenu(car : Car) : Integer
    + carEditMenu(car : Car) : Integer
    + carSelectMenu() : Car
    + {static} clientEditMenu(client : Client) : Integer
    + clientSelectMenu() : Client
    + mainMenu() : Integer
    __
    - clients : ArrayList<Client>
    - cars : ArrayList<Car>
}

Car *-- Client
Car *-- Status
Garage *-- Client
Garage *-- Car

@enduml
```

### Compilation

Pour compiler le projet:

```shell
gcc -o TP1_HALDI_Hugo TP1.c Exercise1.c
```

## Exercice 2

```plantuml
@startuml
enum Type {
    JET
    TURBOPROP
    PISTON_ENGINE
}

enum Use {
    PUBLIC
    MILITARY
}

enum Rank {
    PILOT
    COPILOT
    PURSES
    STEWARD
}

class Compagny {
    + Compagny(name : String,\n staff : ArrayList<Employee>,\n flights : ArrayList<Flight>,\n airports : ArrayList<Airport>)
    ..
    + addFlight(flight : Flight)
    + addEmployee(employee : Employee)
    + addAirport(airport : Airport)
    + addAircraft(aircraft : Aircraft)
    .. Getters ..
    + getName() : String
    + getStaff() : ArrayList<Employee>
    + getFlights() : ArrayList<Flight>
    + getAirports() : ArrayList<Airport>
    + getAircrafts() : ArrayList<Aircraft>
    .. Setters ..
    + setName(name : String)
    __
    - name : String
    - staff : ArrayList<Employee>
    - flights : ArrayList<Flight>
    - airports : ArrayList<Airport>
    - aircrafts : ArrayList<Aircraft>
}

class Aircraft {
    + Aircraft(manufacturer : String,\n matriculation : String,\n model : String,\n type : Type,\n capacity : Integer,\n ladenWeight : Float,\n width : Float,\n length : Float,\n averageSpeed : Float)
    .. Getters ..
    + getManufacturer() : String
    + getMatruculation() : String
    + getModel() : String
    + getType() : Type
    + getCapacity() : Integer
    + getLadenWeight() : Float
    + getWidth() : Float
    + getLength() : Float
    + getAverageSpeed() : Float
    __
    - m_manufacturer : String
    - m_matriculation : String
    - m_model : String
    - m_type : Type
    - m_capacity : Integer
    - m_ladenWeight : Float
    - m_width : Float
    - m_length : Float
    - m_averageSpeed : Float
}

class Employee {
    + Employee(name : String,\n rank : Rank, id : Integer)
    .. Getters ..
    + getRank() : Rank
    + getName() : String
    + getId() : Integer
    .. Setters ..
    + setRank(rank : Rank)
    + setName(name : String)
    __
    - id : Integer
    - m_name : String
    - m_rank : CrewRank
}

class Coordinate {
    + Coordinate(x : Float, y : Float)
    + {static} distance(a : Coordinate, b : Coordinate) : Float
    __
    - m_x : Float
    - m_y : Float
}

class Airport {
    + Airport(icaoCode : String,\n country : String,\n coordinates : Coordinate,\n evelation : Integer,\n use : Use)
    __
    - m_icaoCode : String
    - m_country : String
    - m_coordinates : Coordinate
    - m_elevation : Integer
    - m_use : AirportUse
}

class Flight {
    + Flight(flightNumber : Integer,\n aircraft : Aircraft,\n crew : ArrayList<Employee>,\n departureTime : Long,\n departureAirport : Airport,\n arrivalAirport : Airport)
    .. Getters ..
    + getFlightNumber() : Integer
    + getAircrafts() : Aircraft
    + getCrew() : ArrayList<Employee>
    + getDepartureTime() : Long
    + getArrivalAirport() : Airport
    + getTravelTime() : Long
    + getArrivalTime() : Long
    .. Setters ..
    + setFlightNumber(flightNumber : Integer)
    + setAircraft(aircraft : Aircraft)
    + setCrew(crew : ArrayList<Employee>)
    + setDepartureTime(time : Long)
    + setArrivalAirport(airport : Airport)
    __
    - m_flightNumber : Integer
    - m_aircraft : Aircraft
    - m_crew : ArrayList<Employee>
    - m_departureTime : Long
    - m_departureAirport : Airport
    - m_arrivalAirport : Airport
}

Compagny *-- Airport
Compagny *-- Aircraft
Compagny *-- Employee
Compagny *-- Flight

Aircraft *-- Type

Employee *-- Rank

Airport *-- Use
Airport *-- Coordinate

Flight *-- Aircraft
Flight *-- Airport
Flight *-- Employee
@enduml
```

```plantuml
@startuml
object Geneva {
    m_icaoCode = LSGG
    m_country = "CHE"
    m_coordinates = {x: 46.2380972, y: 6.10894999}
    m_elevation = 1411
    m_use = Public
}
object London {
    m_icaoCode = EGLL
    m_country = "GBR"
    m_coordinates = {x: 51.4775, y: -0.461389}
    m_elevation = 83
    m_use = Public
}
object Boeing {
    m_manufacturer = "Boeing"
    m_matriculation = "757-2G4"
    m_model = "VC-32A"
    ...
}
object Crew {
    ArrayList<Employee>
}
object "Departure Time" as DepartureTime {
    UNIX time
}
object "Flight Number" as FlightNumber {
    Given by aviation authorities
}
Object Flight {
    m_flightNumber = 6341
    m_aircraft = Boeing
    m_crew = Crew
    m_departureAirport = Geneva
    m_arrivalAirport = London
}
Flight *-- Geneva
Flight *-- London
Flight *-- Boeing
Flight *-- Crew
Flight *-- DepartureTime
Flight *-- FlightNumber

@enduml
```

### Compilation

L'implémentation de cet exercice n'étant qu'une bibliothèque, on ne peut que créer un fichier objet:

```shell
gcc -c -fPIC Exercise2.c -o Exercise2.o
```
