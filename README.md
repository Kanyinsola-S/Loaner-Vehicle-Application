# Loaner-Vehicle-Application & Inventory
A ServiceNow App that automates the process of requesting vehicles from the warehouse.

## Table of Contents
## 📑 Table of Contents
- [Sprint 1 – MVP Development](#sprint-1--mvp-development)
- [Sprint 2 – Feature Enhancement](#sprint-2--feature-enhancement)
- [Sprint 3 – Portal Design and Finalization](#sprint-3--portal-design-and-finalization)
- [Testing](#testing)
- [Problems Encountered](#problems-encountered)
- [Lessons Learned](#lessons-learned)
- [Next Steps](#next-steps)


## Sprint 1 – MVP Development
Sprint Goal: Build the foundational structure and critical backend components for managing vehicle loaning, tracking, and servicing using ServiceNow’s Scoped Application framework.

**Overview:**
The primary objective of Sprint 1 was to set up the Loaner Vehicle Request and Inventory application as a standalone scoped app in ServiceNow. This included defining tables, forms, user roles, navigation modules, importing data, and configuring necessary form behaviors to ensure the system supports the basic vehicle lending process.

**Completed User Stories & Features:**
1. Scoped Application Setup
Created a new scoped application titled Loaner Vehicle Request and Inventory to isolate the logic and data structures from other ServiceNow modules.
Set application prefix, advanced settings, and created a custom role lva_user for table access management.

![image](https://github.com/user-attachments/assets/5298ab2d-73ec-46a3-9890-007968715487)


2. Update Set Configuration
Established a dedicated Update Set to track all configuration changes made within this application scope, enabling version control and deployment portability.
![image](https://github.com/user-attachments/assets/c5d97a0b-f2af-44e6-a610-32d0e61aae83)

3. Loaner Vehicle Catalog Table and Form
Created a custom table called Loaner Vehicle Catalog to store information about available vehicles.
Enabled auto-numbering and applied lva_user access.
Added fields and Adjusted field layout for optimal form usability
![image](https://github.com/user-attachments/assets/8ee57a08-e2b6-42a9-8d36-bc9c2604ec83)

4. Application Menu & Navigation Modules
Created an Application Menu for easy access.
Defined modules:
Create New – opens new form
All – shows list of all vehicle catalog records
Ensured navigation reflects consistent UI/UX standards.
![image](https://github.com/user-attachments/assets/e842233e-4f02-491c-a53b-4542028839cc)

5. Data Import (Vehicle Catalog)
Imported vehicle data using Import Sets and Transform Maps, then successfully populated the Loaner Vehicle Catalog table excel file. Manually attached images to each record post import.
![image](https://github.com/user-attachments/assets/10f900c7-57e5-4423-bded-6b1dd9adee6a)








