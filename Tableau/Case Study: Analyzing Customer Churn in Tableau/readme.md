# Data Analysis in Tableau

## Tableau analysis process
- Perform a datacheck.
- Ask different business questions and explore the data.
- Discover insights and visualize them using a fitting visualization.
- Build a dashboard or story so you can cohesively share the information.
- Organize a session with stakeholders and walk them through the dashboard or story.


![image](https://user-images.githubusercontent.com/92245436/148038908-765537c9-0650-4d45-9012-cf51b4197db3.png)



## The problem 
Solving customer churn
- A fictitious data set about churn from a Telecom provider(Databel).
- Your task: discover why customers are churning.

### Churn
The **Churn rate**, also known as the rate of *attrition* or *customer churn*, is the rate at which customer stop doing busines with an entity.
- Keeping customer is easier than getting new customer
- Reducing churn is a priority for mant companies
- Leaky bucket Problem 

![image](https://user-images.githubusercontent.com/92245436/148040082-34a9d3a1-9f70-4bc7-9006-ebeff249337c.png)

#### Calculating Churn 
`Churn rate = customer lost / total number of customer `

### The data 
Key characteristics 
- Databel, a fctitious Telecom provider 
- One big table containing 29 columns
- One row per customer 
- Snapshot of the database at a specic moment in time

#### [Metadata](https://assets.datacamp.com/production/repositories/5952/datasets/060f0299a782a1bdb3fd21a801a58b03190c4163/Metadata%20-%20Case%20study_%20Analyzing%20customer%20churn%20in%20Tableau.pdf)

## 1. Exploratory Analysis
### Data Check 
The first step in any analysis is doing a data check. Lets check count of customer Ids and count of unique cutomer ids.
- Number of Customers - 6687
- Number of Unique Customers - 6687  <br>
We have all Unique customers 

### Calculate Churn Rate
We have to convert Churn Label that indicates **"Yes"** or **"No"** to a binomial coloumn that will contain a **1** or **0**, indicating If the customer churned or not, and use that table to calculate churn rate. <br>
**Churn rate = Number of Churned customers / Number of Customers** <br>
`Churn rate = 26.86`

### Investigate Churn reasons
Visualize the Number of Customers and Churn Reason in column chart. Calculate Number of Customers as a Percent of Total.
![image](https://user-images.githubusercontent.com/92245436/148063254-26280391-9b0b-4c09-acc6-8dd853ba57cd.png)


### Churn category 
![image](https://user-images.githubusercontent.com/92245436/148064109-221329c1-e586-418b-82d5-ea7063cbc80c.png)

### Churn by State 
  ![image](https://user-images.githubusercontent.com/92245436/148066989-c6201c83-ea2a-4f25-ac27-7c7d66ec5d29.png)
