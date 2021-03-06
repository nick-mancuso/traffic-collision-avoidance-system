# traffic-collision-avoidance-system

Scott Fones and Nick Mancuso

## Predicate Coverage

### Predicates

Own_Below_Threat()

`Own_Tracked_Alt < Other_Tracked_Alt`

Own_Above_Threat()

`Other_Tracked_Alt < Own_Tracked_Alt`

Positive_RA_Alt_Thresh()

`Alt` 0 - 3

Inhibit_Biased_Climb()

`Climb_Inhibit` T \ F

Non_Crossing_Biased_Climb()

`upward_preferred`

`result`

Non_Crossing_Biased_Descend()

`upward_preferred`

`result`

alt_sep_test()

`enabled`

`tcas_equipped`

`intent_not_known`

enabled && ((tcas_equipped && intent_not_known) || !tcas)

`need_upward_RA && need_downward_RA`

`need_upward_RA`

`need_downward_RA`

main()
`argc`

### Truth Tables

Own_Below_Threat()                  

| Own_Tracked_Alt < Other_Tracked_Alt |
|-------------------------------------|
| T                                   |
| F                                   |

Own_Above_Threat()        

| Other_Tracked_Alt < Own_Tracked_Alt |
|-------------------------------------|
| T                                   |
| F                                   |


Positive_RA_Alt_Thresh() 

| Alt |
|-----|
| 0   |
| 1   |
| 2   |
| 3   |


Inhibit_Biased_Climb()


| Climb_Inhibit |
|---------------|
| T             |
| F             |

Non_Crossing_Biased_Climb()

`upward_preferred`


| Inhibit_Biased_Climb() > Down_Separation | upward_preferred |   |   |   |   |   |   |
|------------------------------------------|------------------|---|---|---|---|---|---|
| T                                        | T                |   |   |   |   |   |   |
| F                                        | F                |   |   |   |   |   |   |


| Climb_Inhibit | Up_Separation + 100 > Down_Separation | upward_preferred |
|---------------|---------------------------------------|------------------|
| T             | T                                     | T                |
| T             | F                                     | F                |


| Climb_Inhibit | Up_Separation > Down_Separation | upward_preferred |
|---------------|---------------------------------|------------------|
| F             | T                               | T                |
| F             | F                               | F                |


`result`

| upward_preferred | Own_Below_Threat() | Down_Separation >= ALIM() | result |
|------------------|--------------------|---------------------------|--------|
| T                | T                  | T                         | F      |
| T                | T                  | F                         | T      |
| T                | F                  | T                         | T      |
| T                | F                  | F                         | T      |

| upward_preferred | Own_Above_Threat() | Cur_Vertical_Sep >= 300 | Up_Separation >= ALIM() | result |
|------------------|--------------------|-------------------------|-------------------------|--------|
| F                | T                  | T                       | T                       | T      |
| F                | T                  | T                       | F                       | F      |
| F                | T                  | F                       | T                       | F      |
| F                | T                  | F                       | F                       | F      |
| F                | F                  | T                       | T                       | F      |
| F                | F                  | T                       | F                       | F      |
| F                | F                  | F                       | T                       | F      |
| F                | F                  | F                       | F                       | F      |

Non_Crossing_Biased_Descend

`upward_preferred`


| Inhibit_Biased_Climb() > Down_Separation | upward_preferred |
|------------------------------------------|------------------|
| T                                        | T                |
| F                                        | F                |


| Climb_Inhibit | Up_Separation + 100 > Down_Separation | upward_preferred |
|---------------|---------------------------------------|------------------|
| T             | T                                     | T                |
| T             | F                                     | F                |

| Climb_Inhibit | Up_Separation + 100 > Down_Separation | upward_preferred |
|---------------|---------------------------------------|------------------|
| T             | T                                     | T                |
| T             | F                                     | F                |

result


| upward_preferred | Own_Below_Threat() | Cur_Vertical_Sep >= 300 | Down_Separation >= ALIM() | result |
|------------------|--------------------|-------------------------|---------------------------|--------|
| T                | T                  | T                       | T                         | T      |
| T                | T                  | T                       | F                         | F      |
| T                | T                  | F                       | T                         | F      |
| T                | T                  | F                       | F                         | F      |
| T                | F                  | T                       | T                         | F      |
| T                | F                  | T                       | F                         | F      |
| T                | F                  | F                       | T                         | F      |
| T                | F                  | F                       | F                         | F      |


| upward_preferred | Own_Above_Threat() | Up_Separation >= ALIM() | result |
|------------------|--------------------|-------------------------|--------|
| F                | T                  | T                       | T      |
| F                | T                  | F                       | F      |
| F                | F                  | T                       | T      |
| F                | F                  | F                       | T      |

alt_sep_test()

`enabled`


| High_Confidence | Own_Tracked_Alt_Rate <= 600 | Cur_Vertical_Sep > 600 | enabled |
|-----------------|-----------------------------|------------------------|---------|
| T               | T                           | T                      | T       |
| T               | T                           | F                      | F       |
| T               | F                           | T                      | F       |
| T               | F                           | F                      | F       |
| F               | T                           | T                      | F       |
| F               | T                           | F                      | F       |
| F               | F                           | T                      | F       |
| F               | F                           | F                      | F       |

`tcas_equipped`

| Other_Capability == 1 | tcas_equipped |
|-----------------------|---------------|
| T                     | T             |
| F                     | F             |

`intent_not_known`

| Two_of_Three_Reports_Valid | Other_RAC == 0 | intent_not_known |
|----------------------------|----------------|------------------|
| T                          | T              | T                |
| T                          | F              | F                |
| F                          | T              | F                |
| F                          | F              | F                |

`enabled && ((tcas_equipped && intent_not_known) || !tcas_equipped)`

| enabled | tcas_equipped | intent_not_known | RESULT |
|---------|---------------|------------------|--------|
| T       | T             | T                | T      |
| T       | T             | F                | F      |
| T       | F             | T                | T      |
| T       | F             | F                | T      |
| F       | T             | T                | F      |
| F       | T             | F                | F      |
| F       | F             | T                | F      |
| F       | F             | F                | F      |

`need_upward_RA`

| enabled | tcas_equipped | intent_not_known | RESULT |
|---------|---------------|------------------|--------|
| T       | T             | T                | T      |
| T       | T             | F                | F      |
| T       | F             | T                | T      |
| T       | F             | F                | T      |
| F       | T             | T                | F      |
| F       | T             | F                | F      |
| F       | F             | T                | F      |
| F       | F             | F                | F      |

`need_downward_RA`

| Non_Crossing_Biased_Descend() | Own_Above_Threat() | need_downward_RA |
|-------------------------------|--------------------|------------------|
| T                             | T                  | T                |
| T                             | F                  | F                |
| F                             | T                  | F                |
| F                             | F                  | F                |

`need_upward_RA && need_downward_RA`


| need_upward_RA | need_downward_RA | need_upward_RA && need_downward_RA |
|----------------|------------------|------------------------------------|
| T              | T                | T                                  |
| T              | F                | F                                  |
| F              | T                | F                                  |
| F              | F                | F                                  |

main()
`argc`

| argc < 13 |
|-----------|
| T         |
| F         |

### Test Case Generation

 - Own_Tracked_Alt > Other_Tracked_Alt and a case with Other_Tracked_Alt > Own_Tracked_Alt

 - Cases where Alt_Layer_Value = {0, 1, 2, 3}

 - Cases where Climb_Inhibit = 0 and Climb_Inhibit = 1

 - Cases where Up_Separation + 100 > Down_Separation and Up_Separation < Down_Separation

 - Cases with Cur_Vertical_Sep = 700 (Cur_Vertical_Sep > 600) and Cur_Vertical_Sep = 5(Cur_Vertical_Sep <= 300

 - High_Confidence = 1

 - Two_of_Three_Reports_Valid = 1

 - Own_Tracked_Alt_Rate = 1 (Own_Tracked_Alt_Rate <= 600)

 - Other_RAC = {0,1}

 - Other_Capability = {0,1}

A=Cur_Vertical_Sep

B=High_Confidence

C=Two_of_Three_Reports_Valid

D=Own_Tracked_Alt

E=Own_Tracked_Alt_Rate

F=Other_Tracked_Alt

G=Alt_Layer_Value

H=Up_Separation

I=Down_Separation

J=Other_RAC

K=Other_Capability

L=Climb_Inhibit


| A   | B | C | D | E | F | G | H   | I   | J | K | L |
|-----|---|---|---|---|---|---|-----|-----|---|---|---|
| 700 | 1 | 1 | 0 | 1 | 1 | 0 | 500 | 100 | 0 | 0 | 0 |
| 700 | 1 | 1 | 1 | 1 | 0 | 1 | 500 | 100 | 1 | 1 | 1 |
| 700 | 1 | 1 | 1 | 1 | 0 | 2 | 100 | 500 | 0 | 0 | 0 |
| 700 | 1 | 1 | 1 | 1 | 0 | 3 | 100 | 500 | 0 | 0 | 0 |
| 50  | 1 | 1 | 1 | 1 | 0 | 3 | 100 | 500 | 1 | 1 | 1 |

### Results


```bash

File 'tcas.c'
Lines executed:94.17% of 120
Branches executed:100.00% of 74
Taken at least once:75.68% of 74
Calls executed:90.48% of 63
Creating 'tcas.c.gcov'

Lines executed:94.17% of 120


```

### Analysis

It is not possible to satisfy 100% predicate coverage, since `need_upward_RA` and `need_downward_RA` will never both be true; we can never take this branch. Creating this
test suite was challenging because of all of the nested conditions that caused reachability issues. It was not enough to simply satisfy the given condition; we had to
make sure that we were able to reach the necessary branches. Another issue was mutability; since some of the variables are mutated once the program is run, it
made it even more difficult to track the behavior that tweaking each input would
have.

## Active Clause Coverage

1) `result = !(Own_Below_Threat()) || ((Own_Below_Threat()) && (!(Down_Separation >= ALIM())));`
=>  !A | (A & !(B))

| Row# |   | A | B |   | P |   | PA | PB |
|------|---|---|---|---|---|---|----|----|
| 1    |   | T | T |   |   |   | T  | T  |
| 2    |   | T |   |   | T |   |    | T  |
| 3    |   |   | T |   | T |   | T  |    |
| 4    |   |   |   |   | T |   |    |    |

| Major Clause | Set of possible tests |
|--------------|-----------------------|
| A            | (1,3)                 |
| B            | (1,2)                 |

input: (T, T) 700 1 1 0 1 1 0 60000 34567 0 0 34568

input: (T, F) 700 1 1 0 1 1 0 500 100 0 0 0

input: (F, T) 700 1 1 3 1 1 0 60000 34567 0 0 34568


2) `result = Own_Above_Threat() && (Cur_Vertical_Sep >= 300 ) && (Up_Separation >= ALIM());`
=> A & B & C

| Row# |   | A | B | C |   | P |   | PA | PB | PC |
|------|---|---|---|---|---|---|---|----|----|----|
| 1    |   | T | T | T |   | T |   | T  | T  | T  |
| 2    |   | T | T |   |   |   |   |    |    | T  |
| 3    |   | T |   | T |   |   |   |    | T  |    |
| 4    |   | T |   |   |   |   |   |    |    |    |
| 5    |   |   | T | T |   |   |   | T  |    |    |
| 6    |   |   | T |   |   |   |   |    |    |    |
| 7    |   |   |   | T |   |   |   |    |    |    |
| 8    |   |   |   |   |   |   |   |    |    |    |

| Major Clause | Set of possible tests |
|--------------|-----------------------|
|              |                       |
| A            | (1,5)                 |
| B            | (1,3)                 |
| C            | (1,2)                 |

input: (T, T, T) 700 1 1 1 1 0 3 100 500 0 0 0

input: (T, T, F) 700 1 1 1 1 0 3 -1 500 0 0 0

input: (T, F, T) =><=, `enabled` must be true to reach this condition, which requires `Cur_Vertical_Sep > 600`

input: (F, T, T) 700 1 1 -1 1 0 3 100 500 0 0 0

3) `result = Own_Below_Threat() && (Cur_Vertical_Sep >= 300) && (Down_Separation >= ALIM());`
=> A & B & C

| Row# |   | A | B | C |   | P |   | PA | PB | PC |
|------|---|---|---|---|---|---|---|----|----|----|
| 1    |   | T | T | T |   | T |   | T  | T  | T  |
| 2    |   | T | T |   |   |   |   |    |    | T  |
| 3    |   | T |   | T |   |   |   |    | T  |    |
| 4    |   | T |   |   |   |   |   |    |    |    |
| 5    |   |   | T | T |   |   |   | T  |    |    |
| 6    |   |   | T |   |   |   |   |    |    |    |
| 7    |   |   |   | T |   |   |   |    |    |    |
| 8    |   |   |   |   |   |   |   |    |    |    |

| Major Clause | Set of possible tests |
|--------------|-----------------------|
|              |                       |
| A            | (1,5)                 |
| B            | (1,3)                 |
| C            | (1,2)                 |

input: (T, T, T) 0 1 1 0 1 1 0 60000 34567 0 0 34568

input: (T, T, F) 700 1 1 0 1 1 0 500 100 0 0 0

input: (T, F, T) =><=, `enabled` must be true to reach this condition, which requires `Cur_Vertical_Sep > 600`

input: (F, T, T) 700 1 1 3 1 1 0 60000 34567 0 0 34568

4) `result = !(Own_Above_Threat()) || ((Own_Above_Threat()) && (Up_Separation >= ALIM()));`
=> !A | (A & B)

| Row# |   | A | B |   | P |   | PA | PB |
|------|---|---|---|---|---|---|----|----|
| 1    |   | T | T |   | T |   |    | T  |
| 2    |   | T |   |   |   |   | T  | T  |
| 3    |   |   | T |   | T |   |    |    |
| 4    |   |   |   |   | T |   | T  |    |

| Major Clause | Set of possible tests |
|--------------|-----------------------|
|              |                       |
| A            | (2,4)                 |
| B            | (1,2)                 |

input: (T, T) 700 1 1 1 1 0 3 100 500 0 0 0

input: (T, F) 700 1 1 1 1 0 3 -1 500 0 0 0

input: (F, T) 700 1 1 -1 1 0 3 100 500 0 0 0

5) `enabled = High_Confidence && (Own_Tracked_Alt_Rate <= 600) && (Cur_Vertical_Sep > 600);`
=> A & B & C

| Row# |   | A | B | C |   | P |   | PA | PB | PC |
|------|---|---|---|---|---|---|---|----|----|----|
| 1    |   | T | T | T |   | T |   | T  | T  | T  |
| 2    |   | T | T |   |   |   |   |    |    | T  |
| 3    |   | T |   | T |   |   |   |    | T  |    |
| 4    |   | T |   |   |   |   |   |    |    |    |
| 5    |   |   | T | T |   |   |   | T  |    |    |
| 6    |   |   | T |   |   |   |   |    |    |    |
| 7    |   |   |   | T |   |   |   |    |    |    |
| 8    |   |   |   |   |   |   |   |    |    |    |

| Major Clause | Set of possible tests |
|--------------|-----------------------|
|              |                       |
| A            | (1,5)                 |
| B            | (1,3)                 |
| C            | (1,2)                 |

input: (T, T, T) 700 1 1 3 1 1 0 60000 34567 0 0 34568

input: (T, T, F) 0 1 1 0 1 1 0 60000 34567 0 0 34568

input: (T, F, T) 700 1 1 700 700 1 0 60000 34567 0 0 34568

input: (F, T, T) 700 0 1 3 1 1 0 60000 34567 0 0 34568

6) `intent_not_known = Two_of_Three_Reports_Valid && Other_RAC == 0 ;`
=> A & B

| Row# |   | A | B |   | P |   | PA | PB |
|------|---|---|---|---|---|---|----|----|
| 1    |   | T | T |   | T |   | T  | T  |
| 2    |   | T |   |   |   |   |    | T  |
| 3    |   |   | T |   |   |   | T  |    |
| 4    |   |   |   |   |   |   |    |    |

| Major Clause | Set of possible tests |
|--------------|-----------------------|
|              |                       |
| A            | (1,3)                 |
| B            | (1,2)                 |

input: (T, T) 700 0 1 3 1 1 0 60000 34567 0 0 34568

input: (T, F) 50 1 1 1 1 0 3 100 500 1 1 1

input: (F, T) 700 0 0 3 1 1 0 60000 34567 0 0 34568

7) `need_upward_RA = Non_Crossing_Biased_Climb() && Own_Below_Threat() ;`
=> A & B

| Row# |   | A | B |   | P |   | PA | PB |
|------|---|---|---|---|---|---|----|----|
| 1    |   | T | T |   | T |   | T  | T  |
| 2    |   | T |   |   |   |   |    | T  |
| 3    |   |   | T |   |   |   | T  |    |
| 4    |   |   |   |   |   |   |    |    |

| Major Clause | Set of possible tests |
|--------------|-----------------------|
|              |                       |
| A            | (1,3)                 |
| B            | (1,2)                 |


input: (T, T) 700 1 1 0 1 1 0 500 100 0 0 0

input: (T, F) 700 1 1 3 1 1 0 60000 34567 0 0 34568

input: (F, T) 700 1 1 -1 1 0 3 100 500 0 0 0


8) `need_downward_RA = Non_Crossing_Biased_Descend() && Own_Above_Threat();`
=> A & B

| Row# |   | A | B |   | P |   | PA | PB |
|------|---|---|---|---|---|---|----|----|
| 1    |   | T | T |   | T |   | T  | T  |
| 2    |   | T |   |   |   |   |    | T  |
| 3    |   |   | T |   |   |   | T  |    |
| 4    |   |   |   |   |   |   |    |    |

| Major Clause | Set of possible tests |
|--------------|-----------------------|
|              |                       |
| A            | (1,3)                 |
| B            | (1,2)                 |

input: (T, T) 700 1 1 1 1 0 3 100 500 0 0 0

input: (F, T) 700 1 1 3 1 1 0 60000 34567 0 0 34568

input: (T, F) 700 1 1 -1 1 0 3 100 500 0 0 0

9) `(enabled && ((tcas_equipped && intent_not_known) || !tcas_equipped)`
=> A & (( B & C ) | !(B))

| Row# |   | A | B | C |   | P |   | PA | PB | PC |
|------|---|---|---|---|---|---|---|----|----|----|
| 1    |   | T | T | T |   | T |   | T  |    | T  |
| 2    |   | T | T |   |   |   |   |    | T  | T  |
| 3    |   | T |   | T |   | T |   | T  |    |    |
| 4    |   | T |   |   |   | T |   | T  | T  |    |
| 5    |   |   | T | T |   |   |   | T  |    |    |
| 6    |   |   | T |   |   |   |   |    |    |    |
| 7    |   |   |   | T |   |   |   | T  |    |    |
| 8    |   |   |   |   |   |   |   | T  |    |    |

| Major Clause | Set of possible tests                                         |
|--------------|---------------------------------------------------------------|
|              |                                                               |
| A            | (1,5), (1,7), (1,8), (3,5), (3,7), (3,8), (4,5), (4,7), (4,8) |
| B            | (2,4)                                                         |
| C            | (1,2)                                                         |

input: (T, F, T) 700 1 1 -1 1 0 3 100 500 0 0 0

input: (F, T, T) 0 1 1 0 1 1 0 60000 34567 0 1 34568

input: (T, T, F) 700 1 1 1 1 0 1 500 100 1 1 1

input: (T, F, F) 700 1 1 -1 1 0 3 100 500 1 -1 0

### Results


```bash

gcov -b tcas.exec-tcas.gcno
File 'tcas.c'
Lines executed:92.31% of 91
Branches executed:100.00% of 74
Taken at least once:89.19% of 74
Calls executed:87.23% of 47
Creating 'tcas.c.gcov'


```

Note that "Lines executed" seems to have dropped, but this is due to extra instrumentation required by ACC.

### Analysis

It was not possible to satisfy ACC either, since major clauses for some conditions
generated possible tests that could not be satisfied. See (2) and (3) for examples of this. This test suite was even more challenging to create because reachability became
more difficult when we had to satisfy ACC. Additionally, mutability hurt us here as well. However, it was trivial to construct test cases for the predicates with single clauses since ACC collapses into predicate coverage in these cases, and they have been worked out above; for this reason, they have not been included the ACC section.
