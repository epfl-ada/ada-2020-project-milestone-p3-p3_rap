# Project milestone 3 - RAP

### Title
Policing patterns in major cities in the United States of America

### Abstract
Racial injustice is a long lasting problem which affects millions of people in the United States on a daily basis. Recently, the Black Lives Matter movement has helped bring more attention to this issue.
The paper considered suggests a global trend of racial bias in policing in the United States. Using the paper's dataset combined with other information sources, we would like to explore how and why this bias varies across multiple cities.
We focus on three urban areas with different ethnic distributions, each with a majority of white, black and hispanic residents respectively, in order to determine if minorities are stopped more even if they are "the majority", i.e. if a greater exposure to minority groups reduces or emphasises the racial bias.
We then focus on the metropolitan area of Pittsburgh, where our goal is to identify typical profiles among police officers, and analyze the relationship between those profiles and their interventions.

### Research Questions
1. How do policing patterns vary between San Antonio (TX), New Orleans (LA) and Pittsburgh (PA)?
2. Can we extract typical profiles for police officers? If so, does a certain profile stand out, for example by making more racial arrests?

### Proposed dataset
1. We will use the dataset of the original paper [1], focusing on Pittsburgh, New-Orleans, and San Antonio. We decided to focus on the city level data rather than state-wide data to explore dynamics at a finer level and because minorities are mostly concentrated in urban counties, as suggested by [2]. We chose these locations for their varying ethnicity distributions, and because they have rather complete data including pedestrian stops, location (which will be useful for plotting on a map) and span multiple years. Pittsburgh was also chosen due to its data on officers (age, race, sex, years of service, …).  
2. We will combine this dataset with some data from the Data USA's website [3] to have the racial distribution of the different cities we will analyze [4] [5] [6]. The data, which can be downloaded in csv format, includes the number of citizens for each race, with data from 2013 upto 2018. We will probably group different subcategories together, such as "white (hispanic)" and "other (hispanic)".

### Methods
- Data collection:  Download the paper's data in csv format and create a pandas Dataframe with it. Our other datasets will also be downloaded, and processed to obtain the ethnicities in the different cities.

- First question: We can visually compare the amount of stops on a map to see if there is a significant difference between the 3 cities, based on demographics alone. We can add a slider to change either the time or date of the stop (we'll see what gives more interesting results), and we would group the data by intervals (i.e. yearly quarters, part of day, post/pre darkness). We can add such interactive charts to our datastory website using plotly [7]. Since such visual results may be misleading (a majority black city will probably have a majority of blacks stopped) so we will include other types of plots which will be normalized with respect to the population's ethnicity distribution.

- Cluster identification: To identify clusters among the officers, we will use the different policeman characteristics available. Among the characteristics, we have the sex (male, female) or the race (white, black, hispanic). From these, we will create categorical variables as follows: one for the sex (0 or 1 depending on the sex of the police officer), and one or multiple varaibles for the race (we have can either create a binary variable, with 0 is the person is white and 1 if the person is from a minority, or we could create multplie binary variable, one for each race stating if the police officer is of a given race). We are not entirely sure of which method is the best for the race variable, as creating one variable loses some information (the difference between black and hispanic), but creating three variables will increase the dimensionality a lot. Therefore, we will try both methods. \
To find our clusters we could try using DBSCAN and k-means, however this article [8] suggests using k-medoids and partitioning around medoids (PAM) with the gower distance when the data contains both numerical and categorical values. We will need to tune our hyperparameters (e.g. number of clusters) based on the outcome. The quality of our clusters will be evaluated mostly by inspecting the clusters manually and checking if they make sense (seem to capture a category well for example old white males, or middle-aged black women). \
In the case where clusters don't yield good results (i.e. clusters aren't easily interpretable), we can try to manually create them to test certain hypotheses such as grouping them by (race,age) or (race,gender).

- Post clustering: Once we have our clusters, we will look at the distribution of the stops each cluster performed. If the distributions across clusters seem uniform, it could indicate that either there is an overall bias or there is none. On the other hand, if a certain profile (cluster) stands out, we could conclude that that particular group is more / less biased.

### Proposed timeline
We will have a total of 3 weeks to complete the assignment:
1. Download and clean the data. Start the different analysis with the goal to obtain the first results. Create the skeleton of the report and the website for the data story.
2. Finish analysis and start to include them in the website.
3. Finalize website and report, clean up / comment code, make the video

### Organization within the team
- Raphael will gather all needed datasets, and perform basic statistics for the 3 cities. He will work on putting the video together.
- Peter will cluster the police officers using k-medoids and PAM.
- Anton.io will analyse the clusters, make the maps and the skeleton for the jekyll website.

Finally, each of us will participate in the redaction of the paper, the structuring of the website and the flow of the video.

### Questions for TAs (optional)
We wanted to know if this project proposal is final, or if we are free to do some minor adjustments such as slightly adapting our research questions or adding a sub-question along the way if we think of / find something of interest.
During our brainstorming, we came up with the question "Do the police officers have a certain quota of stops to satisfy?". We are not sure to have the time to complete it but thought that it deserved a mention, should we add it to our research questions?

### Links & References
1. [Original paper's data](https://openpolicing.stanford.edu/data/)
2. [Minorities in urban, rural and suburban zone](https://www.pewsocialtrends.org/2018/05/22/views-of-problems-facing-urban-suburban-and-rural-communities/)
3. [Data USA](https://datausa.io/)
4. [Racial data from the city of Pittsburgh](https://datausa.io/api/data?Geography=31000US38300&drilldowns=Race,Ethnicity&measures=Hispanic%20Population,Hispanic%20Population%20Moe)
5. [Racial data from the city of New-Orleans](https://datausa.io/api/data?Geography=79500US2202401&drilldowns=Race,Ethnicity&measures=Hispanic%20Population,Hispanic%20Population%20Moe)
6. [Racial data from the city of San Antonio](https://datausa.io/api/data?Geography=79500US4805901&drilldowns=Race,Ethnicity&measures=Hispanic%20Population,Hispanic%20Population%20Moe)
7. [Plotly](https://plotly.com/javascript/) 
8. [Clustering](https://towardsdatascience.com/clustering-datasets-having-both-numerical-and-categorical-variables-ed91cdca0677)