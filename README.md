# Analysis

## 1. What are the most demanded skills for the Top 3 most popular data roles?

To find the most demanded skills for the top 3 most popular data roles. I first filtered out the duplicated rows and found out the 3 most popular data roles. Next I filtered out the top 5 skills for these 3 roles. This query highlights the most popular job titles and their top skills, showing which skill I should pay attention to depending on the role I'm interested in.

View my notebook with detailed steps here:
[2_Skills_Counting.ipynb](Project\2_Skills_Counting.ipynb)


### Visualize data

```python
fig, ax = plt.subplots(len(Top_3),1)
sns.set_theme(style='ticks')

for i, title in enumerate(Top_3):
    skills = df_skills_percent[df_skills_percent['job_title_short']==title].head(5)
    # skills.plot(kind='barh', ax=ax[i], x='job_skills', y='percent', title=title)
    sns.barplot(data=skills, ax=ax[i], x='percent', y='job_skills', hue='percent', palette='dark:b_r')
    ax[i].legend().set_visible(False)
    ax[i].set_title(title)
    ax[i].set_xlim(0, 80)
    # ax[i].invert_yaxis()
    ax[i].set_ylabel("")
    ax[i].set_xlabel("")
    if i != len(Top_3)-1:
        ax[i].set_xticks([])

    for n,v in enumerate(skills['percent']):
        ax[i].text(v+1,n,f'{v:.0f}%',va='center')

fig.suptitle('Likelihood of Skills Requested in US Job Postings', fontsize=15)
fig.tight_layout(h_pad=0.5)
```

### Results

![Visualization of Top Skills](Project\Images\SkillDemand.png)

### Insights
- Python is a versatile skill, highly demanded across all three roles, but most prominently for Data Scientists (69%) and Data Engineers (63%).
- SQL is the most requested skills for Data Analyst (50%) and Data Engineers (67%). It is also highly demanded for Data Scientist (50%).
- Data Engineers require more specialized technical skills (AWS, Spark, Azure) compared to Data Analysts and Data Scientists who are expected to be more proficient in data management and analysis tools (Excel, Tableau).


## 2. How are in-demand skills trending for Data Analysts?

### Visualize Data

```python

from matplotlib.ticker import PercentFormatter
sns.lineplot(data=df_plot, dashes=False, palette='tab10')
sns.set_theme(style='ticks')
sns.despine()

plt.title('Trending Top Skills for Data Analysis in US')
plt.ylabel('Likelihood in Job Postings')
plt.xlabel('2023')
plt.legend().remove()

ax = plt.gca()
ax.yaxis.set_major_formatter(PercentFormatter(decimals=0))

plt.show()


```

### Results

![Trending top Skills for Data Analysts in the US](Project\Images\Skill_Trend_DA.png)

### Insights:

- SQL remains the most consistently demanded skills through the year, although it shows a gradual decrease in demand.
- Excel experienced a decrease from September to November, but it is the second most demanded skills over the year.
- Tableau and Python shows a relatively stable demand through the year with some fluctuations, but they remain the essential skills for DA. Sas while less demanded than others, shows a slightly downward trend through the year. 