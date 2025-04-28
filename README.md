# Data Jobs Salary Dashboard

![image](https://github.com/user-attachments/assets/aacec42a-3525-4e5f-b16e-7de2b438df85)

---

## Table of Contents
1. [Introduction](#introduction)
2. [Workbook File](#workbook-file)
3. [Dashboard Overview](#dashboard-overview)
   - [Median Salary by Job Title](#median-salary-by-job-title)
   - [Map of Median Salaries by Country](#map-of-median-salaries-by-country)
   - [Job Schedule Type Count](#job-schedule-type-count)
   - [Top Job Platform](#top-job-platform)
4. [Interactivity](#interactivity)
5. [Design Choices](#design-choices)
6. [Conclusion](#conclusion)

## Introduction
This interactive dashboard, built entirely in **Tableau Public**, provides insights into data science job salaries, platform distribution, and job counts across different countries and job types.

- **Tool Used**: Tableau Public  
- **Data Source**: `data_job_salary.xlsx`

---

## Workbook File
The final Tableau workbook is available as **`Data Jobs Salary Dashboard.twbx`**.

---

## Dashboard Overview

### Median Salary by Job Title
**Sheet**: `Median Salary by Job Title`:
   
   ![image](https://github.com/user-attachments/assets/de68e876-57c7-4c17-b5aa-27db9395a115)
   
   - **Visualization**: Horizontal bar chart of median annual salaries for each job title.  
   - **Calculation**: Default Tableau median aggregation on `[Salary Year Avg]`.
   
### Map of Median Salaries by Country
**Sheet**: `Map - Job Country`:
   
   ![image](https://github.com/user-attachments/assets/8f52869b-2721-498b-ae9a-dbb1d7480488)
   
   - **Visualization**: Choropleth world map showing median salaries by country.  
   - **Calculation**: Median aggregation on `[Salary Year Avg]` with geographic role on `[Job Country]`.

### Job Count by Type
**Sheet**: `Chart - Schedule Type`:
   
   ![image](https://github.com/user-attachments/assets/a297cbb1-6c25-4692-8423-da60a4493d4d)
   
   - **Visualization**: Horizontal bar chart of median annual salaries for each job schedule type.  
   - **Calculation**: Median aggregation on `[Salary Year Avg]` grouped by `[Job Schedule Type]`.  
   - **Filters**:
     - Exclude NULL schedule types.  
     - Display certainly schedule types by median salary via Top filter.

### Job Schedule Type Count
**Sheet**: `KPI - Job Count`:
   
   - **Visualization**: KPI showing total job postings by schedule type.  
   - **Calculation**:
     ```tableau
     // Count of distinct job postings
     COUNT([Job Title Short])
     ```

### Top Job Platform
**Sheet**: `KPI - Top Platform`:

   #### Key Calculated Fields
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

---

## Interactivity

- **Context Filters**: `Job Country`, `Job Schedule Type`, and `Job Title Short` are added to Context so that table calculations respect user selections.  
- **Dashboard Actions**:  
  - **Map → KPI**: Selecting a country on the map filters all related sheets and updates the **Top Job Platform** KPI.  
  - **Bar Charts → Other KPIs**: Selecting bars on salary or schedule charts updates the corresponding KPI boxes.

---

## Design Choices

- **Grid Layout**: Enabled grid in Dashboard view (Dashboard → Show Grid) for precise alignment of charts and KPI boxes.  
- **Clean KPI Panels**: Hidden axis headers and sheet titles on KPI sheets to focus attention on key metrics.  
- **Floating Containers**: Used floating containers to position KPI boxes exactly.

---

## Conclusion
This Tableau dashboard empowers users to explore salary distributions, platform popularity, and job counts across countries and job types, showcasing advanced use of LOD expressions, table calculations, and interactive dashboard actions in Tableau.
