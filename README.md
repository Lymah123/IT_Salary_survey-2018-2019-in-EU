# IT_Salary_survey-2018-2020-in-EU
EDA-on-IT-Salary-Survey(2018-2020)
Note: An anonymous salary survey has been conducted annually since 2015 among European IT specialists with a stronger focus on Germany. This year 1238 respondents volunteered to participate in the survey. The data has been made publicly available by the authors. The dataset contains rich information about the salary patterns among the IT professionals in the EU region and offers some great insights. Here is my Data cleaning and analysis of the data.TASK
TASK
Data Acqusition and loading
Data Cleansing
DATA VIZUALIZATION
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import plotly.express as px
import scipy
from scipy import stats
import statistics
DATA ANALYSIS

data_2018.head()
Timestamp	Age	Gender	City	Position	Years of experience	Your level	Current Salary	Salary one year ago	Salary two years ago	Are you getting any Stock Options?	Main language at work	Company size	Company type
0	14/12/2018 12:41:33	43.0	M	München	QA Ingenieur	11.0	Senior	77000.0	76200.0	68000.0	No	Deutsch	100-1000	Product
1	14/12/2018 12:42:09	33.0	F	München	Senior PHP Magento developer	8.0	Senior	65000.0	55000.0	55000.0	No	Deutsch	50-100	Product
2	14/12/2018 12:47:36	32.0	M	München	Software Engineer	10.0	Senior	88000.0	73000.0	54000.0	No	Deutsch	1000+	Product
3	14/12/2018 12:50:15	25.0	M	München	Senior Frontend Developer	6.0	Senior	78000.0	55000.0	45000.0	Yes	English	1000+	Product
4	14/12/2018 12:50:31	39.0	M	München	UX Designer	10.0	Senior	69000.0	60000.0	52000.0	No	English	100-1000	Ecom retailer
data_2020.info()
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 1253 entries, 0 to 1252
Data columns (total 23 columns):
 #   Column                                                                                                                   Non-Null Count  Dtype  
---  ------                                                                                                                   --------------  -----  
 0   Timestamp                                                                                                                1253 non-null   object 
 1   Age                                                                                                                      1226 non-null   float64
 2   Gender                                                                                                                   1243 non-null   object 
 3   City                                                                                                                     1253 non-null   object 
 4   Position                                                                                                                 1247 non-null   object 
 5   Total years of experience                                                                                                1237 non-null   object 
 6   Years of experience in Germany                                                                                           1221 non-null   object 
 7   Seniority level                                                                                                          1241 non-null   object 
 8   Your main technology / programming language                                                                              1126 non-null   object 
 9   Other technologies/programming languages you use often                                                                   1096 non-null   object 
 10  Yearly brutto salary (without bonus and stocks) in EUR                                                                   1253 non-null   float64
 11  Yearly bonus + stocks in EUR                                                                                             829 non-null    object 
 12  Annual brutto salary (without bonus and stocks) one year ago. Only answer if staying in the same country                 885 non-null    float64
 13  Annual bonus+stocks one year ago. Only answer if staying in same country                                                 614 non-null    object 
 14  Number of vacation days                                                                                                  1185 non-null   object 
 15  Employment status                                                                                                        1236 non-null   object 
 16  Сontract duration                                                                                                        1224 non-null   object 
 17  Main language at work                                                                                                    1237 non-null   object 
 18  Company size                                                                                                             1235 non-null   object 
 19  Company type                                                                                                             1228 non-null   object 
 20  Have you lost your job due to the coronavirus outbreak?                                                                  1233 non-null   object 
 21  Have you been 
 forced to have a shorter working week (Kurzarbeit)? If yes, how many hours per week                        373 non-null    float64
 22  Have you received additional monetary support from your employer due to Work From Home? If yes, how much in 2020 in EUR  462 non-null    object 
dtypes: float64(4), object(19)
memory usage: 225.3+ KB
data_2020.shape
(1253, 23)
OBSERVATIONS:- [1] float64(4), object(19) /[2] Columns=123 Rows=1253 /[3] First 5 colunms = Timestamp, Age, Gender, City, Position
stats.mode(data_2018)
odeResult(mode=array([['14/12/2018 13:43:50', 30.0, 'M', 'Berlin', 'Java Developer',
        10.0, 'Senior', 60000.0, 65000.0, 60000.0, 'No', 'English',
        '100-1000', 'Product']], dtype=object), count=array([[  2,  80, 646, 291,  34, 105, 497,  73,  57,  38, 587, 581, 260,
        451]]))
stats.median(data_2018)
​
​
---------------------------------------------------------------------------
AttributeError                            Traceback (most recent call last)
<ipython-input-18-922f12c19f80> in <module>()
----> 1 stats.median(data_2018)
      2 

AttributeError: module 'scipy.stats' has no attribute 'median'

data_2018.isnull().sum
​
<bound method DataFrame.sum of      Timestamp    Age  ...  Company size  Company type
0        False  False  ...         False         False
1        False  False  ...         False         False
2        False  False  ...         False         False
3        False  False  ...         False         False
4        False  False  ...         False         False
..         ...    ...  ...           ...           ...
760      False  False  ...         False         False
761      False   True  ...         False         False
762      False   True  ...         False         False
763      False   True  ...          True          True
764      False  False  ...         False         False

[765 rows x 14 columns]>
DATA CLEANING

data_2020.isnull().sum
​
<bound method DataFrame.sum of       Timestamp  ...  Have you received additional monetary support from your employer due to Work From Home? If yes, how much in 2020 in EUR
0         False  ...                                               True                                                                      
1         False  ...                                               True                                                                      
2         False  ...                                               True                                                                      
3         False  ...                                               True                                                                      
4         False  ...                                               True                                                                      
...         ...  ...                                                ...                                                                      
1248      False  ...                                               True                                                                      
1249      False  ...                                              False                                                                      
1250      False  ...                                               True                                                                      
1251      False  ...                                              False                                                                      
1252      False  ...                                              False                                                                      

[1253 rows x 23 columns]>
data_2018.dropna(axis = 1)
Timestamp
0	14/12/2018 12:41:33
1	14/12/2018 12:42:09
2	14/12/2018 12:47:36
3	14/12/2018 12:50:15
4	14/12/2018 12:50:31
...	...
760	03/06/2020 20:12:51
761	28/07/2020 04:03:13
762	28/07/2020 04:03:20
763	26/08/2020 09:06:44
764	21/09/2020 01:47:10
765 rows × 1 columns

DATA VISUALIZATION

data_2019.info()
​
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 991 entries, 0 to 990
Data columns (total 23 columns):
 #   Column                                                                                                Non-Null Count  Dtype  
---  ------                                                                                                --------------  -----  
 0   Zeitstempel                                                                                           991 non-null    object 
 1   Age                                                                                                   882 non-null    float64
 2   Gender                                                                                                991 non-null    object 
 3   City                                                                                                  991 non-null    object 
 4   Seniority level                                                                                       976 non-null    object 
 5   Position (without seniority)                                                                          990 non-null    object 
 6   Years of experience                                                                                   991 non-null    int64  
 7   Your main technology / programming language                                                           977 non-null    object 
 8   Yearly brutto salary (without bonus and stocks)                                                       990 non-null    float64
 9   Yearly bonus                                                                                          530 non-null    float64
 10  Yearly stocks                                                                                         203 non-null    float64
 11  Yearly brutto salary (without bonus and stocks) one year ago. Only answer if staying in same country  603 non-null    float64
 12  Yearly bonus one year ago. Only answer if staying in same country                                     257 non-null    float64
 13  Yearly stocks one year ago. Only answer if staying in same country                                    139 non-null    float64
 14  Number of vacation days                                                                               931 non-null    float64
 15  Number of home office days per month                                                                  639 non-null    float64
 16  Main language at work                                                                                 986 non-null    object 
 17  Company name                                                                                          257 non-null    object 
 18  Company size                                                                                          977 non-null    object 
 19  Company type                                                                                          960 non-null    object 
 20  Сontract duration                                                                                     962 non-null    object 
 21  Company business sector                                                                               846 non-null    object 
 22  0                                                                                                     0 non-null      float64
dtypes: float64(10), int64(1), object(12)
memory usage: 178.2+ KB
fig = px.pie(data_2019, values='Company type')
fig.show()
