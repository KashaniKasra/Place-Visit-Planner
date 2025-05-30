# Place Visit Planner

This is a C++ program designed to efficiently plan and optimize a schedule for visiting a set of places within a given day based on constraints such as opening/closing times and place rankings.

## Features

- Reads structured CSV input listing locations, their opening/closing times, and priority ranks.
- Calculates the most optimal order to visit locations based on:
  - Whether a place is open and available for visiting.
  - Whether it has already been visited.
  - Which places are ranked higher (lower rank value is better).
- Visits are planned in 1-hour slots with 30-minute transitions.
- Outputs a detailed plan including the name of each location and visit time interval.

## Input File Format

The input CSV must contain rows structured like this:

```
name,openingTime,closingTime,rank
Place A,09:00,17:00,1
Place B,10:30,15:00,3
Place C,08:00,18:00,2
...
```

- `name`: The name of the place.
- `openingTime`, `closingTime`: Format must be `HH:MM`.
- `rank`: An integer representing how desirable the location is (lower is better).

## Compilation

To compile the code, use g++ or any modern C++ compiler:

```bash
g++ -std=c++11 -o planner "Place visit planner.cpp"
```

## Usage

Once compiled, run the program by passing the path to the input CSV file:

```bash
./planner input.csv
```

## Output Format

Each visit is printed in the following format:

```
Location Place A
Visit from 08:00 until 09:00
---
Location Place C
Visit from 09:30 until 10:30
---
...
```

- Each entry specifies the place name and the time window of the visit.
- The program ends when no more feasible locations are available to visit within the day.

## Logic and Constraints

- Visits are 1 hour long where possible.
- There’s a 30-minute transition time between each visit.
- If multiple places are visitable at the same time, the one with the better (lower) rank is chosen.
- If no place is currently open, the program waits for the next one to open.
- Places are not revisited.