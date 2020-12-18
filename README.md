# Project milestone 3 - RAP

:warning: **Note** that our notebook won't render correctly on github, as it uses plotly to generate interactive figures, which requires it's javascript library. The fully rendered version is available [right here](https://nbviewer.jupyter.org/github/epfl-ada/ada-2020-project-milestone-p3-p3_rap/blob/main/notebook.ipynb).

The **datastory** is available here: [https://antonragot.github.io/Policing-Patterns/](https://antonragot.github.io/Policing-Patterns/). 

### Title
Arrest me if you can !

### Abstract
Racial injustice is a long lasting problem which affects millions of people in the United States on a daily basis. Recently, the Black Lives Matter movement has helped bring more attention to this issue.
The paper considered suggests a global trend of racial bias in policing in the United States. Using the paper's dataset combined with other information sources, we would like to explore how and why this bias varies across multiple neighborhoods of Pittsburh (PA).

We want determine if the black drivers are more stopped even if they are more present in certain area, i.e. if a greater exposure to the black minority reduces or emphasises the racial bias.
We then focus on regrouping police officers using different trait such as sex, age or number of arrest.Our goal is to identify typical profiles among police officers, and analyze the relationship between those profiles and their interventions.

### Research Questions
1. Are police officers targeting certain neighborhoods in Pittsburgh (PA)? If so, is it a racial reason?
2. Can we extract typical profiles for police officers from sex, age and experience? If so, does a certain profile stand out, for example by making more racial arrests?

### Proposed dataset
1. We will use the dataset of the original paper [1], focusing on Pittsburgh. We decided to focus on the city level data rather than state-wide data to explore dynamics at a finer level and because minorities are mostly concentrated in urban counties, as suggested by [2]. We chose Pittsburgh for its complete data on officers (age, race, sex, years of service, …) and location (which will be useful for plotting on a map). 
2. We will combine this dataset with some data from the Data USA's website [3] to have the racial distribution of Pittsburgh we will analyze [4]. The data, which can be downloaded in csv format, includes the number of citizens for each race, with data from 2013 upto 2018. We will probably group different subcategories together, such as "white (hispanic)" and "other (hispanic)".
3. We will also add informations on neighborhoods from the Western Pennsylvania Regional Data Center [5]. This will allow us to compare the different neighborhoods based on criminality and income.

### Methods
- Data collection:  Download the paper's data in csv format and create a pandas Dataframe with it. Our other datasets will also be downloaded, and processed to obtain the ethnicities in the different cities.

- First question: We can visually compare the amount of stops on a map to see if there is a significant difference between the different neighborhoods, based on demographics alone. We can add interactive charts to our datastory website using plotly [6]. Since visual results may be misleading (a majority black neighborhoods will probably have a majority of blacks stopped) so we will include other types of plots which will be normalized with respect to the population's ethnicity distribution.

- Cluster identification: To identify clusters among the officers, we will use the different policeman characteristics available. Among the characteristics, we have the sex (male, female) or the race (white, black, hispanic). From these, we will create categorical variables as follows: one for the sex (0 or 1 depending on the sex of the police officer), and one or multiple varaibles for the race (we have can either create a binary variable, with 0 is the person is white and 1 if the person is from a minority, or we could create multplie binary variable, one for each race stating if the police officer is of a given race). We are not entirely sure of which method is the best for the race variable, as creating one variable loses some information (the difference between black and hispanic), but creating three variables will increase the dimensionality a lot. Therefore, we will try both methods. \
To find our clusters we could try using DBSCAN and k-means, however this article [7] suggests using k-medoids and partitioning around medoids (PAM) with the gower distance when the data contains both numerical and categorical values. We will need to tune our hyperparameters (e.g. number of clusters) based on the outcome. The quality of our clusters will be evaluated mostly by inspecting the clusters manually and checking if they make sense (seem to capture a category well for example old white males, or middle-aged black women). \
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
- Anton will analyse the clusters, make the maps and the skeleton for the jekyll website.

Finally, each of us will participate in the redaction of the paper, the structuring of the website and the flow of the video.

### Links & References
1. [Original paper's data](https://openpolicing.stanford.edu/data/)
2. [Minorities in urban, rural and suburban zone](https://www.pewsocialtrends.org/2018/05/22/views-of-problems-facing-urban-suburban-and-rural-communities/)
3. [Data USA](https://datausa.io/)
4. [Racial data from the city of Pittsburgh](https://datausa.io/api/data?Geography=31000US38300&drilldowns=Race,Ethnicity&measures=Hispanic%20Population),
5. [Western Pennsylvania Regional Data Center](https://data.wprdc.org/dataset/pgh)
6. [Plotly](https://plotly.com/javascript/) 
7. [Clustering](https://towardsdatascience.com/clustering-datasets-having-both-numerical-and-categorical-variables-ed91cdca0677)
