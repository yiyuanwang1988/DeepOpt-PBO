# DeepOpt-PBO-v1

## Compilation

g++ pms.cpp -static -O3 -o Deepoptv1

## Code execution command

./Deepoptv1 <input_file.wecnf> <cutoff_time> <seed> <input_file.opb>

- input_file.wecnf is a PBO instance encoded into .wecnf file format.
- input_file.opb is a PBO instance encoded into .opb file format.
- The purpose of the fourth parameter ,input_file.opb ,is to extract the objective function of the .opb file to obtain the true objective function value by substituting the solution, i.e., the assignment of PBO instance into the objective function.

## How to convert .opb file to .wecnf file

Files with the ".wecnf" extension are DeepOpt-PBO-v1's standard input files that can be converted from .opb files.

Example: test.opb
minimize the objective functin :  8x1 + 4x2 + x3
subject to :                      1x1 + 2(-x2) + 3x3 >= 2

convert to test.wecnf :
								p wcnf 3 4 14         // p wcnf number_vars number_constrains top
								14 2 1 1 2 -2 3 3 0   // 1x1 + 2(-x2) + 3x3 >= 2
								8 1 1 -1 0
								4 1 1 -2 0
								1 1 1 -3 0
								
- First, record the sum of the literal coefficients of the objective function: sum = 8 + 4 + 1 = 13,
  "top = sum + 1 =  14" is used to distinguish between hard and soft clauses;
- The parameters line is "p wcnf nbvar nbconst top". Each constraint has a weight, which is the first integer in the constraint. 
  Weights must be greater than or equal to 1, and smaller than 2^63. The sum of the weights must be less than 2^64-1. 
  Hard constraints have weight "top" and soft constraints have a weight smaller than "top". "top" will always be greater than the sum of the soft clause weights. 
- The second num of each constraint is the degree of the constraint followed by the coefficient of literal and literal itself. 
  Each constraint must end with '0'. Constraint: <weight> <degree> <coeff> <lit> ... <coeff> <lit> 0

## Citation

[1]Wenbo Zhou, Yujiao Zhao, Yiyuan Wang, Shaowei Cai, Shimao Wang, Xinyu Wang, Minghao Yin: Improving Local Search for Pseudo Boolean Optimization by Fragile Scoring Function and Deep Optimization. CP 2023: 41:1-41:18

[2]Zhendong Lei, Shaowei Cai, Chuan Luo, Holger H. Hoos: Efficient Local Search for Pseudo Boolean Optimization. SAT 2021: 332-348





