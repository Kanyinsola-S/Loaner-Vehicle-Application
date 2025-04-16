# Loaner-Vehicle-Application & Inventory
A ServiceNow App that automates the process of requesting vehicles from the warehouse.

## Table of Contents
- [Sprint 1 – MVP Development](#sprint-1--mvp-development)
- [Sprint 2 – Feature Enhancement](#sprint-2--feature-enhancement)
- [Sprint 3 – Portal Design and Finalization](#sprint-3--portal-design-and-finalization)
- [Tech Stacks](#Tech-Stacks)
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

4. Loaner Vehicle Catalog Table and Form
   
Created a custom table called Loaner Vehicle Catalog to store information about available vehicles.
Enabled auto-numbering and applied lva_user access.
Added fields and Adjusted field layout for optimal form usability
![image](https://github.com/user-attachments/assets/8ee57a08-e2b6-42a9-8d36-bc9c2604ec83)

6. Application Menu & Navigation Modules
   
Created an Application Menu for easy access.
Defined modules:
Create New – opens new form
All – shows list of all vehicle catalog records
Ensured navigation reflects consistent UI/UX standards.
![image](https://github.com/user-attachments/assets/e842233e-4f02-491c-a53b-4542028839cc)

8. Data Import (Vehicle Catalog)
   
Imported vehicle data using Import Sets and Transform Maps, then successfully populated the Loaner Vehicle Catalog table excel file. Manually attached images to each record post import.
![image](https://github.com/user-attachments/assets/10f900c7-57e5-4423-bded-6b1dd9adee6a)

10. Vehicle Tracker Table and Form
    
Built the Vehicle Tracker table to monitor the loan process and vehicle status in the field.
Added Key fields and organized fields into logical form sections: Return Details and Activity.

![image](https://github.com/user-attachments/assets/6700bb43-89f0-4397-8f00-6b8c49f99707)

8. Vehicle Servicing Table and Form
   
Created a Vehicle Servicing table to track maintenance and repairs.
Added Key fields and organized fields into Forms and assigned a separate role for access management.

![image](https://github.com/user-attachments/assets/91c64c5d-d360-48e2-87d3-ce16e78c2015)

9.  Vehicle Tracker & Servicing  Modules
    
Added navigation modules for: All, Open, and Closed records
Ensured correct filtering based on Tracker Status and Ticket Status.

![image](https://github.com/user-attachments/assets/8cdba659-37fe-4058-b69f-e351e061910d)

10. Related Lists Configuration
    
Established related list relationships between:
Loaner Vehicle Catalog ↔ Vehicle Tracker
Loaner Vehicle Catalog ↔ Vehicle Servicing
Vehicle Tracker ↔ Vehicle Servicing

![image](https://github.com/user-attachments/assets/6ffe1098-c95a-494c-b52f-ccbd1b16aa98)

11. Form UI Policies
    
Added dynamic UI policies on the Vehicle Tracker form
Fields such as Assigned to, Location, and Expected Return Date are mandatory if Vehicle Status = Pending Release or Out on Field
Return Date, Return Status, and Return Notes become editable and mandatory when Vehicle Status = Returned for Inspection
![image](https://github.com/user-attachments/assets/19a9f698-682f-466d-b9a7-60a52fcb472a)

13. UI Actions (Custom Buttons)
    
Implemented two custom buttons on the Vehicle Tracker form:
Return to Warehouse – Updates status if vehicle is returned in good condition.
Send to Repair – Triggers servicing workflow if vehicle needs repairs.
Buttons are conditionally visible based on form values
![image](https://github.com/user-attachments/assets/de979650-e2c8-44a7-bc1b-feaa6d9f2b89)

15. Request Loaner Vehicle (Catalog Item Form)
    
Designed a Service Catalog item to allow users to request vehicles.
![image](https://github.com/user-attachments/assets/b9c3464c-cd73-4d48-95ba-7eb77d359532)


**Sprint Outcome:**
By the end of Sprint 1, we had a fully functioning MVP that:

-Captures and stores vehicles available for request

-Tracks loan requests and vehicle statuses

-Monitors servicing activities

-Enables users to request vehicles via the Service Portal


## Sprint 2 – Feature Enhancement 
Sprint Goal: Implement client-side validations, automate loaner vehicle request processing, and configure access controls and notifications for secure and seamless operation.

**Overview:**
The focus of Sprint 2 was to elevate the MVP by adding automation, validation, and security features. This sprint emphasized form behavior through client scripts, built a flow to manage loaner vehicle approvals and fulfillment, and introduced access control rules and notifications to support real-world operational use.

**Completed User Stories & Features:**
1. Client Scripts for Catalog Form
Implemented a client script to auto-fill the Office Location field based on the selected Requested For user.
Then Validation script to ensure the Return Date is not before the Date Needed. If the validation fails, the return date is cleared and an error message is shown.

![image](https://github.com/user-attachments/assets/0bab6f50-ef1c-4b72-a64c-8d4702873f8a)

3. Request Loaner Vehicle Flow
Flow Design: Built a ServiceNow Flow to trigger on submission of the catalog item "Request Loaner Vehicle."
Also created a Group Setup
THis was created to streamline task assignments, workflow routing, and role-based access. Two distinct groups were defined: **Loaner Vehicle Approvers (with the approver_user role)** to handle approval of vehicle requests, and **Loaner Vehicle Delivery (with the itil role)** to manage fulfillment tasks once approvals are granted. This setup ensures requests are reviewed and approved before being actioned.

To maintain clarity and prevent overlap, each user is assigned to only one group. This separation of duties supports a clean workflow process, simplifies permissions management, and ensures accountability across the approval and fulfillment stages.
![image](https://github.com/user-attachments/assets/358e695b-e85b-4c3d-a8ed-b64fc421f608)
![image](https://github.com/user-attachments/assets/f978c5da-b122-40ee-9191-eccb167a725d)


3. Access Control Rules (ACLs) and Groups
ACLs were implemented to ensure proper data security and role-based access within the Loaner Vehicle application.
The **Loaner Vehicle Catalog and Vehicle Tracker tables** allow all users to read data, but only users with the **lva_user role** can create or edit records, while deletion is restricted to **admins.**
For the Vehicle Servicing table, only users in the **Maintenance Team role** can read, create, or update records, and again, only admins can delete.
This setup ensures users can interact with the system based on their responsibilities without compromising data integrity.

New Roles & Groups:
To support role-based workflows, two specialized user groups were created. 
**Loaner Vehicle Warehouse Managers** were given full access to all three core tables—Catalog, Tracker, and **Loaner Vehicle Servicing** allowing them to oversee the end-to-end vehicle management process. 
Meanwhile, the Loaner Vehicle Maintenance Team was restricted to the Vehicle Servicing table, aligning their access strictly with repair and maintenance tasks. 
This clear separation of duties enforces accountability and prevents unauthorized actions across the application.
![image](https://github.com/user-attachments/assets/df406d5f-2721-4d20-b2f1-48258c829a14)

4. Notification Setup
A targeted notification was configured to enhance user communication in the loaner vehicle process. When a vehicle request (RITM) is marked as **Closed Complete** and the item is **Request Loaner Vehicle**, an automated email is sent to the original requester. The email reminds them to return the vehicle with the associated ticket number, reinforcing accountability and closing the loop on the loan process.

**Sprint Outcome:**
By the end of Sprint 2, the system could now:

- Validate input before submission to avoid errors

- Automatically create tracker records and route approvals

- Manage fulfillment through tasks

- Enforce table-level security

- Send closure-based notifications to keep users informed

## Sprint 3 – Portal Design and Finalization

**Sprint Goal:**
Automate key processes for better data synchronization and accountability while improving user interaction through a custom Service Portal.

**Overview:**
The focus of Sprint 3 was to strengthen backend automation and deliver a more user-friendly frontend experience. We introduced business rules that streamline vehicle status management and servicing workflows. Additionally, a basic Service Portal was developed to enhance visibility and accessibility of the loaner vehicle system for end users.

**Completed User Stories & Features:**
1. Business Rules
A series of business rules were implemented to automate vehicle status updates and servicing workflows.
The Vehicle Tracker table drives the status of the associated Loaner Vehicle Catalog record—marking it Unavailable during active use or servicing, Available when returned, and Decommissioned if retired.
When a vehicle is marked Sent for Servicing, the system checks for existing servicing tickets and auto-generates a new one if none exist, populating key details. To maintain process integrity, users are blocked from closing servicing tickets while the vehicle is still In Service.
Once servicing is complete and the ticket is closed, the system updates the Vehicle Tracker with the final status and closes the ticket record automatically.

5. Custom Service Portal Development
A simple Service Portal was built to provide a comprehensive list view of all Loaner Vehicles and their details and a widget that links directly to the Loaner Vehicle Request Catalog Item, allowing easy vehicle requests.

**Sprint Outcome:**
Sprint 3 delivered robust backend automation that ensures data consistency between vehicle records and servicing workflows. 
The initial version of the Service Portal boosts user engagement by offering a streamlined way to browse vehicles and submit loan requests.

**Additional Features (Backlog Items)**
These are not mandatory features but add-ons that can further improve the application. In Agile projects, we call these backlog items—ideas or enhancements that are valuable but not immediately prioritized for the main sprints. 
They can be picked up later based on time, capacity, or user feedback. Some of the proposed backlog features include:

Advanced dashboards and reporting for tracking vehicle usage and servicing trends

Knowledge Base integration for support and user self-service

Enhanced widgets and filters in the Service Portal for a smoother user experience

Real-time request tracking and servicing progress for requesters


## Tech Stacks
Platform: ServiceNow App Engine Studio 

Client-Side: GlideForm APIs, Client Scripts 

Server-Side: Business Rules, Script Includes

Service Portal: Widgets, Catalog Items, UI Pages, HTML & CSS

Source Control: GitHub for backup, version control

## Problems Encountered
1. Scripting Challenges
I don’t know how to code, so writing JavaScript for business rules and logic was tough. I had to learn JavaScript basics (still not sure I like it 😂), and it slowed me down at first.

2. Technical Issues with My PDI
My ServiceNow instance was released, and I got a message warning me.
I had to back up my app and data using GitHub. Restoring it was stressful—some files failed, and I got errors like "application already exists" or "update set skipped." A real lesson in managing environments.

## Lessons Learned
Leverage out-of-box solutions to build faster—don’t reinvent the wheel

A working solution doesn’t require advanced coding—logic and persistence go a long way

Documenting and backing up regularly saves time and stress

Always test access and automation as if you’re the end user

## Next Steps
Keep learning.
Keep building.
This is just the beginning.
