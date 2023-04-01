---
title: "Transitioning from Drag-and-Drop to Code-based Data Visualization with GPT -- DRAFT"
author: Abigail Haddad
date: "2023-03-26"
---


# Cutting the Learning Curve with GPT

- GPT reduces the barriers to entry for code-based data visualization
- Assists users at every step, from data cleaning to app development
- Accelerates the learning process by providing code, but also it can explain to you what it's doing

---

# Why Transition to Coding for Data Visualization?

- Reusability: Code-based solutions make it easier to reuse and repurpose code for visualizations, saving time and effort. Example: Create a custom library/module for your organization's preferred graph style, easily share it, and update it as needed.
- Version control: Track changes and maintain a clear history of your work, facilitating collaboration, tracking changes, and being able to revert when you break stuff.
- Transparency and documentation: Coding lets you and others see what you've done, reducing the "black box" effect. More trustworthy and easier to build on.
- Separation of data and code: Keep your data and visualization code separate, making it easier to update and manage access to

---

# Overview of Data Visualization Ecosystems in Python and R

- Python libraries: Matplotlib, Seaborn, Plotly, Dash, Bokeh, Altair, Geopandas (for mapping)
- R libraries: ggplot2, Shiny, Plotly, lattice, leaflet (for mapping)
- Dashboards: Streamlit (Python), Flask (Python), Shiny (R)
- Both ecosystems provide powerful tools for creating static, interactive, and web-based visualizations, including mapping

---

# Data Cleaning and Input with GPT-generated Code

- GPT can generate code to import, filter, and preprocess data for your specific visualization needs
- Doing this via coding lets you scale with fewer errors -- for instance, if we have many files with similar structure, we can read in and aggregate them all at once
- This also makes it easier to update your visualizations when your data updates in an automated way (for instance, by having your figure titles reflect the most recent data)

---

# Example Prompting: Data Cleaning and Input

- "I am going to ask for your help writing R code. I am new to writing in R, but I want to do a good job. I want to have code that is documented, in functions, conforms to R coding standards. I want to write code that Hadley Wickham would approve of. I also want to you explain to me what it's actually doing so I can learn from it. Let's start. I want to automate downloading this file, unzipping it, and putting it into a dataframe or table or whatever: https://datasets.imdbws.com/name.basics.tsv.gz"
- "thanks. I want to generate a table with this data. this is how it's structured. name.basics.tsv.gz – Contains the following information for names:
nconst (string) - alphanumeric unique identifier of the name/person
primaryName (string)– name by which the person is most often credited
birthYear – in YYYY format
deathYear – in YYYY format if applicable, else '\N'
primaryProfession (array of strings)– the top-3 professions of the person
knownForTitles (array of tconsts) – titles the person is known for ; I want to pull first names out of the nconst field (I guess by splitting it and taking the first part?), put those in a field called "firstName", and then I want to create a new table/dataframe that aggregates to get counts of each firstName"
- "this is taking a long time to run. is there a faster way? like the equivalent of "apply" in python?"

---

# Generating Code for Graphs from Descriptions

- Input a text description of the desired graph or chart
- GPT outputs code for the specified visualization using libraries like matplotlib, seaborn, or plotly/dash
- Example: "Create a line chart showing the monthly revenue of an online store from January 2022 to December 2022"
- You can customize your formatting extensively, although it may not get everything correct immediately

---

# Example Prompting: Graphs

- "can you suggest some graphs for showing the top names in terms of counts, and then write me code for them?"
- "I want to make some formatting changes. I want the number labels to either be formatted with commas, or if there's some automated way that it can look at the numbers and determine a good unit -- like "thousands" or "millions", that would be cool. I'd also like times new roman for the whole thing"
- "15: In grid.Call(C_textBounds, as.graphicsAnnot(x$label),  ... : font family not found in Windows font database"
- [picture of output]

---
# Learning and Debugging with GPT

- GPT writes high-quality code and explains its functionality, helping users learn best practices
- GPT assists with debugging by interpreting error messages and suggesting solutions
- Shortens the process of fixing issues and improves code quality

---

# Example Prompting: Learning and Debugging

- "great. now I want a graph showing the most popular female name by birthYear. Can you suggest some different formats?"
- "analyze_name_basics(name_basics_data, top_n, top_n_women), Error in arrange(., desc(count)) : object 'first_name_counts' not found"

---

# App Development Assistance through GPT-generated Code

- GPT can also reduce the learning curve/write you code for creating interactive dashboards
- It can write you code, but also walk you through processes like where and how to deploy an app
- [slide with example of prompts/responses]

---

# Conclusion

- Transitioning from drag-and-drop tools to code-based data visualization opens up new possibilities
- Python and R ecosystems provide a wide array of libraries and frameworks for creating powerful visualizations, including mapping
- GPT is a valuable assistant throughout the entire process, from data cleaning to app development

---

# Questions and Discussion
