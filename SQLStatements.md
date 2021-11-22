## Create Table Statements

### DROP Code
The drop code below was run at the beginning before creating the tables

``` sql
PRAGMA foreign_keys = OFF;

DROP TABLE IF EXISTS Offers;
DROP TABLE IF EXISTS Viewing;
DROP TABLE IF EXISTS Property;
DROP TABLE IF EXISTS Vendor;
DROP TABLE IF EXISTS Client;
DROP TABLE IF EXISTS EstateAgents;
DROP TABLE IF EXISTS NNStaff;

PRAGMA foreign_keys = ON;
```


### CREATE Code
The tables were created in the order shown above: NNStaff, EstateAgents, Client, Vendor, Property, Viewing and Offers.

```sql
CREATE TABLE NNStaff (
    NNStaffNo	INTEGER PRIMARY KEY AUTOINCREMENT,
    FirstName	VARCHAR(255),
    LastName	VARCHAR(255),
    YearsExperience INT(3),
    Salary 	DECIMAL(9,2),
    NI 		CHAR(9) NOT NULL,
    PhoneNumber	CHAR(11),
    Email	VARCHAR(75)
);


CREATE TABLE EstateAgents (
    AgentId	INTEGER PRIMARY KEY AUTOINCREMENT,
    Name	VARCHAR(255),
    AddressLine1	VARCHAR(255),
    AddressLine2	VARCHAR(255),
    Town	VARCHAR(255),
    County	VARCHAR(255),
    Postcode	CHAR(8) NOT NULL,
    PhoneNumber	CHAR(11),
    EmailAddress	VARCHAR(75)
);

CREATE TABLE Client (
    ClientId	INTEGER PRIMARY KEY AUTOINCREMENT,
    Title	VARCHAR(5),
    FirstName	VARCHAR(255),
    LastName	VARCHAR(255),
    AddressLine1	VARCHAR(255),
    AddressLine2	VARCHAR(255),
    Town	VARCHAR(255),
    County	VARCHAR(255),
    Postcode	CHAR(8) NOT NULL,
    PhoneNumber	CHAR(11),
    EmailAddress	VARCHAR(75)
);

CREATE TABLE Vendor (
    VendorId	INTEGER PRIMARY KEY AUTOINCREMENT,
    Title	VARCHAR(5),
    FirstName	VARCHAR(255),
    LastName	VARCHAR(255),
    AddressLine1	VARCHAR(255),
    AddressLine2	VARCHAR(255),
    Town	VARCHAR(255),
    County	VARCHAR(255),
    Postcode	CHAR(8) NOT NULL,
    PhoneNumber	CHAR(11),
    EmailAddress	VARCHAR(75),
    OwnershipType	VARCHAR(10)
);

CREATE TABLE Property (
    PropertyId	INTEGER PRIMARY KEY AUTOINCREMENT,
    AddressLine1	VARCHAR(255),
    AddressLine2	VARCHAR(255),
    Town	VARCHAR(255),
    County	VARCHAR(255),
    Postcode	CHAR(8) NOT NULL,
    BuildDate	DATE,
    ListedDate	DATE,
    SoldDate	DATE,
    PropertyValue	DECIMAL(10,2),
    PropertyType	VARCHAR(20),
    PropertyStatus	VARCHAR(25),
    AgentId 	INT(4),
    VendorId	INT(10),
    FOREIGN KEY (AgentId) REFERENCES EstateAgents(AgentId),
    FOREIGN KEY (VendorId) REFERENCES Vendor(VendorId)
);

CREATE TABLE Viewing (
    ViewingId	INTEGER PRIMARY KEY AUTOINCREMENT,
    ViewingDate	DATE,
    ViewingTime	TIME,
    Outcome	VARCHAR(10),
    ClientId 	INT(10),
    PropertyId	INT(10),
    NNStaffNo	INT(10),
    FOREIGN KEY (ClientId) REFERENCES Client(ClientId),
    FOREIGN KEY (PropertyId) REFERENCES Property(PropertyId),
    FOREIGN KEY (NNStaffNo) REFERENCES NNStaff(NNStaffNo)
);

CREATE TABLE Offers (
    OffersId	INTEGER PRIMARY KEY AUTOINCREMENT,
    OfferStage	VARCHAR(10),
    OfferStatus	VARCHAR(10),
    OfferValue 	DECIMAL(10,2),
    ClientId	INT(10),
    PropertyId	INT(10),
    FOREIGN KEY (ClientId) REFERENCES Client(ClientId),
    FOREIGN KEY (PropertyId) REFERENCES Property(PropertyId)
);
```

### Insert SQL Values
Each table was then populated in the same order as they were created. 
A SELECT * query was run following the insert statements to show the data for each table.

```sql
--Insert statements
--NNStaff
INSERT INTO NNStaff(FirstName, LastName, YearsExperience, Salary, NI, PhoneNumber,Email)
VALUES ('Ingrim','Marquand',6,36845.75,948935738,0803344570,'imarquand0@nn.co.uk'),
	('Cornie','Loiterton',3,33340.57,0863218105,916486204,'cloiterton1@nn.co.uk'),
	('Ricki','Elderkin',14,62141.09,7507675157,452930202,'relderkin2@nn.co.uk'),
	('Erhart','Kilrow',10,59931.88,8445350412,392152138,'ekilrow3@nn.co.uk'),
	('Tawnya','Creek',3,50636.04,2598364791,528541390,'tcreek4@nn.co.uk');

SELECT * from NNStaff;

--EstateAgent
INSERT INTO EstateAgents(Name, AddressLine1, AddressLine2, Town, County, Postcode, PhoneNumber,EmailAddress)
VALUES ('Reeds Rains',	'4 High Street', 'Boston',	'Manchester', 'Greater Manchester',	'M3 5RR',	01615454555,	'contact@reedsrains.co.uk'),
	('Entwistle Green',	'33 Main Street',	'Parbold',	'Manchester', 'Greater Manchester',	'M23 4PW',	01618889999, 'contact@entwistlegreen.co.uk'),
	('Regan And Halworth',	'55 Market Street',	'Standish',	'Manchester', 'Greater Manchester', 'M55 7QQ',	01617774444,	'contact@reganhalworth.co.uk'),
	('Yopa',	'11 Moss Road',	'Shevington',	'Manchester',	'Greater Manchester','M11 7HH',	01612223333,	'contact@yopa.co.uk'),
	('Strike',	'5 Main Street',	'Bispham',	'Manchester',	'Greater Manchester', 'M23 4PW',	01619995555,	'contact@strike.co.uk');

SELECT * from EstateAgents;

--CLIENT
INSERT INTO Client(Title, FirstName, LastName, AddressLine1, AddressLine2, Town, County, Postcode, PhoneNumber, EmailAddress)
VALUES 	('Ms', 'Devi', 'Tristram', '55 Meadow View','', 'Manchester', 'Greater Manchester','M22 2LL', 07123456789, 'dtristram0@google.com'),
	('Mr', 'Sid', 'Durning', '34 Hollow Ridge Parkway','', 'Liverpool', 'Merseyside', 'L11 1PP',07426607195, 'sdurning1@constantcontact.com'),
	('Dr', 'Isidore', 'Axston',	'7th Way', '', 'Liverpool', 'Merseyside', 'L44 9PU', 07669147561,'iaxston2@free.fr'),
	('Mr', 'Geoff',	'Borgnet', '94 Melody Plaza', '', 'Manchester', 'Greater Manchester', 'M1 9YY', 07596652798, 'gborgnet3@exblog.com'),
	('Mrs',	'Rosella', 'Frensche', '40 Clemons Circle','', 'Manchester', 'Greater Manchester','M78 9NN', 077788831245, 'rfrensche4@merriam-webster.com');

SELECT * from Client;

--Vendor
INSERT INTO Vendor(Title, FirstName, LastName, AddressLine1, AddressLine2, Town, County, Postcode, PhoneNumber, EmailAddress, OwnershipType)
VALUES 	('Ms','Diana','Tram', '34 Fairview Crossing', 'Upton','Manchester','Greater Manchester', 'M1 4BM',05528445529,'dtram0@google.com','Single'),
	('Mrs','Noreen','Petrus','6 Myrtle Way','Greasby','Manchester','Greater Manchester','M23 4DS', 03533911607,'npetrus@google.com','Single'),
	('Mrs','Cristina','Meach','4187 Monument Point','Standish','Manchester','Greater Manchester','M71 7WW',07869692818,'cmeach@hotmail.com','Single'),
	('Mr','Webster','Dulanty','4 Orin Drive','Irby','Manchester','Greater Manchester','M53 4KH',03445694658,'wdulanty@google.com','Single'),
	('Mr','Chad','Romney','75 Lyons Crossing','Birkenhead','Manchester','Greater Manchester','M12 3TT',07902538907,'cromney@gmail.com','Joint');

SELECT * from Vendor;

--Insert statements for Property
INSERT INTO Property(AddressLine1, AddressLine2, Town, County, Postcode, BuildDate, ListedDate, SoldDate, PropertyValue, PropertyStatus, PropertyType, AgentId, VendorId)
VALUES 	('755 Oasis Point', 'Altrincham', 'Manchester', 'Greater Manchester', 'M11 1UU', '1995-05-05','2020-05-05','', 800000.50,'On the Market','Detached', 1,5);

--More insert statements for Property
INSERT INTO Property(AddressLine1, AddressLine2, Town, County, Postcode, BuildDate, ListedDate, SoldDate, PropertyValue, PropertyStatus, PropertyType, AgentId, VendorId)
VALUES 	('5 Peak Street', 'Timperley', 'Manchester', 'Greater Manchester', 'M11 1UU', '1999-05-05','2020-05-05','', 600000.50,'On the Market','Detached', 1,1),
	('80 Beverly Hills', 'Standish', 'Wirral', 'Merseyside', 'L71 1UT', '2005-05-05','2020-08-05','', 550000.50,'On the Market','Semi-Detached', 2,2),		
	('99 Boston Road', 'Sale', 'Manchester', 'Greater Manchester', 'M41 1YU', '2020-05-05','2020-08-05','', 500000.50,'On the Market','Terraced', 3,3),
	('6 Belmont Grove', 'Altrincham', 'Manchester', 'Greater Manchester', 'M91 1PU', '2001-05-05','2020-09-05','', 199000.50,'On the Market','Bungalow', 4,4);

INSERT INTO Property(AddressLine1, AddressLine2, Town, County, Postcode, BuildDate, ListedDate, SoldDate, PropertyValue, PropertyStatus, PropertyType, AgentId, VendorId)
VALUES 	('90 Beverly Hills', 'Standish', 'Wirral', 'Merseyside', 'L71 1UT', '2005-05-05','2020-08-09','', 500000.50,'On the Market','Semi-Detached', 2,2);

SELECT * from Property;

--Insert statements for Viewing
INSERT INTO Viewing(ViewingDate,ViewingTime,Outcome,ClientId,PropertyId,NNStaffNo)
VALUES ('2020-09-01', '13:15:00','No Show',1,1,4);

--More insert statements for Viewing
INSERT INTO Viewing(ViewingDate,ViewingTime,Outcome,ClientId,PropertyId,NNStaffNo)
VALUES 	('2020-09-10', '10:00:00','Attended',1,1,4),
		('2020-09-09', '12:15:00','Attended',2,5,4),
		('2020-08-01', '10:00:00','Attended',2,4,2),
		('2020-07-01', '12:30:00','Attended',3,3,1),
		('2020-08-01', '13:00:00','Attended',3,3,1),
		('2020-09-21', '13:15:00','Attended',4,2,5),
		('2020-09-16', '15:30:00','Attended',4,2,4),
		('2020-10-01', '13:15:00','Attended',5,3,3),
		('2020-09-01', '15:15:00','Attended',5,1,3);

SELECT * FROM Viewing;

--Insert statements for Offers Table
INSERT INTO Offers(OfferStage,OfferStatus,OfferValue,ClientId,PropertyId)
VALUES ('Initial','Pending',750000,1,1);

INSERT INTO Offers(OfferStage,OfferStatus,OfferValue,ClientId,PropertyId)
VALUES 	('Final','Pending',790000,1,1),
	('Final','Accepted',599000,1,2),
	('Initial','Pending',590000,2,2),
	('Final','Pending',540000,3,3),
	('Initial','Pending',499000,1,4);

SELECT * FROM Offers;
```

### Queries
1.	List all properties located in the city of Manchester with a list price of over £200,000

```sql
SELECT * FROM Property
WHERE PropertyValue > 200000
AND Town Like 'Manchester' OR Town Like 'MANCHESTER';
```

2.	List all viewings that took place in August or September 2020 and the clients who requested the viewings
```sql
SELECT ViewingId, ViewingDate, ViewingTime, Outcome, Client.ClientId, Title,FirstName,LastName
FROM Viewing INNER JOIN Client
ON Viewing.ClientId = Client.ClientId
where (strftime('%m', ViewingDate) = '08' OR strftime('%m', ViewingDate) = '09') AND strftime('%Y', ViewingDate) = '2020';
```

3.	For each owner, list their total portfolio value (i.e. the total of all their properties’ prices) but only for properties which are houses.

```sql
SELECT Title, FirstName, LastName,SUM(PropertyValue),PropertyStatus,PropertyType
FROM Vendor INNER JOIN Property
USING (VendorId)
WHERE PropertyType Like '%Detached%' OR PropertyType Like '%Terraced%'
GROUP BY FirstName;
```

4.	For each property, list the smallest offer made by clients and which client made the offer, but only for properties which have not been sold

```sql
SELECT Client.FirstName, Client.LastName, MIN(OfferValue), OfferStage, OfferStatus,propertystatus, Property.PropertyId
FROM Client, Offers, Property
where Client.ClientId = Offers.ClientId 
and Property.PropertyId = Offers.PropertyId
GROUP BY Property.PropertyId
```
