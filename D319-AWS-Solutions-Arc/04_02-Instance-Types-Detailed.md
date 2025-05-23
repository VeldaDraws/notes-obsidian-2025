![[type_1.jpg]]
![[type_2.jpg]]
## Current generation instances (2025)
- [General purpose:](https://docs.aws.amazon.com/ec2/latest/instancetypes/gp.html) 
	- #### M5, M6, M7, M8, Mac, T2, T3, T4
		- `M5 | M5a | M5ad | M5d | M5dn | M5n | M5zn` 
		- `M6a | M6g | M6gd | M6i | M6id | M6idn | M6in` 
		- `M7a | M7g | M7gd | M7i | M7i-flex `
		- `M8g | M8gd` 
		- `Mac1 | Mac2 | Mac2-m1ultra | Mac2-m2 | Mac2-m2pro` 
		- `T2 | T3 | T3a | T4g`
	- Provides a balance of compute, memory, and networking resources.
	- The T instance family is also referred to as burstable performance instances.
- [Compute optimized:](https://docs.aws.amazon.com/ec2/latest/instancetypes/co.html)
	- #### C5, C6, C7, C8
		- `C5 | C5a | C5ad | C5d | C5n `
		- `C6a | C6g | C6gd | C6gn | C6i | C6id | C6in` 
		- `C7a | C7g | C7gd | C7gn | C7i | C7i-flex` 
		- `C8g | C8gd`
	- Designed for compute intensive applications that benefit from high performance processors.
- [Memory optimized:](https://docs.aws.amazon.com/ec2/latest/instancetypes/mo.html) 
	- #### R5, R6, R7, R8, U~, X~, z1d
		- `R5 | R5a | R5ad | R5b | R5d | R5dn | R5n` 
		- `R6a | R6g | R6gd | R6i | R6idn | R6in | R6id` 
		- `R7a | R7g | R7gd | R7i | R7iz` 
		- `R8g | R8gd` 
		- `U-3tb1 | U-6tb1 | U-9tb1 | U-12tb1 | U-18tb1 | U-24tb1 | U7i-6tb | U7i-8tb | U7i-12tb | U7in-16tb | U7in-24tb | U7in-32tb | U7inh-32tb` 
		- `X1 | X1e | X2gd | X2idn | X2iedn | X2iezn | X8g | z1d`
	- Designed to deliver fast performance for workloads that process large data sets in memory.
- [Storage optimized:](https://docs.aws.amazon.com/ec2/latest/instancetypes/so.html) 
	- #### D2, D3, H1, I~
		- `D2 | D3 | D3en` 
		- `H1` 
		- `I3 | I3en | I4g | I4i | I7i | I7ie | I8g | Im4gn | Is4gen`
	- Designed for workloads that require high, sequential read and write access to very large data sets on local storage.
- [Accelerated computing:](https://docs.aws.amazon.com/ec2/latest/instancetypes/ac.html) 
	- #### DL~, F1, F2, G~, Inf~, P~, Trn~, VT1
		- `DL1 | DL2q` 
		- `F1 | F2` 
		- `G4ad | G4dn | G5 | G5g | G6 | G6e | Gr6` 
		- `Inf1 | Inf2` 
		- `P3 | P3dn | P4d | P4de | P5 | P5e | P5en` 
		- `Trn1 | Trn1n | Trn2 | Trn2u` 
		- `VT1`
- [High-performance computing:](https://docs.aws.amazon.com/ec2/latest/instancetypes/hpc.html) 
	- #### HPC~
		- `Hpc6a | Hpc6id | Hpc7a | Hpc7g`

#### Previous Generation
AWS offers previous generation instance types for users who have optimized their applications around them and have yet to upgrade. Use of current generation is encouraged.
- **General purpose**: A1 | M1 | M2 | M3 | M4 | T1
- **Compute optimized**: C1 | C3 | C4
- **Memory optimized**: R3 | R4
- **Storage optimized**: I2
- **Accelerated computing**: G3