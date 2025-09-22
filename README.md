# **Programming Assignment 4**
---
### File links: 
Program Assignment 4: [https://PA 4.com](https://github.com/ajtdengust326/DUADICO_2ECE-B_Programming-Assignment-4/blob/main/DUADICO_2ECE-B_ECE2112_PA%204.ipynb)  
board2.xlsx: [https://board2.com](https://github.com/ajtdengust326/DUADICO_2ECE-B_Programming-Assignment-4/blob/main/board2.xlsx)

---
## **ECE BOARD EXAM PROBLEM**
> Using data wrangling and data visualization technique with storytelling, analyze the data and present different
> >(i) data frames; and  
> >(ii) visuals using the dataset given.

Output:
| Name | Gender | Track | Math |
| :------------------- | :----------: | :----------: | ----------: |
| S4            | Male      | Instrumentation       | 65 |
| S11              | Female      | Communication     | 48 |
| S22               | Female      | Communication       | 64 |

### 1). Create the following data frames based on the format provided:  
##### Example: Vis = [“Name”, “Gender”, “Track”, “Math<70”]; hometown is constant as Visayas  
***
```
import pandas as pd

df = pd.read_excel('board2.xlsx')     
```
> This is to be able to read the Excel file, so it can be loaded into the data frame. (board2.xlsx)

#### a) Filename: Instru = [“Name”, “GEAS”, “Electronics >70”]; where track is constant as Instrumentation and hometown Luzon
```
Instru = df.loc[(df['Track']=='Instrumentation')&(df['Hometown']=='Luzon')&(df['Electronics']>70),['Name', 'GEAS', 'Electronics']]
Instru
```
> We are asked to locate the data with these given conditions.
#### b) Filename: Mindy = [ “Name”, “Track”, “Electronics”, “Average >=55”]; where hometown is constant as Mindanao and gender Female
```
df['Ave'] = df[['Math','Electronics','GEAS','Communication']].mean(axis=1)  #line 1                      
Mindy = df.loc[(df['Hometown']=='Mindanao')&(df['Gender']=='Female')&(df['Ave']>=55),['Name', 'Track', 'Electronics','Ave']] #Line 2
Mindy
```
>  This code computes the average scores across those subjects for each student and stores the result in the column. (Line 1)
> > We are also asked to locate the data with these given conditions. (Line 2)

### 2). Create a visualization that shows how the different features contributes to average grade. Does chosen track in college, gender, or hometown contributes to a higher average score?
##### This is for the average score in terms of the chosen track in college
```
import matplotlib.pyplot as plt

tracks = df['Track'].unique()
```
> This code identifies all different categories or options listed under without any duplicates.
```                                           
plt.bar(tracks, [df[df['Track'] == t]['Ave'].mean() for t in tracks]
```
> This is to compute the average grade in terms of the chosen track and shows the visualization.
##### This is for the average score in terms of gender 
```
genders = df["Gender"].unique()
```
> This code identifies all different categories or options listed under without any duplicates.
```
plt.bar(genders, [df[df["Gender"] == g]["Ave"].mean() for g in genders])
```
> This is to compute the average grade in terms of the gender and shows the visualization.
##### This is for the average score in terms of hometown
```
hometowns = df["Hometown"].unique()
```
> This code identifies all different categories or options listed under without any duplicates.
```
plt.bar(hometowns, [df[df["Hometown"] == h]["Ave"].mean() for h in hometowns]) 
```
> This is to compute the average grade in terms of the gender and shows the visualization.

#### To summarize question number (2), I included a conclusion base of the output data
## Conclusion:
> From the graphs, it looks like the track in college has the biggest effect on the average grade since the scores vary a bit between Instrumentation, Communication, and Microelectronics. On the other hand, gender doesn’t really show much difference because male and female students have almost the same average grades. The same goes for hometown, where Luzon, Mindanao, and Visayas students all have very close scores. This means the chosen track matters more than gender or hometown when it comes to average grades.
