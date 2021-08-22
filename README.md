*NOTE:* This file is a template that you can use to create the README for your project. The *TODO* comments below will highlight the information you should be sure to include.
test
# Your Project Title Here

*TODO:* Write a short introduction to your project.

## Project Set Up and Installation
*OPTIONAL:* If your project has any special installation steps, this is where you should put it. To turn this project into a professional portfolio project, you are encouraged to explain how to set up this project in AzureML.

## Dataset

### Overview
*TODO*: Explain about the data you are using and where you got it from.
I chose the dataset of [Heart Failure records from Kaggle](https://www.kaggle.com/andrewmvd/heart-failure-clinical-data) because it has a high usability score of 10 meaning that the dataset is easy to understand, machine readable, includes essential metadata and is maintained. It is also a very interesting topic. According to Kaggle, Cardiovascular diseases (CVDs) are the number 1 cause of death globally, accounting for 31% of all deaths worlwide. 

Environmental and behavioural risk factors such as tobacco use, unhealthy diet and obesity, physical inactivity and harmful use of alcohol could be used as features for estimation models. Being able to estimate the probability of developping a CVD could be of great help for high risk people.

The Dataset is tabular with 13 columns (12 features and 1 target variable) and contains 299 rows.
kaggle datasets download -d andrewmvd/heart-failure-clinical-data
### Task
*TODO*: Explain the task you are going to be solving with this dataset and the features you will be using for it.
The task I am trying to solve is to generate a model that predicts if a person might have a heart failure or not. I will be looking at the following features:

|    | Variable name             | Type            | Description                                               | Example           |
|----|---------------------------|-----------------|-----------------------------------------------------------|-------------------|
| 1  | age                       | numerical       | age of the patient                                        | 25                |
| 2  | anaemia                   | boolean         | Decrease of red blood cells or hemoglobin                 | 0 or 1            |
| 3  | creatinine_phosphokinase  | numerical       | Level of the CPK enzyme in the blood                      | 542               |
| 4  | diabetes                  | boolean         | If the patient has diabetes                               | university.degree |
| 5  | ejection_fraction         | numerical       | Percentage of blood leaving the heart at each contraction | 45                |
| 6  | high_blood_pressure       | boolean         | If the patient has hypertension                           | 0 or 1            |
| 7  | platelets                 | numerical       | Platelets in the blood                                    | 149000            |
| 8  | serum_creatinine          | numerical       | Level of serum creatinine in the blood                    | 0.5               |
| 9  | serum_sodium              | numerical       | Level of serum sodium in the blood                        | jun               |
| 10 | sex                       | boolean         | Woman or man                                              | 0 or 1            |
| 11 | smoking                   | boolean         | If the patient smokes                                     | 285               |
| 12 | time                      | numerical       | follow-up period (days)                                   | 4                 |
|----|---------------------------|-----------------|-----------------------------------------------------------|-------------------|
| 21 | DEATH_EVENT [Target]      | boolean         | if the patient deceased during the follow-up period       | 0 or 1            |

### Access
*TODO*: Explain how you are accessing the data in your workspace.
The are several ways to access the data in the workspace. Once the data is uploaded to Azure ML, we can access it through the key we gave it. Here my dataset `key = 'heart_failure_records'`, so I can retrieve the dataset using the following command:
`dataset = ws.datasets[key] `

Once the dataset is loaded, I can use it as a pandas dataframe for further exploration.
## Automated ML
*TODO*: Give an overview of the `automl` settings and configuration you used for this experiment
Here are the automl settings I choose:
```python
automl_settings = {
    "experiment_timeout_minutes": 20,
    "max_concurrent_iterations": 5,
    "primary_metric" : 'accuracy'
}
```

| Parameter | Description | Value |
|-----------|-------------|-------|
| experiment_timeout_minutes | The maximum amount of time (in minutes) that the experiment is allowed to run before it is automatically stopped and results are automatically made available. | 20 |
| max_concurrent_iterations | The maximum number of concurrent training iterations allowed for the experiment. | 5 |
| primary_metric | The primary metric used to determine the experiment's status. | accuracy |

Here is the automl config I choose:

```python
automl_config = AutoMLConfig(
    compute_target=compute_target,
    task='classification',
    training_data=dataset,
    label_column_name='DEATH_EVENT',
    enable_early_stopping= True,
    featurization= 'auto',
    debug_log = "automl_errors.log",
    n_cross_validations=5,
    **automl_settings
)
```
| Parameter | Description | Value |
|-----------|-------------|-------|
| compute_target | The compute instance that will run the job | compute_target |
| task | The type of task to be solved. | classification |
| training_data | The dataset to be used for training. | dataset |
| label_column_name | The name of the column containing the label. | DEATH_EVENT |
| enable_early_stopping | Enable early stopping. | True |
| featurization | The featurization method to be used. | auto |
| debug_log | The path to the log file. | automl_errors.log |
| n_cross_validations | The number of cross-validations to be performed. | 5 |

### Results
*TODO*: What are the results you got with your automated ML model? What were the parameters of the model? How could you have improved it?

*TODO* Remeber to provide screenshots of the `RunDetails` widget as well as a screenshot of the best model trained with it's parameters.

## Hyperparameter Tuning
*TODO*: What kind of model did you choose for this experiment and why? Give an overview of the types of parameters and their ranges used for the hyperparameter search


### Results
*TODO*: What are the results you got with your model? What were the parameters of the model? How could you have improved it?

*TODO* Remeber to provide screenshots of the `RunDetails` widget as well as a screenshot of the best model trained with it's parameters.

## Model Deployment
*TODO*: Give an overview of the deployed model and instructions on how to query the endpoint with a sample input.

## Screen Recording
*TODO* Provide a link to a screen recording of the project in action. Remember that the screencast should demonstrate:
- A working model
- Demo of the deployed  model
- Demo of a sample request sent to the endpoint and its response

## Standout Suggestions
*TODO (Optional):* This is where you can provide information about any standout suggestions that you have attempted.
test