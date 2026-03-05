# The Analysis
##  What are the most demanded skills for the top 3 popular data roles?

To find the most demanded skills for the top three data roles, I first identified which jobs are the most popular. Then I selected the top five skills required for each of these roles.

This analysis shows the most common job titles and their key skills, helping me understand which skills I should focus on learning depending on the role I want to pursue.

You can view my notebook with the detailed steps here:
[2_Skill.ipynb](3_Project_overview/2_Skill.ipynb).

### Visualize data
```Python
fig, ax = plt.subplots(len(job_titles), 1)

sns.set_theme(style='ticks')

for i, job_title in enumerate(job_titles):

    df_plot = df_skills_perc[
        df_skills_perc['job_title_short'] == job_title
    ].head(5)

    sns.barplot(
        data=df_plot,
        x='skill_percentage',
        y='job_skills',
        ax=ax[i],
        hue='skill_count',
        palette='dark:b_r'
    )

    ax[i].set_title(job_title)
    ax[i].set_ylabel('')
    ax[i].set_xlabel('')
    ax[i].get_legend().remove()
    ax[i].set_xlim(0, 78)

    for n, v in enumerate(df_plot['skill_percentage']):
        ax[i].text(v + 1, n, f'{v:.0f}%', va='center')

    if i != len(job_titles) - 1:
        ax[i].set_xticks([])

fig.suptitle('Likelihood of Skills Requested in US Job Postings', fontsize=15)
fig.tight_layout(h_pad=0.5)  #  overlap
plt.show()
```

### Result
Most demanding jobs

![Visualize plot of three most demanding skills](3_Project_overview/Images/3_most_demand_skill.png)


# Data Analyst Skills: Salary vs Demand

This project shows the difference between highest paid skills and most in-demand skills for data analysts.

## Top 10 Highest Paid Skills

The first chart shows the skills that give the highest median salary.
Some of these skills are dplyr, Bitbucket, GitLab, Solidity, Hugging Face, Couchbase, and Ansible.

These skills can give higher salaries (around $150K–$200K), but they are not always required in many data analyst jobs because they are more specialized tools.

## Top 10 Most In-Demand Skills

The second chart shows the skills that appear most often in data analyst job postings.

Some of the most common skills are Python, Tableau, R, SQL Server, SQL, Power BI, Excel, and PowerPoint.

These are basic and important skills that most companies expect from a data analyst.

Check the whole in here along with diffrent style visualized charts:[20_Seaborn_intro.ipynb](2_Advanced/20_Seaborn_intro.ipynb).

### Visualize data

```Python

sns.set_theme(style="ticks")

fig, ax = plt.subplots(2, 1, figsize=(8, 6))

# Top 10 Highest Paid Skills
sns.barplot(
    data=df_DA_top_pay,
    x='median',
    y=df_DA_top_pay.index,
    ax=ax[0],
    hue='median',
    palette='dark:b_r',
    legend=False
)

ax[0].set_title('Top 10 Highest Paid Skills for Data Analysts')
ax[0].set_ylabel('')
ax[0].set_xlabel('')
ax[0].xaxis.set_major_formatter(
    plt.FuncFormatter(lambda x, _: f'${int(x/1000)}K')
)


# Top 10 Most In-Demand Skills
sns.barplot(
    data=df_DA_skills,
    x='median',
    y=df_DA_skills.index,
    ax=ax[1],
    hue='median',
    palette='dark:b_r',
    legend=False
)

ax[1].set_title('Top 10 Most In-Demand Skills for Data Analysts')
ax[1].set_ylabel('')
ax[1].set_xlabel('Median Salary (USD)')

# Make both plots share same x-axis scale
ax[1].set_xlim(ax[0].get_xlim())

ax[1].xaxis.set_major_formatter(
    plt.FuncFormatter(lambda x, _: f'${int(x/1000)}K')
)

plt.tight_layout()
plt.show()

```

### Result

![Salary based on skills](3_Project_overview/Images/Analytics_with_seaborn.png).

# Key Insights

1. Python Dominates Technical Roles
Python is one of the most important programming languages in the data field. It is required across all three roles — Data Analyst, Data Scientist, and Data Engineer. However, the demand is highest for Data Scientists (72%) and Data Engineers (65%), showing its strong importance in advanced data work as shown in [2_Skill.ipynb](3_Project_overview/2_Skill.ipynb).

2. SQL is Essential for Data Analysis
SQL is the most commonly requested skill for Data Analysts and Data Scientists. It appears in more than 50% of job postings, highlighting the importance of database querying and data extraction in these roles.

3. Python is Critical for Data Engineering
For Data Engineers, Python appears in 68% of job postings, making it the most demanded skill. This reflects the role of Python in data pipeline development, automation, and large-scale data processing.

4. Core Skill Foundation in Data Careers
Overall, Python and SQL form the core skill foundation across most data-related roles, while the specific tools vary depending on the responsibilities of each role.

### Conclusion:
These insights highlight the key skills required in the data industry and show how different roles emphasize different technologies, from analysis tools to large-scale data infrastructure.