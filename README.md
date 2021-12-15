# Simulation Based What-If Analysis of COVID-19 Spread in Universities

#### Kara Rofe, Talia Seshaiah, Yifan Zhao


## Application 

This project was based off the article *"Simulation-based what if-analysis for controlling the spread of COVID-19 in universities"* (Ghaffarzadegan, 2021). 

Our project uses a SEIR-model framework to look at the transmission of COVID-19 among both students and faculty among Ivy League universities. SEIR (Susceptible, Exposed, Infected, Recovered) models are often used for diseases, and can help with understanding disease dynamics. 

- S: susceptible individuals (those who able to contract the disease)
- E: exposed individuals (those who have been exposed/infected)
- I: infectious individuals (those who can transmit the disease)
- R: recovered individuals (those who have recovered from the disease)


## Variables
<img src="https://github.com/taliajs/php2560final/blob/main/parameter-table.PNG">

## Simulation 


### Main Functions

There is one main function for this simulation - `simfunc`. 


### Equations

The equations used were based on Equations 3,4,6, and 8 from the article (the equations are simplified), and represent the transmission dynamics
- <img src="https://latex.codecogs.com/svg.image?\frac{dS}{dt}&space;=&space;-&space;i_N&space;C\frac{S}{N}(\mu&space;E&plus;\alpha&space;I)&plus;A_s&space;-&space;L_s" title="\frac{dS}{dt} = - i_N C\frac{S}{N}(\mu E+\alpha I)+A_s - L_s" />  (Equation 3)

- <img src="https://latex.codecogs.com/svg.image?\frac{dE}{dt}&space;=&space;i_N&space;C\frac{S}{N}(\mu&space;E&plus;\alpha&space;I)&space;-&space;\frac{E}{\tau_1}&space;&plus;A_E&space;-&space;L_E" title="\frac{dE}{dt} = i_N C\frac{S}{N}(\mu E+\alpha I) - \frac{E}{\tau_1} +A_E - L_E" />  (Equation 4)

- <img src="https://latex.codecogs.com/svg.image?\frac{dI}{dt}&space;=&space;\frac{E}{\tau_1}-\frac{I}{\tau_2}-L_I" title="\frac{dI}{dt} = \frac{E}{\tau_1}-\frac{I}{\tau_2}-L_I" />  (Equation 6)

- <img src="https://latex.codecogs.com/svg.image?\frac{dR}{dt}&space;=&space;\frac{I}{\tau_2}-L_R" title="\frac{dR}{dt} = \frac{I}{\tau_2}-L_R" />  (Equation 8)
- dS/dt represents the rate of change in susceptible population. It is calculated as the incoming susceptible student population (A_s) minus the leaving susceptible students (L_x) minus the population that is already exposed to the disease (first component in the equation). mu*E + alpha*I is the effective population that could transmit the disease. The transmission rate is affected by the infection probability (i_N) and contact rate C.
  -  Contact Rate C is subject to change over time. It is related to students' sensitivity to the disease and rolling average of COVID cases. Defined as:
      - <img src="https://latex.codecogs.com/svg.image?C=C_{max}W_N" title="C=C_{max}W_N" />
      -    <img src="https://latex.codecogs.com/svg.image?W_N&space;=&space;exp(-h(\frac{Rolling&space;Avg}{N}))" title="W_N = exp(-h(\frac{Rolling Avg}{N}))" /> (Equation 17)   
- dE/dt represents the rate of change in exposed population. It takes in the exposed population and arrival exposed students (A_E) and subtracts the leaving exposed students (L_E) and population that is already infected (E/tau_1)
- dI/dt represents the rate of change in infected population. It is calculated as incoming infected population minus the leaving infected students (L_I) and recovered population (I/tau_2)
- dR/dt represents the rate of change in recovered population. It is the newly recovered population (I/tau_2) minus the leaving recovered students (L_R)

### Parameter Descriptions
- **Arrival rate of students:** 
  - Changes initial population of susceptible. When users select an Ivy League from the drop-down, the arrival rate is changed to that specific university

- **Constant contact rate:** 
  - The maximum contact rate (person/day) possible. 

- **infection probability:**
  - Affect rate of transmission/infection

- **Student Sensitivity to COVID:**
  - Students' sensitivity to the disease and rolling average of COVID cases. It affects the Contact Rate, which is subject to change over time. 

- **University Closure Decision:**
  - 1: University starts to evacuate students. 0: University operates as normal. It affects the leaving rate of students. e.g. When set to 1, students leave campus at certain rate.


## Shiny App 

[Link to app](https://taliajs.shinyapps.io/seir_covid_model/)

When the app is first run, it shows a single run of this model using default parameters. Users can look at the transmission of COVID-19 among students and faculty for different universities, by selecting an Ivy League school and changing the model parameters. When users select an Ivy League, the arrival rate is changed to that specific university. Users can learn more about the inputs by clicking on the `Information about Inputs` button on the App.

**School Data**
- Fall 2020 student to faculty ratios were used. 
- All data came from Common Data Sets(CDS)
- Only using full-time equivalent students and full-time instructional faculty (no TAs)


The tab `Daily cases` shows the daily cases of COVID-19 for exposed and infected individuals, with min, max and average contact rate listed below. 

The tab `Cumulative cases` shows the cumulative cases of COVID-19 over time. 

The `Summary` table shows the statistics for contact rate for specific variables.



### Sources
- Ghaffarzadegan N (2021) Simulation-based what-if analysis for controlling the spread of Covid-19 in universities. PLoS ONE 16(2): e0246323. https://doi.org/10.1371/journal.pone.0246323

- https://sites.me.ucsb.edu/~moehlis/APC514/tutorials/tutorial_seasonal/node4.html
