# Official Requirements Document

Authors: Maurizio Morisio, Luca Ardito, Riccardo Coppola

Date: 24/03/2020


# Contents
- [Abstract](#abstract)
- [Stakeholders](#stakeholders)
- [Context Diagram and interfaces](#context-diagram-and-interfaces)
	+ [Context Diagram](#context-diagram)
	+ [Interfaces](#interfaces) 
	
- [Stories and personas](#stories-and-personas)
- [Functional and non functional requirements](#functional-and-non-functional-requirements)
	+ [Functional Requirements](#functional-requirements)
	+ [Non functional requirements](#non-functional-requirements)
- [Use case diagram and use cases](#use-case-diagram-and-use-cases)
	+ [Use case diagram](#use-case-diagram)
	+ [Use cases](#use-cases)
	+ [Relevant scenarios](#relevant-scenarios)
- [Glossary](#glossary)
- [System design](#system-design)
- [Deployment diagram](#deployment-diagram)

# Abstract

Some colleagues share a coffee machine in a common space for breaks. Capsules are left aside the machine. Whoever uses a capsule writes this down in a notebook left aside the coffee machine. One of the colleagues (called *administrator*) copies consumptions in an excel sheet and collects money from colleagues to (re)order capsules.

One of the colleagues, the *hacker*, volunteers to develop a simple application to support the administrator. To keep things simple the application is standalone, and is meant to be used only by the administrator. Possibly the administrator role is taken by different colleagues over time. Instead of the notebook, the hacker sets up a WhatsApp group. Whenever a colleague uses a capsule, he sends a message to the group.


# Stakeholders

| Stakeholder name  | Description | 
| ----------------- |:-----------:|
| User     |Uses the application to locate gas stations and the prices in an area | 
| Admin    |Uses the application to add/remove gas station and manage errors | 

# Context Diagram and interfaces

## Context Diagram

```plantuml
left to right direction
actor User as a
a -- (EZGas)
```

## Interfaces
| Actor | Logical Interface | Physical Interface  |
| ------------- |:-------------:| -----:|
|User|GUI |Touch Screen|


# Stories and personas
Joseph has few amount of money and want to get the fuel but it is in riserva. He open the application and looking for the nearest gas station with the lowest price and goes there.

Mark is a statistic and want to evalutate the number of gas station for each geographic area to analyse if there are some correlation with the geographical position and how the tecnlogical advantage affect the gas sation distribution. 

Mary is a stranger and doen't know anithing of the country, she has a car and she what to get fuel but she down't know the location of gas stations and also the price of the fuel in that country. She uses the app to find the best palce to go.

Frank find an error in the 

# Functional and non functional requirements

## Functional Requirements

| ID        | Description  |
| ------------- |:-------------:| 
|  FR1     | Record new gas station opened |  
|  FR2     | Record the location of a gas station  |
|  FR3     | Record price for each type of fuel for a gas station |
|  FR4     | Record that n capsules of a certain type have been received, and paid for |
|  FR5     | Produce a list/map visualization of all gas station in a choosen area |
|  FR6     | Produce the indication of each fuel type from a chosen gas station |
|  FR7     | Manage types fuels |
|  FR8     | Manage areas of gas stations |
|  FR9     | Manage closed gas stations |
## Non Functional Requirements

| ID        | Type (efficiency, reliability, .. see iso 9126)           | Description  | Refers to |
| ------------- |:-------------:| :-----:| -----:|
|  NFR1     | Usability | Application should be intuitive and easy to used for any type of users  | All FR |
|  NFR2     | Performance | All functions should complete in < 0.5 sec  | All FR |
|  NFR3     | Portability | The application runs on android / iOS (android 5.0 / iOS 6)  | All FR |
|  NFR4     | Maintainability | Administrator add/remove information from application. The time to do a change should be little ||


# Use case diagram and use cases

## Use case diagram

```plantuml
left to right direction
actor Administrator as a
a -- (FR1  Record usage of capsules by colleague)
a -- (FR2 Record usage of capsules by visitor)
a -- (FR3 Record recharge of account of colleague)
a -- (FR4 Record purchase of capsules)
a -- (FR5 Produce report on consumption of colleague)
a -- (FR6 Produce report on all consumptions)
```
## Use Cases

### Use case 1, UC1 - FR1  Record usage of capsules by colleague

| Actors Involved        | Administrator |
| ------------- |:-------------:| 
|  Precondition     | Capsule T exists, colleague C exists |  
|  Post condition     | T.quantity_post < T.quantity_pre |
| | C.PersonalAccount.balance_post < C.PersonalAccount.balance_pre |
|  Nominal Scenario     | Administrator selects capsule type T, selects colleague C, Deduce quantity for capsule T, deduce price of T by account of colleague C|
|  Variants     | Account of colleague C has not enough money, issue warning |

### Use case 2, UC2 - FR2 Record usage of capsules by visitor

| Actors Involved        | Administrator |
| ------------- |:-------------:| 
|  Precondition     | Capsule T exists, visitor has no account |  
|  Post condition     | T.quantity_post < T.quantity_pre |
| | LaTazzaAccount.amount_post > LaTazzaAccount.amount_pre |
|  Nominal Scenario     | Administrator selects capsule type T, Deduce quantity for capsule T, add price of T on LaTazzaAccount.amount|
|  Variants     |  |

### Use case 3, UC3 - FR3 Record recharge of account of colleague

| Actors Involved        | Administrator |
| ------------- |:-------------:| 
|  Precondition     | Personal Account PA exists , quantity >0 |  
|  Post condition     | PA.balance_post = PA.balance_pre + quantity |
|  | LaTazzaAccount.balance_post = LaTazzaAccount.balance_pre + quantity  |
|  Nominal Scenario     | Administrator selects account PA of colleague C, increase account of  quantity, increase LaTazza account of quantity|
|  Variants     |  |

### Use case 4, UC4 - FR4 Record purchase of capsules

| Actors Involved        | Administrator |
| ------------- |:-------------:| 
|  Precondition     | Capsule type CT exists,  LaTazzaAccount.balance has enough money for the purchase|  
|  Post condition     | CT.quantity_post > CT.quantity _pre |
| | LaTazzaAccount.balance_post < LaTazzaAccount.balance_pre|
|  Nominal Scenario     | At time of order Administrator records money spent for order. At time of reception administrator selects capsule type CT, increases its quantity by a given number|
|  Variants     |  |

### Use case 5, FR5 Produce report on consumption of colleague

| Actors Involved        | Administrator  |
| ------------- |:-------------:| 
|  Precondition     | Colleague C exists |  
|  Post condition     |  |
|  Nominal Scenario     | Administrator selects colleague C, defines a time range,  application collects all transactions for C (recharges and capsules taken) in the time range and presents them|
|  Variants     | |

### Use case 6, FR6 Produce report on all consumptions

| Actors Involved        | Administrator |
| ------------- |:-------------:| 
|  Precondition     |  |  
|  Post condition     |  |
|  Nominal Scenario     | Administrator defines a time range,  application collects all transactions (recharges, purchases, and capsules taken) in the time range and presents them |
|  Variants     | |


# Relevant scenarios

## Scenario 1

| Scenario ID: SC1        | Corresponds to UC1  |
| ------------- |:-------------| 
| Description | Colleague uses one capsule of type T|
| Precondition |  account of C has enough money to buy capsule T|
| Postcondition |  account of C updated, count of T updated |
| Step#        |  Step description   |
|  1     | Administrator selects capsule type T |  
|  2     |  Administrator selects colleague C |
|  3     | Deduce one for quantity of capsule T |
| 4 | Deduce price of T from account of C|

## Scenario 2

| Scenario ID: SC2        | Corresponds to UC1  |
| ------------- |:-------------| 
| Description | Colleague uses one capsule of type T, account negative|
|Precondition |  account of C has not enough money to buy capsule T|
|Postcondition |  account of C updated, count of T updated |
| Step#        | Step description  |
|  1     | Administrator selects capsule type T |  
|  2     | Administrator selects colleague C |
|  3     | Deduce one for quantity of capsule T  |
|  4     | Deduce price of T from account of C  |
|  5     | Account of C is negative, issue warning  |


# Glossary

```plantuml
class LaTazza
class Colleague {
+ name
+ surname
}

class PersonalAccount {
+ balance
}

class CapsuleType {
+ name
+ price
+ quantity
}

class LaTazzaAccount {
+ balance
}

class BoxPurchase {
+ quantity
}

class Transaction {
+ date
+ amount
}

class Recharge
class Consumption


LaTazza -- "*" Colleague
LaTazza -- "*" CapsuleType
LaTazza -- LaTazzaAccount

LaTazzaAccount -- "*" BoxPurchase
LaTazzaAccount -- "*" Consumption

CapsuleType -- "*" Consumption
CapsuleType -- "*" BoxPurchase

Colleague -- PersonalAccount
PersonalAccount -- "*" Transaction

Transaction <|-- Recharge
Transaction <|-- Consumption
Transaction <|-- BoxPurchase

```

# System Design
Not really meaningful in this case. Only one personal computer is needed.

```plantuml
class "Personal Computer"
```

# Deployment Diagram
As a stand-alone application only one node is needed.

```plantuml
artifact "La Tazza Application" as a
node "Personal Computer" as n
a -- n
```

