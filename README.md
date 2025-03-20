# project_1_4610

## Group Members - Group 4
- [Tobias Allers](https://github.com/tka29934/project_1_4610/tree/main)
- [Luke Mabry]
- [Alicia Lim]
- [Chris Sierra]
- [Pranav Rohit]

## Project Scenario and Overview
We were given the task of creating a new, high level for the NBA. They wanted database that could give an overview of their franchise. We built the data model with Teams being the central entity, and most other entities, such as executives on the team board, brand sponsorships, and coaches and players stemming from this primary entity. We were charged with building a data model to visualize the database, populate the database with data relevant to the NBA, and write queries to prove the efficacy of the database built.

## Data Model
<img width="568" alt="MIST 4610 Project 1 Data Model" src="https://github.com/user-attachments/assets/39af895d-bcab-4eb2-b48f-310f4b6cb46b" />


## Data Dictionary

<img width="636" alt="Screenshot 2025-03-20 at 12 26 50 PM" src="https://github.com/user-attachments/assets/7037747a-78c2-421f-bd51-28987c4ee8fc" />
<img width="632" alt="Screenshot 2025-03-20 at 12 27 05 PM" src="https://github.com/user-attachments/assets/a2487ea8-c71c-4ebb-b5c8-3aa06e1d1210" />
<img width="633" alt="Screenshot 2025-03-20 at 12 27 44 PM" src="https://github.com/user-attachments/assets/17260096-fb32-47c7-bec5-7dcf4f75a41f" />
<img width="633" alt="Screenshot 2025-03-20 at 12 28 12 PM" src="https://github.com/user-attachments/assets/f1756d02-dae2-4330-ac15-38f9b2484580" />
<img width="635" alt="Screenshot 2025-03-20 at 12 28 42 PM" src="https://github.com/user-attachments/assets/95d6a982-134b-4b09-83d5-8b224b815d92" />
<img width="635" alt="Screenshot 2025-03-20 at 12 29 23 PM" src="https://github.com/user-attachments/assets/6ef7c94e-139b-4525-99e7-e1349ed9de0f" />
<img width="638" alt="Screenshot 2025-03-20 at 12 30 15 PM" src="https://github.com/user-attachments/assets/8996f146-a84f-4cab-a720-59807d18bc7a" />
<img width="639" alt="Screenshot 2025-03-20 at 12 30 35 PM" src="https://github.com/user-attachments/assets/dbb9f77f-457c-4b67-bf69-48c36ac2625e" />
<img width="633" alt="Screenshot 2025-03-20 at 12 30 56 PM" src="https://github.com/user-attachments/assets/1420e97e-dccd-4fae-a9f1-49e8794f5c81" />
<img width="640" alt="Screenshot 2025-03-20 at 12 31 19 PM" src="https://github.com/user-attachments/assets/609545fc-320b-4416-b6ec-871e9850ed35" />
<img width="634" alt="Screenshot 2025-03-20 at 12 31 41 PM" src="https://github.com/user-attachments/assets/741881e7-66f6-4702-bfdc-ea26e5016dd5" />

## Queries

## Query 1 and Description

SELECT s.seasonYear, s.seasonWinner
FROM Seasons s
WHERE EXISTS (
    SELECT 1
    FROM Teams t
    WHERE t.teamName = s.seasonWinner
    AND t.dateFormed < '1980-01-01'
    AND t.numFans < 10000000);

## Description: Gives Team Name and seasonYear of teams who are seasonWinners and were formed before 1980 and also have less than 10000000 fans. (Shows significant smaller market teams who have been good recently, could be used to bump up league revenue distributed to these teams due to tenure in league and success level).

## Query 2 and Description

SELECT e.execID, e.firstName, e.lastName
FROM Executives e
WHERE EXISTS (
    SELECT 1
    FROM Teams t
    JOIN Cities c ON t.homeCity = c.cityID
    WHERE e.teamWorkedFor = t.teamName
    AND c.population > 800000  -- Try lowering the threshold);

## Description: Displays execID, firstName, and lastName of Executives that work for teams which are located in cities with a population of 800,000 or more. The reason for this query is because if you are a player’s agent (person who tries to find a player a contract on a team) and are trying to find a large market team for your player to play for, you would want to contact one of these executives. 

## Query 3 and Description
 
Select specialty, Coaches.firstName, Coaches.lastName, Coaches.teamSigned
From Coaches
Where specialty On (
Select specialty From Coaches Group By specialty Having Count(*)>1)
Order By specialty, Coaches.lastName;

##Description: This query identifies the coaches that have similar specialties and what team they coach for. This is important for executives choosing a specific coach that they believe will be beneficial to the team and to be a better fit for a manager. From a ownership perspective, understanding which position the coach is in, and how successful their team has been under their tenure in their specialty will help to narrow down the options for a new coach for that specialty. 


## Query 4 and Description

 Select Teams.teamName, Players.firstName, Players.lastName, Players.yearsPlayed
 From Teams
 Join Players ON Teams.teamName=Players.teamSigned
 Where Teams.teamName  (
	Select teamSigned From Players Group By teamSigned Having Avg(yearsPlayed)>5)
    Order By Players.yearsPlayed DESC;

##Description: This helps to narrow down the experience of players by filtering through the amount of years played and ordering the number of players who have played over 5 years. This helps Executives to select a player that has some more experience and give them a shot of winning a championship with that team. 



## Query 5 and Description


## Query 6 and Description


## Query 7 and Description


## Query 8 and Description


## Query 9 and Description


## Query 10 and Description




