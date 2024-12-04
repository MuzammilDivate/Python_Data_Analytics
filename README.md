# The Analysis

# 1. What are the most demanded skills for the top 3 most popular data roles?

To find the most demanded skills for the top 3 data roles, I filtered out those positions by which ones were the most popular and got the top 5 skills for these top 3 roles. This query highlights the most popular job titles and their top skills, showing which skills one should pay attention depending on their target role.

View my notebook with detailed steps here:
[02_skill_demand.ipynb](Project_01\02_skill_demand.ipynb)

## Visualize data

```python
fig, ax = plt.subplots(len(job_titles), 1, figsize=(10, 8))
sns.set_theme(style='ticks')
for i, job_title in enumerate(job_titles):
    df_plot = df_perc[df_perc['job_title_short']==job_title].head(5)
    sns.barplot(data=df_plot, x='perc', y='job_skills', ax=ax[i], hue='job_skills', palette='dark:g')
    ax[i].set_title(job_title)
    ax[i].set_ylabel('')
    if i != len(job_titles)-1:
        ax[i].set_xlabel('')
    ax[i].set_xlim(0,78)
    
    for n, v in enumerate(df_plot['perc']):
        ax[i].text(v +1, n, f'{v:0.1f}%', va='center')
    if i != len(job_titles)-1:
        ax[i].set_xticks([])
ax[len(job_titles)-1].set_xlabel('Percentage')
fig.suptitle('Likelyhood of skills requested in US Job Posting')
fig.tight_layout()
```

## Results

![Visualization of Top skills](Project_01\Images\Skill_demand_all_data_roles.png)

## Insights


- Data Analysts

For Data Analysts, the key skills and their likelihood in job postings are:

> SQL: 50.8% - SQL stands out as the most in-demand skill, highlighting its importance for data querying and database management.

> Excel: 40.6% - Excel's high demand underscores its critical role in data analysis and manipulation.

> Tableau: 28.5% - Tableau is valued for data visualization, making it an essential skill for presenting insights.

> Python: 27.1% - Python's presence indicates a growing need for advanced data analysis and automation.

> SAS: 19.5% - Although less common, SAS is still relevant for statistical analysis.

- Data Engineers

Data Engineers need the following skills, with their likelihood in job postings:

> SQL: 68.3% - SQL is crucial for data infrastructure, reflecting its necessity in database creation and management.

> Python: 64.9% - Python's prominence signifies its vital role in data processing and automation.

> AWS: 42.8% - Experience with AWS highlights the importance of cloud platforms for handling big data.

> Azure: 32.3% - Azure is also significant for cloud-based data engineering.

> Spark: 32.0% - Spark's demand points to the need for handling large-scale data processing.

- Data Scientists

For Data Scientists, the critical skills and their likelihood in job postings are:

> Python: 72.0% - Python is the top skill, crucial for data analysis, machine learning, and developing algorithms.

> SQL: 51.1% - SQL remains essential for querying databases and managing data.

> R: 44.2% - R is important for statistical analysis and data visualization.

> SAS: 24.4% - SAS is still relevant for specialized statistical tasks.

> Tableau: 23.6% - Tableau is valued for visualizing complex data insights.


## Conclusion


The chart reveals that while SQL and Python are foundational across all data-related roles, the demand for specific skills like Excel, Tableau, AWS, Azure, Spark, and R varies significantly based on the job title. Data Analysts should focus on SQL, Excel, and Tableau, while Data Engineers need to emphasize SQL, Python, and cloud platforms like AWS and Azure. Data Scientists should prioritize Python, SQL, and R to stay competitive in their field.

# 2. How are in-demand skills trending for Data Analysts

## Visualize data

```python
from matplotlib.ticker import PercentFormatter
from adjustText import adjust_text

plt.figure(figsize=(8, 6))

sns.lineplot(df_plot, dashes=False, palette='tab10')
sns.set_theme(style='ticks')
plt.title('Trending top skills for data analyst in US')
plt.xlabel("Months")
plt.ylabel('Likelihood in job posting')
plt.legend().remove()

texts = []
for i in range(5):
    texts.append(plt.text(11.1,df_plot.iloc[-1, i], df_plot.columns[i]))

adjust_text(texts=texts, arrowprops=dict(arrowstyle='-', color='red', lw=2))

sns.despine()
ax = plt.gca()
ax.yaxis.set_major_formatter(PercentFormatter(decimals=0))
plt.tight_layout()

# Idk how to deal with the overlapping of the lines at the end ill update it if i find a way
```

## Results

![Trending top skills for data analyst in US](Project_01\Images\skill_trend.png)


## Insights 

- SQL
> This remains the most sought-after skill throughout the year, though its demand shows a slight decline from approximately 55% in January to around 45% by December. This suggests that while SQL is crucial, other skills are becoming more prominent.

- Excel
> The demand for Excel is relatively stable throughout the year, with a minor dip in November and a slight rise in December. This consistency highlights Excel's enduring relevance in data analytics roles.

- Python
> The interest in Python shows a gradual increase with minor fluctuations. Starting at around 25% in January and ending at about 28% in December, Python's growing demand indicates its rising importance in data analytics.

- Tableau
> Tableau's demand exhibits notable fluctuations, peaking in August before settling around 28% in December. This trend may reflect seasonal variations in the need for data visualization skills.

- SAS
> The demand for SAS remains relatively stable with minor fluctuations, starting at around 20% and ending at about 22%. This indicates a steady, albeit lower, demand for SAS compared to other skills.

## Conclusion


The graph highlights the evolving landscape of essential skills for data analysts in the US. While SQL and Excel remain foundational, the growing interest in Python and Tableau suggests a shift towards more advanced and versatile data analysis and visualization tools. Job seekers in data analytics should consider enhancing their proficiency in these trending skills to stay competitive in the job market.


# 3. How well do jobs and skills pay for Data Analysts

# Salary Analysis

## Visualize data

```python
sns.boxplot(data=df_us_top6, x='salary_year_avg', y='job_title_short', order=df_ordered)
sns.set_theme(style='ticks')
plt.ylabel('')
plt.ylabel('')
ax = plt.gca()
ax.xaxis.set_major_formatter(plt.FuncFormatter(lambda x, _:f'${int(x/100.0)}K'))
plt.title('Salary distribution in the US')
plt.xlim(0, 600000)
plt.xlabel('Yearly Salary($USD)')
```

## Result

![Salary Analysis for jobs in US](Project_01\Images\salary_analysis.png)

## Insights 


- Senior Data Scientist

> Median Salary: The median salary is quite high, indicating that Senior Data Scientists are well-compensated.

> Salary Range: The interquartile range (IQR) is wide, with the upper quartile extending significantly, suggesting that there are a number of very high earners in this role.

- Senior Data Engineer

> Median Salary: Slightly lower than Senior Data Scientists, but still very competitive.

> Salary Range: Similar to Senior Data Scientists, the IQR is broad, showing substantial variability in earnings.

- Data Scientist

> Median Salary: Lower than Senior positions but still solid, reflecting the importance of this role in analytics.

> Salary Range: The range is narrower compared to Senior roles, indicating more consistency in salaries.

- Data Engineer

> Median Salary: Comparable to Data Scientists, with slight variations.

> Salary Range: The IQR is similar to Data Scientists, suggesting a stable salary range for this role.

- Senior Data Analyst

> Median Salary: Lower than Data Scientists and Engineers, but higher than regular Data Analysts.

> Salary Range: A moderate range, showing less variability compared to senior technical roles.

- Data Analyst

> Median Salary: The lowest among the listed roles, reflecting the entry-level nature of this position.

> Salary Range: The narrowest range, suggesting consistent earnings for Data Analysts across different organizations.

## Conclusion


The box plot reveals a clear hierarchy in salaries within the data field, with senior roles commanding higher pay and wider salary ranges. This indicates that experience and advanced expertise are highly valued. Data Analysts have the most consistent earnings, while higher-level roles like Senior Data Scientist and Senior Data Engineer show more variability, likely due to bonuses, stock options, and other compensation benefits at higher experience levels.


# 4. How well do jobs and skills pay for Data Analysts?

## Highest paid and most demanded skills for Data Analysts in US

# Visualize

```python
fig, axs = plt.subplots(2, 1, figsize=(10, 7))
sns.set_theme(style="ticks")

sns.barplot(data=df_DA_top_pay, x='median', y='job_skills', ax=axs[0], hue='median', palette='dark:g_r')
axs[0].legend().remove()
axs[0].set_title('Highest Paying Jobs')
axs[0].set_xlabel('Median Yearly Salary')
axs[0].set_ylabel('')
axs[0].xaxis.set_major_formatter(plt.FuncFormatter(lambda x, _:f'${int(x/1000)}K'))

sns.barplot(data=df_DA_skills, x='median', y='job_skills', ax=axs[1],hue='median', palette='light:g')
axs[1].legend().remove()
axs[1].set_title('Jobs with the most counts')
axs[1].set_xlabel('Median Yearly Salary')
axs[1].set_ylabel('')
axs[1].xaxis.set_major_formatter(plt.FuncFormatter(lambda x, _:f'${int(x/1000)}K'))
axs[1].set_xlim(axs[0].get_xlim())

plt.suptitle('Job Salary Analysis')
plt.tight_layout()
```

# Results

![Highest paid and most demanded skills for Data Analysts in US](Project_01\Images\Highest_paid_and_most_demanded_skills_for_Data_Analysts_in_US.png)


## Insights

- Highest Paying Jobs

> dplyr: One of the highest paying jobs, with a median yearly salary approaching $200K.

> bitbucket: Also high on the list, offering competitive salaries.

> gitlab: Comparable to bitbucket, with substantial compensation.

> solidity: A well-compensated role, indicating high demand.

> hugging face: Commands a significant salary, reflecting its importance in the industry.

> couchbase: Offers lucrative pay, attracting skilled professionals.

> ansible: A highly paid position, indicating strong industry demand.

> mxnet: Also among the higher paying roles, showing its value.

> cassandra: Provides competitive salaries, a sign of its critical role.

> vmware: Well-compensated, indicating a valuable skill set.

- Jobs with the Most Counts

> python: Highly counted and well-compensated, showing its ubiquity and importance.

> tableau: Frequently required, with a solid median salary.

> r: Commonly listed, offering competitive pay.

> sql server: In high demand, reflecting its critical role in data management.

> sql: Widely needed and well-paid, showing its foundational importance.

> sas: Frequently listed, with substantial compensation.

> power bi: Commonly required, reflecting the demand for data visualization skills.

> powerpoint: Often needed, with a reasonable median salary.

> excel: Highly counted and essential, offering solid pay.

> word: Frequently listed, indicating its broad utility.

## Conclusion


The box plot reveals a clear distinction between the highest paying jobs and those with the most counts. Skills like dplyr, bitbucket, and gitlab command top salaries, indicating their specialized and high-demand nature. On the other hand, foundational skills like python, tableau, and sql are widely required and offer competitive compensation, reflecting their critical role in data-related fields.


# 5. What is the most optimal skill to learn as a Data Analyst?

## Most optimal skills for a Data Analyst in US

## Visualize

```python
from adjustText import adjust_text
from matplotlib.ticker import PercentFormatter

sns.scatterplot(
    data=df_plot,
    x='percent',
    y='median_salary',
    hue='technology'
)
sns.set_theme(style='ticks')
sns.despine()
plt.title('Most optimal skills for a Data Analyst in US')
plt.xlabel('Percent of Data Analyst jobs')
plt.ylabel('Median yearly salary')

texts =[]
for i, txt in enumerate(df_plot['skills']):
    texts.append(plt.text(df_plot['percent'].iloc[i],df_plot['median_salary'].iloc[i], txt))

adjust_text(texts, arrowprops=dict(arrowstyle='->', color='blue'))

ax = plt.gca()
ax.yaxis.set_major_formatter(plt.FuncFormatter(lambda y, _:f'${int(y/1000)}K'))
ax.xaxis.set_major_formatter(PercentFormatter(decimals=0))

plt.tight_layout()
plt.show()
```

## Results

![Most Optimal Skills For A Data Analyst in US](Project_01\Images\Most_optimal_skills_For_Data_analyst_in_US.png)


## Insights

### High Salary and Demand


> - Python: As a programming skill, Python is associated with the highest median yearly salary (around $98K) and is required in about 30% of Data Analyst jobs. This highlights Python's value in the industry for tasks like data analysis, automation, and machine learning.

> - SQL: SQL is in the highest demand, required in approximately 55% of Data Analyst jobs, with a median yearly salary of about $90K. This indicates SQL's essential role in database management and querying.

### High Salary, Lower Demand

> - Oracle: Although Oracle is required in only about 15% of Data Analyst jobs, it offers a high median yearly salary (~$96K). This suggests that while not as widely required, expertise in Oracle is highly valued and can command a premium.

### Moderate Salary and Demand

> - Excel: Excel is required in about 45% of Data Analyst jobs with a median yearly salary of around $86K. Despite being a fundamental skill, its median salary is slightly lower compared to other skills, reflecting its widespread use and lower learning curve.

> - Power BI and SAS: Both skills have similar median yearly salaries (~$90K) and are required in about 20% of Data Analyst jobs. This indicates a balanced demand and compensation for these data visualization and analytics tools.

### Lower Salary and Demand

>  * Word: Word is associated with the lowest median yearly salary (around $82K) and is required in about 10% of Data Analyst jobs. While useful, it is not a core technical skill for data analysis, thus reflecting its lower demand and compensation.

## Conclusion


This scatter plot provides a clear perspective on the most optimal skills for Data Analysts in the US. Python and SQL stand out as the most valuable skills in terms of both demand and salary. Excel remains a critical tool but offers slightly lower compensation. Specializing in tools like Power BI, SAS, and Oracle can lead to higher salaries, although they are less frequently required. Understanding these trends can help aspiring Data Analysts prioritize their skill development to maximize their job prospects and earning potential.