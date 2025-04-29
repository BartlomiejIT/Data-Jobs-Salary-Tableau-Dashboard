# Data Jobs Salary Dashboard - Tableau 

![image](https://github.com/user-attachments/assets/f3b9e493-e78d-4bfd-9a7d-f7ff5fcf866a)

---

## Table of Contents
- [Overview](#overview)
- [Key Features](#key-features)
- [Tools](#tools)
- [Data Source](#data-source)
- [Dashboard Components](#dashboard-components)
- [Technical Implementation](#technical-implementation)
- [Interactivity Features](#interactivity-features)
- [Design Considerations](#design-considerations)
- [Usage](#usage)
- [Conclusion](#conclusion)


## Overview

Interactive Tableau dashboard analyzing global salary trends, job distribution, and platform popularity for data-related positions. Enables data-driven career decisions through comparative insights across countries, job titles, and employment types.

---

## Key Features

- 🌍 Interactive choropleth world map with salary heatmap
- 📊 Comparative salary analysis by job title
- 🔍 Dynamic filtering by country and employment type
- 📈 Real-time KPI updates
- 📱 Responsive design

---

## Tools

- **Tableau Public**: Design, build, and publish interactive dashboards.

- **Microsoft Excel**: Clean, transform, and validate raw salary data in .xlsx format.

- **Markdown**: Documentation formatting for README and project overview.

---

## Data Source

`data_job_salary.xlsx` containing:
- 5,000+ job records
- 15+ data-related job titles
- 50+ countries worldwide
- Annual salary averages in USD
- Job platform metadata

---

## Dashboard Components

### Median Salary by Job Title
   **Sheet**: `Median Salary by Job Title`:
   
   ![image](https://github.com/user-attachments/assets/cb9407e1-fde8-497a-a3ba-6d035dbe1722)

   - **Type**: Horizontal bar chart
   - **Metric**: Median of [Salary Year Avg]
   - **Purpose**: Compare median annual salaries across different job titles.

---
   
### Map of Median Salaries by Country
   **Sheet**: `Map - Job Country`:
   
![image](https://github.com/user-attachments/assets/59330309-5253-4244-aaa7-b70f7f34d2bd)

   - **Type**: Choropleth map
   - **Metric**: Median of [Salary Year Avg]
   - **Purpose**: Visualize salary variation across countries.

---

### Job Count by Type
   **Sheet**: `Chart - Schedule Type`:
   
   ![image](https://github.com/user-attachments/assets/a297cbb1-6c25-4692-8423-da60a4493d4d)
   
   - **Type**: Horizontal bar chart
   - **Metric**: Count of postings grouped by [Job Schedule Type]
   - **Filters**: Exclude null schedule types; apply top N filter by median salary.
   - **Purpose**: Analyze which schedule types are most common and their salary ranges.

---

### Median Salary
**Sheet**: `KPI - Median Salary`

  - **Metric**:
  ```Tableau
  // Median aggregation of Salary Year Avg
  MEDIAN([Salary Year Avg])
  ```
  - **Purpose**: Display the median annual salary for the selected filters, providing a quick overview of central salary tendency.

---

### Top Job Platform
   **Sheet**: `KPI - Top Platform`:

   #### Key Calculated Metrics / Fields:
   1. **Platform Job Count**  
      ```tableau
      // Number of postings per platform
      COUNT([Job Title Short])
      ```
   2. **Max Count by Country**  
      ```tableau
      // Highest posting count within selected country
      { FIXED [Job Country] : MAX([Platform Job Count]) }
      ```
   3. **Top Platform by Country**  
      ```tableau
      // Platform(s) matching the max count
      IF [Platform Job Count] = [Max Count by Country]
      THEN [Clean Job Platform]
      END
      ```
   4. **Top Platform Global**  
      ```tableau
      // Highest posting count across all countries
      { FIXED : MAX([Platform Job Count]) }
      ```
   5. **Top Platform Combined**  
      ```tableau
      // Use country‐level if available, else global
      IFNULL([Top Platform by Country], [Clean Job Platform])
      ```
   - **Purpose**: Identify the platform with the highest number of job postings, either within the selected country or globally.

---

### Job Schedule Type Count
   **Sheet**: `KPI - Job Count`:
   
   - **Visualization**: KPI showing total job postings by schedule type.  
   - **Metric**:
     ```tableau
     // Count of distinct job postings
     COUNT([Job Title Short])
     ```
   - **Purpose**: Display total number of job postings based on current filters.

---

## Technical Implementation

- **Data Aggregation**: Utilizes Tableau's built-in median aggregation and Level of Detail (LOD) expressions.

- **Calculated Fields**: Custom LOD expressions for platform analysis and KPI metrics.

- **Layout**: Floating containers and grid layout for precise alignment.

- **Performance**: Context filters optimize query performance for large datasets.

---

## Interactivity Features

- **Filters**: Country, Job Title, and Schedule Type filters influence all dashboard components.

- **Actions**:

   - **Map** → **All Sheets**: Clicking a country updates KPIs and charts.
   
   - **Bar Charts** → **KPIs**: Selecting a bar filters KPI panels accordingly.

---

## Design Considerations

- Minimalist color palette and typography for clarity.

- Hidden headers and axes on KPI sheets to reduce visual noise.

- Consistent spacing and container styles for a cohesive look.

--- 

## Usage

1. Open Data Jobs Salary Dashboard.twbx in Tableau Public.

2. Connect to data_job_salary.xlsx.

3. Use the filters panel to refine your analysis.

4. Hover or click on elements to view detailed tooltips and update KPIs.

---

## Conclusion
This Tableau dashboard empowers users to explore salary distributions, platform popularity, and job counts across countries and job types, showcasing advanced use of LOD expressions, table calculations, and interactive dashboard actions in Tableau.
