# Venturing Database Design

## Modules

The Venturing Database will be made up of modules that focus on specific tasks within the Venturing program.  These modules will consist of

1. Scouting Organization
2. Participants
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

| Table Name       | Column Name    | Column Type  | Event Tracked | Description |
|------------------|----------------|--------------|---------------|-------------|
| Unit             | OID            | INT          | No            | Object Identifier |
| Unit             | UnitType       | INT          | Yes           | Reference to UnitType.OID |
| Unit             | UnitNumber     | INT          | Yes           | The unit number |
| Unit             | Location       | INT          | Yes           | Reference to Location.OID |
| Unit             | MeetingTime    | INT          | Yes           | Reference to MeetingTime.OID |
| Unit             | IsActive       | BIT          | Yes           | Is the unit active? |
| UnitEvent        | OID            | INT          | No            | Object Identifier |
| UnitEvent        | Unit           | INT          | No            | Reference to Unit.OID |
| UnitEvent        | EventType      | VARCHAR(20)  | No            | Create, EditType, EditNumber, EditLocation, EditMeetingTime, Activate, Deactivate |
| UnitEvent        | EventUser      | INT          | No            | Reference to Participant.OID |
| UnitEvent        | EventDateTime  | DateTime     | No            | DateTime of the event. | 
| UnitType         | OID            | INT          | No            | Object Identifier |
| UnitType         | Description    | VARCHAR(20)  | Yes           | e.g., Pack, Troop, Crew, Post |
| UnitType         | IsActive       | BIT          | Yes           | Is the unit type active? |
| UnitTypeEvent    | OID            | INT          | No            | Object Identifier |
| UnitTypeEvent    | UnitType       | INT          | No            | Reference to UnitType.OID |
| UnitTypeEvent    | EventType      | VARCHAR(20)  | No            | Create, EditDescription, Activate, Deactivate |
| UnitTypeEvent    | EventUser      | INT          | No            | Reference to Participant.OID |
| UnitTypeEvent    | EventDateTime  | DateTime     | No            | DateTime of the event. | 
| Location         | OID            | INT          | No            | Object Identifier |
| Location         | LocationName   | VARCHAR(250) | Yes           | Name of the Location | 
| Location         | Address        | INT          | Yes           | Reference to Address.OID |
| Location         | IsActive       | BIT          | Yes           | Is the location active? |
| LocationEvent    | OID            | INT          | No            | Object Identifier |
| LocationEvent    | Location       | INT          | No            | Reference to Location.OID |
| LocationEvent    | EventType      | VARCHAR(20)  | No            | Create, EditLocation, EditAddress, Activate, Deactivate |
| LocationEvent    | EventUser      | INT          | No            | Reference to Participant.OID |
| LocationEvent    | EventDateTime  | DateTime     | No            | DateTime of the event. | 
| MeetingTime      | OID            | INT          | No            | Object Identifier | 
| MeetingTime      | StartTime      | TIME         | Yes           | Time the meeting starts |
| MeetingTime      | Endtime        | TIME         | Yes           | Time the meeting ends |
| MeetingTime      | IsActive       | BIT          | Yes           | Is the meeting time active? |
| MeetingTimeEvent | OID            | INT          | No            | Object Identifier |
| MeetingTimeEvent | EventType      | VARCHAR(20)  | No            | Create, EditStartTime, EditEndTime, Activate, Deactivate |
| MeetingTimeEvent | EventUser      | INT          | No            | Reference to Participant.OID |
| MeetingTimeEvent | EventDateTime  | DateTime     | No            | DateTime of the event. | 

## Participants

The participants module provides the infrastructure for identifying individuals, their role with the unit, and details regarding
their participation. This module will provide support to all other modules in the database system.

### Tables

1. **Participant:** Records the basic information related to individuals participating in the scouting unit.
2. **ParticipantEvent:** Records information regarding changes to a participant.
3. **Address:** Records a participant's address information.
4. **Phone:** Records of participant phone numbers.
5. **EmailAddress:** Records a participant's email address.
6. **ContactInfoEvent:** Records changes to participant address, phone, or e-mail address.



### Leadership

1. **Role:** Records unit leadership roles
2. **RoleEvent:** Records changes in unit leadership roles
3. **Leadership:** Records leadership roles being filled by participants.

###
