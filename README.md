# Masters Eligibility Analytics Dashboard
Developed an interactive Power BI dashboard to streamline candidate eligibility assessment for a Master's degree admissions process. Performed extensive data cleaning, transformation, and modeling using Power Query and DAX, including eligibility classification, post-qualifying experience calculation, and qualification categorization. Designed interactive dashboards with slicers, maps, treemaps, funnel charts, and drill-down visualizations to provide actionable insights into applicant qualifications, experience, geographic distribution, and admission eligibility.

## Data Cleaning, Transformation & Data Modeling

The raw candidate dataset contained semi-structured information related to academic qualifications, professional experiences, and applicant details. Extensive data preparation was performed using **Power Query** and **DAX** to transform the raw data into an analysis-ready format for eligibility assessment.

### 1. Data Cleaning and Preparation using Power Query

The initial dataset contained nested academic and experience details stored as text strings. Power Query was used to extract, clean, and restructure this information into meaningful attributes.

#### Academic Qualification Data Transformation
- Split nested qualification records using delimiters to separate individual academic qualifications.
- Extracted key attributes including:
  - Institute name
  - Qualification/Degree name
  - Qualification start date
  - Qualification completion date
  - Degree classification/grade
- Removed unnecessary prefixes, symbols, brackets, and empty columns generated during splitting.
- Renamed columns systematically (e.g., Qualification 1, Institute 1, From(Q1), To(Q1), Grade(Q1)) to improve readability and maintain a structured format.

#### Professional Experience Data Transformation
- Extracted experience-related information from nested text fields by separating:
  - Company name
  - Job position
  - Employment start date
  - Employment end date
- Standardized experience columns using a consistent naming convention:
  - Company 1, Company 2, ...
  - Position 1, Position 2, ...
  - From(P1), To(P1), ...

#### Data Standardization and Quality Improvements
- Converted text fields into a consistent sentence-case format to improve readability.
- Replaced missing categorical values with "Undefined" to maintain data completeness.
- Removed duplicate records to improve data accuracy.
- Standardized variations of institution and qualification names:
  - Unified different naming formats of professional bodies such as CA Sri Lanka, CIMA, CMA, CIPM, and AAT.
  - Standardized university names and degree titles for consistent categorization.
- Applied grouping techniques to classify:
  - Academic institutions
  - Degree classifications
  - Qualification types

---

## 2. Data Transformation and Feature Engineering using DAX

Calculated columns and measures were created using DAX to generate business rules required for candidate evaluation.

### Qualification Duration Calculation
Calculated the duration of each qualification by comparing qualification start and completion dates.

**Purpose:**
- Identify degree duration (3-year, 4-year, honors degree).
- Support eligibility classification logic.

Example:
Qualification Duration =DATEDIFF(Start Date, End Date, YEAR)

### Eligibility Category Classification

A rule-based classification model was developed to categorize qualifications based on academic level, duration, and institution.

The classification logic included:

- **Honors Degree**
  - Qualification contains "Hons"
  - Duration is equal to or greater than 4 years

- **4-Year Degree**
  - Degree duration is 4 years or above

- **3-Year Degree**
  - Qualification duration is 3 years
  - Recognized professional degree pathways such as CIMA

- **Professional Qualification**
  - Qualifications from recognized professional institutes such as CA, CIM, and CIPM

- **Other / Undefined**
  - Qualifications that did not match predefined categories

This created structured eligibility categories for each qualification (Eligibility Category Q1, Q2, etc.).

---

## 3. Post-Qualifying Experience Calculation

A major requirement of the eligibility assessment was calculating professional experience gained after completing the candidate's qualification.

### Effective Qualification Completion Date
The earliest completed qualification date was identified using DAX by comparing multiple qualification completion dates.

This effective date was used as the starting point for calculating relevant professional experience.

### Position Duration Calculation
For each employment record:

- Checked whether employment started after qualification completion.
- Calculated experience duration until:
  - Employment end date, or
  - The evaluation reference date if the candidate was still employed.

Calculated experience was stored as:

- PositionDuration(P1)
- PositionDuration(P2)
- PositionDuration(P3)

### Total Post-Qualifying Experience

Individual employment durations were aggregated to calculate the total professional experience after qualification.
PostQualifyingExperience =SUM(Position Duration Columns)

This metric was used as a key factor in determining eligibility.

---

## 4. Candidate Eligibility Decision Model using DAX

A comprehensive eligibility framework was developed based on academic qualifications and professional experience.

Candidates were classified into:

| Category | Criteria |
|---|---|
| Direct Eligibility (Category 1) | Honors Bachelor's degree in Business from University of Moratuwa |
| Direct Eligibility (Category 2) | Four-year Business/related degree |
| Eligible with Experience (Category 3) | Four-year non-business degree with relevant experience |
| Eligible with Experience (Category 4) | Three-year degree with required work experience |
| Eligible (Category 5) | Recognized professional qualification with experience |
| Special Admission (Category 6) | Senior managers and entrepreneurs |
| Not Eligible | Does not satisfy admission requirements |

A final eligibility status column was created:

- Eligible
- Not Eligible

---

## 5. Qualification Type and Institute Classification

Additional calculated categories were created to support dashboard analysis:

### Degree Type Classification
Qualifications were grouped into:

- Business / Management
- Non-Business
- Professional Qualification
- Non-Degree
- Undefined

### Institute Location Classification
Institutes were categorized geographically by:

- City
- Country

This enabled geographic analysis of applicant backgrounds.

## Data Modeling Outcome

After completing the transformation process, the raw dataset was converted into a structured analytical model containing:

- Cleaned candidate profiles
- Standardized qualifications
- Categorized academic backgrounds
- Calculated professional experience
- Automated eligibility decisions

The prepared dataset enabled the development of an interactive Power BI dashboard for admission analysis and data-driven decision-making.
