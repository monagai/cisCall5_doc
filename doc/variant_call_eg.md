# Variant call example

In this section, a cisCall Muton benchmark assessment with a GATK MuTect2 was conducted.

## Test Data

For the benchmarking, cisCall muton and MuTect2 were executed with following sequence data:

|                      | Normal                        | Tumor                 |
| :-:                  | :-:                           | :-:                   |
| sample               | HCC-78 (Human lung carcinoma) | Lung cancer cell line |
| File size R1/R2 (GB) | 6.1/6.3                       | 1.5/1.5               |
| Read number          | 74,962,014                    | 19,339,651            |

## Mutation call

Execute cisCall and MuTect2 with default parameter settings.

## Results Comparison

|                | cisCall | MuTect2 |
| ---            | ---     | ---     |
| Total hit      | -       | 1364    |
| Passed Filters | 9       | 227     |
|                |         |         |
| **SNVs**       | 9       | 227     |
| **Insertions** | 0       | 0       |
| **Deletions**  | 0       | 0       |
