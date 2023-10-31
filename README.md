# SIMPLI-field

**SIMPLI-field** is a physics-inspired automated ML framework for in-cylinder engine flow field prediction from the work  *"Swirl-induced Motion Prediction with Learning and Inspirations from In-cylinder Flow Field Structure"* (Under Review). It is empowered by AutoGluon v0.8.2 and realized in Python. "SIMPLI-field" is capable to deal with extremely complicated in-cylinder flow field with very high prediction accuracy, suggesting the idea that a better incorporation between spatial and temporal information could work well on simple machine learning models compared with large, complicated deep neural networks. 

The source code for ML our model training, prediction, and distillation is published in this GitHub repo. If you are interested to further expand our idea on other flow dataset, please cite our coming paper. 
License: GNU General Public License v3.0

## Engine Parameters

| Category                     | Value                          |
| ---------------------------- | ------------------------------ |
| Engine  speed [rpm]          | 800                            |
| Bore  [mm]                   | 86                             |
| Stroke  [mm]                 | 94.6                           |
| Clearance  volume [cm3]      | 49.96                          |
| Displacement  [cm3]          | 549.51                         |
| Intake  Valve Open [º ATDC]  | -362/-362  (Primary/Secondary) |
| Intake  Valve Close [º ATDC] | -144/-132  (Primary/Secondary) |
| Exhaust  Valve Open [º ATDC] | 131                            |
| Exhaust Valve Close [º ATDC] | 372                            |

CAD: Crank Angle Degree

ATDC: After Top Dead Center

## Computational Resources

| **Item**                        | **Value**                  |
| ------------------------------- | -------------------------- |
| CPU                             | Intel  i9-13900K           |
| #  Cores                        | 24  (8 P-core + 16 E-core) |
| #  Threads                      | 32                         |
| Peak  Memory Usage              | 252.8MB                    |
| Total  Training Time            | ≈25 hours                  |
| Prediction  Time per Flow Field | ≈45 seconds                |

## Repo Guidelines

### Training

Training source code arranged to Python Jupyter Notebook: 

```
./Training-Revised-Edition.ipynb
```

Complete training data and well-trained ML models are published but could be available on request.

### Prediction

Training source code arranged to Python Jupyter Notebook: 

```
./Prediction-Revised-Edition.ipynb
```

### Distillation

Since we are using ensemble learning algorithm, the distillation process could select well-performed meta-model during the model stacking process. This process could help trim down the size of the model and improve prediction efficiency.

 Training source code arranged to Python Jupyter Notebook: 

```
./Distillation.ipynb
```

### Dataset

| Item             | Value                                                        |
| ---------------- | ------------------------------------------------------------ |
| Swirl Ratio      | High = 5.68                                                  |
|                  | Medium = 1.33                                                |
|                  | Low = 0.55                                                   |
| # Cycle          | 100 : 1~100, {70,80,90} published in the repo                |
| CAD Range        | -300 CAD (intake) ~ -60 CAD (late compression)               |
| Training Dataset | Low SR, Cycle = {1,2,..,9,11,...,19,21,...,91,...99}, # Cycle = 90 |
| Test Dataset     | Low SR, Cycle = {10, 20, ..., 90}, # Cycle = 10              |
|                  | Medium SR, Cycle = {10, 20, ..., 90}, # Cycle = 10           |
|                  | High SR, Cycle = {10, 20, ..., 90}, # Cycle = 10             |

**Note:** we only publish cycle 70, 80, 90  for result validation. Other data could be made available on request. It is also encouraging to test the SIMPLI-field on other flow field scenario.

### Result

The result of Cycle 70, 80, 90 for three swirl ratio conditions are published. Each cycle contains the result consecutively predicted from -300 CAD to -60 CAD. For each prediction result we present:

* x/y: the raw data from the experiment (e.g. "2-raw.dat") and simulation (e.g. "2.dat");
* SI: the structural index evaluation of data
* MI: the magnitude index evaluation of data
* Raw: Input-output comparison. The flow field on the left is the input flow field and that on the right is the output. 

Note: The red vectors come from prediction and green vectors come from experiments.

Examples:

./result/sr_C6_01/Cycle-090/-260CAD_ATDC/SI/2.png
![SI](https://github.com/ziming-zh/SIMPLI-field/blob/main/result/sr_C6_01/Cycle-090/-260CAD_ATDC/SI/2.png?raw=true)

./result/sr_C6_01/Cycle-090/-260CAD_ATDC/MI/2.png
![MI](https://github.com/ziming-zh/SIMPLI-field/blob/main/result/sr_C6_01/Cycle-090/-260CAD_ATDC/MI/2.png?raw=true)

./result/sr_C6_01/Cycle-090/-260CAD_ATDC/Raw/2.png
![MI](https://github.com/ziming-zh/SIMPLI-field/blob/main/result/sr_C6_01/Cycle-090/-260CAD_ATDC/Raw/2.png?raw=true)
