# Venturing Database Design

## Modules

The Venturing Database will be made up of modules that focus on specific tasks within the Venturing program.  These modules will consist of

1. Scouting Organization
2. Participants
3. Address (U.S. Based)
3. Outdoor Program
4. HEAT Program
5. Advancement
6. Leadership
7. Finance
8. Inventory

## Scouting Organization

1. **Unit:** Provides the basic information related to the scouting unit.
2. **UnitEvent:** Records information regarding changes to a scouting unit.
3. **UnitType:** Records the type of unit in the scouting organization.
4. **UnitTypeEvent:** Records changes to the Unit Type
5. **Location:** Provides the meeting location for the unit
6. **LocationEvent:** Records changes to the unit location
7. **MeetingTime:** Provides the meeting time for the unit
8. **MeetingTimeEvent:** Records changes to the meeting time

### Unit

| Column Name    | Column Type  | Event Tracked | Description |
|----------------|--------------|---------------|-------------|
| OID            | INT          | No            | Object Identifier |
| UnitType       | INT          | Yes           | Reference to UnitType.OID |
| UnitNumber     | INT          | Yes           | The unit number |
| Location       | INT          | Yes           | Reference to Location.OID |
| MeetingTime    | INT          | Yes           | Reference to MeetingTime.OID |
| IsActive       | BIT          | Yes           | Is the unit active? |

### UnitEvent

| Column Name    | Column Type  | Event Tracked | Description |
|----------------|--------------|---------------|-------------|
| OID            | INT          | No            | Object Identifier |
| Unit           | INT          | No            | Reference to Unit.OID |
| EventType      | VARCHAR(20)  | No            | Create, EditType, EditNumber, EditLocation, EditMeetingTime, Activate, Deactivate |
| EventUser      | INT          | No            | Reference to Participant.OID |
| EventDateTime  | DateTime     | No            | DateTime of the event. | 

### UnitType

| Column Name    | Column Type  | Event Tracked | Description |
|----------------|--------------|---------------|-------------|
| OID            | INT          | No            | Object Identifier |
| Description    | VARCHAR(20)  | Yes           | e.g., Pack, Troop, Crew, Post |
| IsActive       | BIT          | Yes           | Is the unit type active? |

### UnitTypeEvent

| Column Name    | Column Type  | Event Tracked | Description |
|----------------|--------------|---------------|-------------|
| OID            | INT          | No            | Object Identifier |
| UnitType       | INT          | No            | Reference to UnitType.OID |
| EventType      | VARCHAR(20)  | No            | Create, EditDescription, Activate, Deactivate |
| EventUser      | INT          | No            | Reference to Participant.OID |
| EventDateTime  | DateTime     | No            | DateTime of the event. | 

### Location

| Column Name    | Column Type  | Event Tracked | Description |
|----------------|--------------|---------------|-------------|
| OID            | INT          | No            | Object Identifier |
| LocationName   | VARCHAR(250) | Yes           | Name of the Location | 
| Address        | INT          | Yes           | Reference to Address.OID |
| IsActive       | BIT          | Yes           | Is the location active? |

### LocationEvent

| Column Name    | Column Type  | Event Tracked | Description |
|----------------|--------------|---------------|-------------|
| OID            | INT          | No            | Object Identifier |
| Location       | INT          | No            | Reference to Location.OID |
| EventType      | VARCHAR(20)  | No            | Create, EditLocation, EditAddress, Activate, Deactivate |
| EventUser      | INT          | No            | Reference to Participant.OID |
| EventDateTime  | DateTime     | No            | DateTime of the event. | 

### MeetingTime

| Column Name    | Column Type  | Event Tracked | Description |
|----------------|--------------|---------------|-------------|
| OID            | INT          | No            | Object Identifier | 
| StartTime      | TIME         | Yes           | Time the meeting starts |
| Endtime        | TIME         | Yes           | Time the meeting ends |
| IsActive       | BIT          | Yes           | Is the meeting time active? |

### MeetingTimeEvent

| Column Name    | Column Type  | Event Tracked | Description |
|----------------|--------------|---------------|-------------|
| OID            | INT          | No            | Object Identifier |
| EventType      | VARCHAR(20)  | No            | Create, EditStartTime, EditEndTime, Activate, Deactivate |
| EventUser      | INT          | No            | Reference to Participant.OID |
| EventDateTime  | DateTime     | No            | DateTime of the event. | 

## Participants

The participants module provides the infrastructure for identifying individuals, their role with the unit, and details regarding
their participation. This module will provide support to all other modules in the database system.

For simplicity, these tables will be U.S. centric and include a first name and last name.

### Tables

1. **Person:** Records the basic information related to individuals participating in the scouting unit.
2. **PersonEvent:** Records information regarding changes to a participant.
3. **Address:** Records a participant's (or location's) address information.
4. **Phone:** Records of participant phone numbers.
5. **EmailAddress:** Records a participant's email address.
6. **ContactInfoEvent:** Records changes to participant address, phone, or e-mail address.

## Address

1. **Address:** Records of addresses for locations and people
2. **AddressStreet:** Child records allowing multi-line addresses
3. **State:** Table of state names and postal abbreviations

### Address

| Property    |  Type          | Event Track | Description |
|-------------|----------------|-------------|-------------|
| OID         |  INT           |  No         | Object Identifier |
| City        |  VARCHAR(250)  |  Yes        | City name |
| State       |  INT           |  Yes        | Reference to State.OID |
| Zip         |  VARCHAR(10)   |  Yes        | ZIP Code (12345-1234) |
| IsMailing   |  BIT           |  Yes        | Is the Address a Mailing Address |
| IsPhysical  |  BIT           |  Yes        | Is the address a physical address |
| IsActive    |  BIT           |  Yes        | Is the address active |


### AddressEvent

| Property       |  Type          | Event Track | Description |
|----------------|----------------|-------------|-------------|
| OID            |  INT           |  No         | Object identifier |
| ParentAddress  |  INT           |  No         | Reference to Address.OID |
| EventType      |  VARCHAR(12)   |  No         | (Create, EditCity, EditState, EditZip, EditMailing, EditPhysical, Activate, Deactivate) |
| PreviousValue  |  VARCHAR(250)  |  No         | Previous value of the property |
| EventUser      |  INT           |  No         | Reference to Person.OID |
| EventDateTime  |  DATETIME      |  No         | DateTime of the event |


### AddressStreet

| Property     |  Type          | Event Track | Description |
|--------------|----------------|-------------|-------------|
| OID          |  INT           |  No         | Object identifier |
| Address      |  INT           |  Yes        | Reference to Address.OID   |
| Order        |  INT           |  Yes        | Address line order |
| AddressLine  |  VARCHAR(250)  |  Yes        | Address line content |
| IsActive     |  BIT           |  Yes        | Is this line active? |


### AddressStreetEvent

| Property             |  Type          | Event Track | Description |
|----------------------|----------------|-------------|-------------|
| OID                  |  INT           |  No         | Object Identifier |
| ParentAddressStreet  |  INT           |  Reference to AddressStreet.OID |
| EventType            |  VARCHAR(12)   |  (Create, EditAddress, EditOrder, Activate, Deactivate) |
| PreviousValue        |  VARCHAR(250)  |  Previous value of the property |
| EventUser            |  INT           |  Reference to Person.OID |
| EventDateTime        |  DATETIME      |  DateTime of the event |

### State

| Property           |  Type          | Event Track | Description |
|--------------------|----------------|-------------|-------------|
| OID                |  INT           |  No         | Object identifier |
| State              |  VARCHAR(20)   |  Yes        | State Name  |
| StateAbbreviation  |  VARCHAR(2)    |  Yes        | State Postal Abbreviation |
| IsActive           |  BIT           |  Yes        | Is the State Active? |


### StateEvent 

| Property      |  Type          | Event Type | Description |
|---------------|----------------|------------|-------------|
| OID           | INT            | No         | Object identifier |
| ParentState   | INT            | No         | Reference to State.OID |
| EventType     | VARCHAR(12)    | No         | (Create, EditState, EditAbbrev, Activate, Deactivate) |
| EventUser     | INT            | No         | Reference to Person.OID |
| EventDateTime | DATETIME       | No         | DateTime of the event |


### Leadership

1. **Role:** Records unit leadership roles
2. **RoleEvent:** Records changes in unit leadership roles
3. **Leadership:** Records leadership roles being filled by participants.

###
