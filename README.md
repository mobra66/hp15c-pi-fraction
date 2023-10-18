# Pi Fraction Approximation for HP-15C
Find a fraction which approximates Pi to a given limit.
Uses registers 1 and 2 for numerator and demoninator. Register 3 is the delta between Pi and the fraction.
Register 4 must be set by the user before running the program, it is the target limit accuracy, e.g. 1E-05.

Tested using HP-15C Collector's Edition.

| Label  | Instruction | Code     | Comment                                                    |
| ------ | ----------- | -------- | ---------------------------------------------------------- |
|        |             |          | Initialize limit in reg 4 to e.g. 0.00001                  |
| LBL A  |             | 41.21.11 |                                                            |
|        | 1           | 1        |                                                            |
|        | STO 1       | 44 1     |                                                            |
|        | STO 2       | 44 2     |                                                            |
|        | STO 3       | 44 3     |                                                            |
| LBL .1 |             | 42.21.,1 |                                                            |
|        | RCL 3       | 45 3     |                                                            |
|        | X>0?        | 43.30.1  | Sign of delta determines if fraction is too high or low    |
|        | GTO .2      | 22 ,2    |                                                            |
|        | 1           | 1        |                                                            |
|        | STO+ 2      | 44.40.2  | Incerement denominator                                     |
|        | GTO .3      | 22 ,3    |                                                            |
| LBL .2 |             | 42.21.,2 |                                                            |
|        | 1           | 1        |                                                            |
|        | STO+ 1      | 44.40.1  | Increment numerator                                        |
| LBL .3 |             | 42.21.,3 |                                                            |
|        | PI          | 43 26    |                                                            |
|        | RCL 1       | 45 1     |                                                            |
|        | RCL 2       | 45 2     |                                                            |
|        | /           | 10       |                                                            |
|        | -           | 30       |                                                            |
|        | STO 3       | 44 3     |                                                            |
|        | ABS         | 43 16    | X := abs ( PI - numerator / denominator )                  |
|        | RCL 4       | 45 4     |                                                            |
|        | X<=Y?       | 43 10    | End loop when delta is less than limit in reg 4            |
|        | GTO .1      | 22 ,1    |                                                            |
|        | RCL 1       | 45 1     | Display result numerator                                   |
|        | PSE         | 42 31    |                                                            |
|        | RCL 2       | 45 2     | Display result denominator                                 |
|        | RTN         | 43 32    |
