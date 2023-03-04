![](Aspose.Words.02e4c1d8-8466-462b-941e-1b3ff427014e.001.jpeg)

**Review-1                  CSE3020-Data Visualization** 

**Slot: D1             Faculty: Lydia Jane G** 

**Indian Startups-2021** 

**Submitted by: Satwik Tanwar (20BCE2945)** 

**Dataset Details:** 

**Dataset**: Indian Startups – 2021 

The Dataset contains the list of Private Limited companies registered with Ministry of Corporate Affairs (MCA) across India in 2021 (January to April). The data is anonymised and unique id is generated for the companies registered. 

URL:[ https://www.kaggle.com/bhararthshiviah/indian-startups-2021 ](https://www.kaggle.com/bhararthshiviah/indian-startups-2021)Cleaned Data URL:[ https://drive.google.com/file/d/1_ST97Tc2dILzk- w_JaUsw9k9k_bSd4XE/view?usp=sharing ](https://drive.google.com/file/d/1_ST97Tc2dILzk-w_JaUsw9k9k_bSd4XE/view?usp=sharing)

Number of Items (Rows) : 54,894 Number of Attributes (Columns) : 12 

Language used: Python 

**Attributes Definition**: 

1. **company\_uid:**  Unique  identification  number  generated  for  each  registered company. 
1. **date\_of\_registration:** Date when the company was register with Ministry of Corporate Affairs (MCA). 
1. **month\_name:** Which month the company was registered. 
1. **state:** In which region/location that company was registered. 
1. **roc:** This field informs in which Registrar of Companies (RoC) the company was registered.  
1. **category:** Weather the entity is limited by shares or guarantee. 
1. **class:** Whether the entity is PRIVATE LIMITED (OPC) or PRIVATE LIMITED.  
1. **company\_type:** Whether it is run by Government or Private. 
1. **authorized\_capital:** Authorized capital is the maximum amount of capital a company is authorized to raise from its shareholders. 
1. **paidup\_capital:** Paid-up capital is the amount paid by the shareholders for the shares held by them in the company. 
1. **activity\_code:** This provides the id of the nature of business the entity is legally registered for. 
1. **activity\_description:** This provides the nature of business the entity is legally registered for. 

**Task Abstraction:** 

**Q1**. What were the trends of registration of new companies during January-2021 and    

April-2021? 

*Attributes Required:* month\_name, date\_of\_registration 

**Q2.** How did COVID-19 second-wave affected the number of companies registered 

monthly? 

*Attributes Required:* montt\_name, date\_of\_registration 

**Q3.** What are the trends in authorized and paid-up capital? 

*Attributes Required:* authorized\_capital, paidup\_capital, activity\_description 

**Q4.** Which sector has the most potential for future opportunities throughout  the 

country? 

*Attributes Required:* authorized\_capital, paidup\_capital, activity\_description 

**Q5.** Does the business trends at the national level reflects in the trends at states and 

RoC levels? 

*Attributes Required:* state, roc, authorized\_capital , paidup\_capital 

**Q6.** What are the sectors in which foreign countries are investing in India? 

*Attributes Required:* company\_type, activity\_description 

**Q7.** How are the foreign companies performing in India? 

*Attributes  Required:*  company\_type,  activity\_description,  authorized\_capital, paidup\_capital 

**Q8.** What is the preferred category of company in India and why? 

*Attributes Required:* category, company\_type, activity\_description 

The first action is to identify the plots that can represent the data in the best possible  way  and  then  understand  those  plots  to  achieve  the  target  of  answering  these question through visualizing the data and getting insights about the new businesses and their trends in India.  

**Data Abstraction:** 



|**S.no.** |**Attributes** |**Datatypes** |
| - | - | - |
|1. |company\_uid |Categorical  |
|2. |date\_of\_registration |Quantitative Ordered |
|3. |month\_name |Categorical |
|4. |state |Categorical |
|5. |roc |Categorical |
|6. |category |Categorical |
|7. |class |Categorical |
|8. |company\_type |Categorical |
|9. |authorized\_capital |Quantitative Ordered |
|10. |paidup\_capital |Quantitative Ordered |
|11. |activity\_code |Categorical |
|12. |activity\_description |Categorical |

**Encoding: Code:** 

- In[1]: 

import numpy as np 

import pandas as pd 

import matplotlib.pyplot as plt 

import seaborn as sns get\_ipython().run\_line\_magic('matplotlib', 'inline') 

- In[2]: companies=pd.read\_csv('2021\_registered\_companies.csv') 
- ### Number of Companies Registered in each month. 
- In[3]: 

ax=plt.figure(figsize=(10,8)).add\_axes([0,0,1,1]) sns.set\_style('white') sns.countplot(x='month\_name',data=companies) 

for rect in ax.patches: 

`    `ax.text (rect.get\_x() + rect.get\_width() / 2,rect.get\_height(),"%i"% rect.get\_height()              ,fontsize=14 ) 

plt.title('Registered Companies',fontsize=14, weight='bold') plt.xlabel('Month',fontsize=14) 

plt.ylabel('Number of Companies Registered',fontsize=14) plt.show() 

- ### Companies Registered by Date 
- In[4]: 

companies\_date=pd.DataFrame(companies['date\_of\_registration'].groupby 

`                              `(companies['date\_of\_registration'].iloc[:]).count()) companies\_date.rename(columns={"date\_of\_registration":"count"},inplace=True) companies\_date.sort\_values('date\_of\_registration') companies\_date.reset\_index(inplace=True) 

\# In[5]: 

df=companies.pivot\_table(index=['month\_name','date\_of\_registration']) df['count']=np.array(companies\_date['count']) df.drop('activity\_code',axis=1,inplace=True) df.sort\_values('date\_of\_registration',inplace=True) df.reset\_index(inplace=True) 

- In[6]: 

ax=plt.figure(figsize=(10,8)).add\_axes([0,0,1,1]) sns.set\_style('white') sns.boxplot(x='month\_name',y='count',data=df) plt.title('Registered Companies in a day',fontsize=14, weight='bold') plt.xlabel('Month',fontsize=14) 

plt.ylabel('Number of Companies Registered in a day',fontsize=14) plt.show() 

- ### Companies in each Sector 
- In[7]: 

ax=plt.figure(figsize=(11,8)).add\_axes([0,0,1,1]) sns.set\_style('white') sns.countplot(y='activity\_description',data=companies) 

for rect in ax.patches: 

`    `ax.text (rect.get\_width(), rect.get\_y() + rect.get\_height() / 2,              "%i"% rect.get\_width(),fontsize=13 ) 

plt.title('Sectors of Companies',fontsize=14, weight='bold') plt.xlabel('Number of Companies Registered',fontsize=14) plt.ylabel('Sectors',fontsize=14) 

plt.show() 

- In[8]: 

companies\_sector=pd.DataFrame(companies['activity\_description'].groupby 

`                              `(companies['activity\_description'].iloc[:]).count()) companies\_sector.rename(columns={"activity\_description":"count"},inplace=True) companies\_sector.sort\_values('count',ascending=False,inplace=True) companies\_sector.loc['Others'] = [ companies\_sector.iloc[5:,0].sum()]  companies\_sector.sort\_values('count',ascending=False,inplace=True) companies\_sector=companies\_sector.iloc[:6,0] 

\# In[9]: 

plt.figure(dpi=1000) 

pie, ax = plt.subplots(figsize=[10,7]) 

labels = companies\_sector.keys() 

plt.pie(x=companies\_sector, autopct="%.1f%%",labels=labels, pctdistance=0.5) plt.title("Registered Companies by Sector", weight='bold',fontsize=14); plt.show() 

- ### Comparision of Companies on the basis of Authorized and Paid-up capital 
- In[10]: 

companies\_activity=companies.pivot\_table(index='activity\_description',values=['paidup\_capi tal','authorized\_capital']) 

companies\_activity.reset\_index(inplace=True) 

- In[11]: 

plt.figure(figsize=(17,8)) 

df = companies\_activity.melt('activity\_description', var\_name='capital',  value\_name='vals') sns.pointplot(x="activity\_description", y="vals", hue='capital', data=df) 

plt.xticks(rotation = 90) 

plt.title('Comparision between sectors',fontsize=14, weight='bold') plt.xlabel('Sectors',fontsize=14) 

plt.ylabel('Capital',fontsize=14) 

plt.show() 

- ### Companies registered in states 
- In[12]: 

companies\_state=pd.DataFrame(companies['state'].groupby 

`                              `(companies['state'].iloc[:]).count()) companies\_state.rename(columns={"state":"count"},inplace=True) companies\_state.sort\_values('count',ascending=False,inplace=True) companies\_state.reset\_index(inplace=True) 

- In[13]: 

plt.figure(figsize=(17,7)) 

sns.set\_style('whitegrid') sns.barplot(x='state',y='count',data=companies\_state) 

plt.xticks(rotation = 90) 


plt.title('Registered Companies in States',fontsize=10, weight='bold') plt.xlabel('States',fontsize=14) 

plt.ylabel('Number of Companies Registered',fontsize=14) plt.show() 

- #### The graph of some of the graphs at last are not visibile so they are seperately plotted #here 
- In[14]: 

plt.figure(figsize=(17,7)) 

sns.set\_style('whitegrid') sns.barplot(x='state',y='count',data=companies\_state[21:]) 

plt.xticks(rotation = 90) 

plt.title('Registered Companies in States',fontsize=10, weight='bold') plt.xlabel('States',fontsize=14) 

plt.ylabel('Number of Companies Registered',fontsize=14) plt.show() 

- ### Comparision of trends in top 5 states with national trends 
- In[15]: 

companies5=companies[(companies['state'] == 'Maharashtra') |                      (companies['state'] == 'Uttar Pradesh') | 

`                     `(companies['state'] == 'Delhi') | 

`                     `(companies['state'] == 'Karnataka') | 

`                     `(companies['state'] == 'Telangana') 

`                    `] 

- In[16]: 

companies5\_sector=pd.DataFrame(companies5['activity\_description'].groupby 

`                              `(companies5['activity\_description'].iloc[:]).count()) companies5\_sector.rename(columns={"activity\_description":"count"},inplace=True) companies5\_sector.sort\_values('count',ascending=False,inplace=True) companies5\_sector.loc['Others'] = [ companies5\_sector.iloc[5:,0].sum()]  companies5\_sector.sort\_values('count',ascending=False,inplace=True) companies5\_sector=companies5\_sector.iloc[:6,0] 

- In[17]: plt.figure(dpi=1000) 

pie, ax = plt.subplots(figsize=[10,7]) 

labels = companies5\_sector.keys() 

plt.pie(x=companies5\_sector, autopct="%.1f%%",labels=labels, pctdistance=0.5) plt.title("Registered Companies by Sector in top 5 states", weight='bold',fontsize=14); plt.show() 

- In[18]: 

companies5\_activity=companies5.pivot\_table(index='activity\_description',values=['paidup\_c apital','authorized\_capital']) 

companies5\_activity.reset\_index(inplace=True) 

- In[19]: 

plt.figure(figsize=(17,8)) 

df = companies5\_activity.melt('activity\_description', var\_name='capital',  value\_name='vals') sns.pointplot(x="activity\_description", y="vals", hue='capital', data=df) 

plt.xticks(rotation = 90) 

plt.title('Comparision between sectors in top 5 states',fontsize=14, weight='bold') plt.xlabel('Sectors',fontsize=14) 

plt.ylabel('Capital',fontsize=14) 

plt.show() 

- ### Companies registered in various RoC 
- In[20]: 

companies\_roc=pd.DataFrame(companies['roc'].groupby 

`                              `(companies['roc'].iloc[:]).count()) companies\_roc.rename(columns={"roc":"count"},inplace=True) companies\_roc.sort\_values('count',ascending=False,inplace=True) companies\_roc.reset\_index(inplace=True) 

- In[21]: 

plt.figure(figsize=(17,7)) sns.set\_style('whitegrid') 

sns.barplot(x='roc',y='count',data=companies\_roc) 

plt.xticks(rotation = 90) 

plt.title('Registered Companies at RoC',fontsize=10, weight='bold') plt.xlabel('RoC',fontsize=14) 

plt.ylabel('Number of Companies Registered',fontsize=14) plt.show() 

- ### Foreign Investments in India 
- In[22]: 

companies\_foreign=companies[companies['company\_type']=='Subsidiary of Foreign Company'] 

- In[23]: 

ax=plt.figure(figsize=(11,8)).add\_axes([0,0,1,1]) sns.set\_style('white') sns.countplot(y='activity\_description',data=companies\_foreign) for rect in ax.patches: 

`    `ax.text (rect.get\_width(), rect.get\_y() + rect.get\_height() / 2,              "%i"% rect.get\_width(),fontsize=13 ) 

plt.title('Sectors of Companies',fontsize=14, weight='bold') plt.xlabel('Number of Companies Registered',fontsize=14) plt.ylabel('Sectors',fontsize=14) 

plt.show() 

- ### Capital Raised by Foreign Countries in India 
- In[24]: 

ax=plt.figure(figsize=(17,10)).add\_axes([0,0,1,1]) 

sns.set\_style('whitegrid') sns.stripplot(x='activity\_description',y='paidup\_capital',data=companies[companies['paidup\_ capital']<1.5e9], 

`              `jitter=True,hue='company\_type',palette='hls',size=10) 

plt.xticks(rotation = 90) 

plt.title('Paid-up Capital',fontsize=14, weight='bold') 

plt.xlabel('Sectors',fontsize=14) 

plt.ylabel('Capital',fontsize=14) 

plt.show() 

- In[25]: 

fcompanies\_activity=companies\_foreign.pivot\_table(index='activity\_description',                                                   values=['paidup\_capital','authorized\_capital']) fcompanies\_activity.reset\_index(inplace=True) 

- In[26]: 

plt.figure(figsize=(17,8)) 

foreign = fcompanies\_activity.melt('activity\_description', var\_name='capital',  value\_name='vals') 

sns.pointplot(x="activity\_description", y="vals", hue='capital', data=foreign) plt.xticks(rotation = 90) 

plt.title('Comparision between sectors',fontsize=14, weight='bold') plt.xlabel('Sectors',fontsize=14) 

plt.ylabel('Capital',fontsize=14) 

plt.show() 

- In[27]: 

ax=plt.figure(figsize=(10,8)).add\_axes([0,0,1,1]) sns.set\_style('white') sns.countplot(x='category',data=companies) 

for rect in ax.patches: 

`    `ax.text (rect.get\_x() + rect.get\_width() / 2,rect.get\_height(),"%i"% rect.get\_height()              ,fontsize=14 ) 

plt.title('Category of Registered Companies',fontsize=14, weight='bold') plt.xlabel('Categories',fontsize=14) 

plt.ylabel('Number of Companies Registered',fontsize=14) 

plt.show() 

- In[28]: 

plt.figure(figsize = (5,5)) sns.scatterplot(x='company\_type',y='category',data=companies) plt.xticks(rotation = 90) 

plt.show() 

- In[29]: 

ax=plt.figure(figsize=(7,5)).add\_axes([0,0,1,1]) 

sns.set\_style('white') sns.countplot(y='activity\_description',data=companies[companies['category']=='Company Limited by Guarantee']) 

for rect in ax.patches: 

`    `ax.text (rect.get\_width(), rect.get\_y() + rect.get\_height() / 2, 

`             `"%i"% rect.get\_width(),fontsize=13 ) 

plt.title('Sectors of Companies Limited by Guarantee',fontsize=14, weight='bold') plt.xlabel('Number of Companies Registered',fontsize=14) plt.ylabel('Sectors',fontsize=14) 

plt.show() 

**Graphs:** 

![](Aspose.Words.02e4c1d8-8466-462b-941e-1b3ff427014e.002.png)

This graph shows the total number of companies that were registered in each month in the given period of time. 

![](Aspose.Words.02e4c1d8-8466-462b-941e-1b3ff427014e.003.jpeg)

During January 2021 the condition of daily COVID-19 cases was just getting better and the number of companies registered in most of the days of January was between 550 to 650 approximately but there were some days when it was much lower. 

As the condition was getting better during February the number of companies registered each day increased and the consistency was good, the value even got better in March but in April the second wave of COVID-19 hit us and the number of companies registered each day decreased and the consistency also went down. 

![](Aspose.Words.02e4c1d8-8466-462b-941e-1b3ff427014e.004.jpeg)

This graph shows the comparison between the number of companies registered with different activity descriptions i.e. in different sectors. 

![](Aspose.Words.02e4c1d8-8466-462b-941e-1b3ff427014e.005.jpeg)

It shows the percentage of companies with different activity description that were registered. 

We can clearly observe the sector in which maximum number of companies were registered from the above graphs (Barplot and Pie Chart) 

![](Aspose.Words.02e4c1d8-8466-462b-941e-1b3ff427014e.006.jpeg)

We can observe from the above graph that apart from two sectors (Electricity, Gas & Water Companies and Mining & Quarrying), the difference between authorized and paid-up capital is no that much which means that they have already generated most of the capital that they can but there is a lot of capital available that can be generated in Electricity, Gas & Water Companies and Mining & Quarrying. 

If we look at the above three plots we can observe that only 1% and 0.6% of total companies  registered  were  in  Electricity,  Gas  &  Water  Companies  and  Mining  & Quarrying sectors respectively but the amount of capital left to be generated in these sectors  is  enormous,  therefore  these  sectors  have  a  lot  of  potential  for  future opportunities provided people can come up with new innovative ideas to make proper use of this potential. 

![](Aspose.Words.02e4c1d8-8466-462b-941e-1b3ff427014e.007.jpeg)

This  graph  shows  the  number  of  companies  registered  in  each  state  and  Union Territory with the top 5 states being Maharashtra, Uttar Pradesh, Delhi, Karnataka and Telangana. 

![](Aspose.Words.02e4c1d8-8466-462b-941e-1b3ff427014e.008.jpeg)

This is a zoomed in version of the States and Union Territories with least registered 

companies. 

Companies Registered in TOP 5 States:- ![](Aspose.Words.02e4c1d8-8466-462b-941e-1b3ff427014e.009.jpeg)

This shows the percentage of companies registered in different sectors in the states with top 5  number of companies registered. 

Companies registered in whole country :- ![](Aspose.Words.02e4c1d8-8466-462b-941e-1b3ff427014e.010.jpeg)

If we compare the pie chart for top 5 states with the similar pie chart that we created for the whole country, we can observe that the national trends are reflected in these states while talking about the number of companies registered  in each sector. 


![](Aspose.Words.02e4c1d8-8466-462b-941e-1b3ff427014e.011.jpeg)

This graph shows the trends of authorized and paid-up capitals of companies in the top 5 states. We can observe that there is a very less difference between authorized and paid-up capitals in almost every sector as compared to the data of all the states and also the difference for Electricity, Gas & Water Companies is significantly lower. This is due to the fact that most of the big companies are located in these places and also there is a lot of competition in these places.  

Mining and Quarrying still have a lot of potential capital to be generated in these states as compared to other sectors.  

![](Aspose.Words.02e4c1d8-8466-462b-941e-1b3ff427014e.012.jpeg)

This barplot compares the number of companies registered in each RoC. 

We can observe that the top five RoC are from the top 5 states and therefore, we can conclude that the trends that we observed for these stats are reflected on these RoC too. 

![](Aspose.Words.02e4c1d8-8466-462b-941e-1b3ff427014e.013.jpeg)

` `This plot shows all the sectors in which new subsidiaries of foreign companies have been registered. We can observe that the maximum investments are made in the Business Services Sectors by foreign companies. 

![](Aspose.Words.02e4c1d8-8466-462b-941e-1b3ff427014e.014.jpeg)

This Jitter Plot shows the paid-up capitals of all the companies of the dataset with different colours for different types of companies. 

We can observe that most of the foreign companies have more paid-up capital than Indian companies, since more that 65% of foreign companies are in Business Services sector and their paid-up capitals are more than most of the other companies, we can conclude that foreign companies are performing quite well in India. 

![](Aspose.Words.02e4c1d8-8466-462b-941e-1b3ff427014e.015.jpeg)

This  shows  the  difference  between  authorized  and  paid-up  capitals  of  foreign companies. We can observe that for most of the sectors,  authorized and paid-up capitals are same but in Business services there is a good difference between them indicating potential of growth in this sector for foreign companies. 

![](Aspose.Words.02e4c1d8-8466-462b-941e-1b3ff427014e.016.jpeg)

This plot shows that more than 99% of the companies are limited by share in Indian. This is because of the fact that these companies make profits but a company limited by guarantee is a non-profit company. 

![](Aspose.Words.02e4c1d8-8466-462b-941e-1b3ff427014e.017.png)

This scatter plot shows that none of the subsidiaries of foreign companies and Union Government Companies are limited by guarantee. 

![](Aspose.Words.02e4c1d8-8466-462b-941e-1b3ff427014e.018.jpeg)

From this plot, we can observe that more than 99% of the companies limited by guarantee are in the Community, personal & Social Services sector because these companies are generally non-profit companies. 
