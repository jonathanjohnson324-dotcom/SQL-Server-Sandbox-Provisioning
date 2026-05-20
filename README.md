
# SQL Server Sandbox Provisioning & Storage Optimization

## Project Overview
This repository documents the structural setup, resource planning, and provisioning of a local Microsoft SQL Server 2022 Express development environment. The goal of this project was to isolate a local sandbox database instance while implementing strategic storage optimization practices to preserve primary operating system resources.

---

## Architectural & Design Decisions

### Cross-Drive Storage Allocation
To maximize system performance and manage strict hardware storage constraints, a split-drive configuration was manually engineered:
* **Operating System Volume (`C:\`):** Reserved strictly for core application binaries, SQL Server engine executable files, and standard system configurations to leverage fast OS read/write speeds.
* **Secondary Storage Volume (`D:\`):** Provisioned to house all heavy data resources, including primary relational database instances, transaction logs, and external backup directories (`D:\SQL backup`). 

**Technical Reasoning:** This separation ensures that scaling databases or large-scale testing operations cannot inadvertently fill the primary operating system drive, preventing potential OS instability or critical disk space failures.

---

## Environment Configuration & Specifications

* **Database Engine:** Microsoft SQL Server 2022 Express Edition
* **Management IDE:** SQL Server Management Studio (SSMS 22)
* **Authentication Method:** Windows Authentication (Secured locally via Trusted Server Certificates to bypass local SSL handshake overhead)
* **Target Schema Sourced:** Microsoft AdventureWorks2022 OLTP (Online Transaction Processing) Industry Standard Sandbox

---

## Step-by-Step Provisioning & Data Ingestion

### 1. File Structure & Sourcing
* Created a dedicated ingestion directory at `D:\SQL backup\` to prevent local Windows permissions/administrative lockouts.
* Sourced the official `AdventureWorks2022.bak` database restoration file directly from Microsoft Learn repository. Link Below.
  https://learn.microsoft.com/en-us/sql/samples/adventureworks-install-configure?view=sql-server-ver17&tabs=ssms
<img width="891" height="212" alt="image" src="https://github.com/user-attachments/assets/fc738f34-4cd6-4b6e-8b25-c46eae347092" />


### 2. Database Restoration (Instance Mapping)
Rather than executing a standard default database creation, the environment was provisioned by restoring a full database backup file and mapping the underlying relational structures directly to the localized server instance.

Perform the following steps.
1. In Object Explorer, Right Click on Database.
2. Select Restore Database.

<img width="567" height="562" alt="image" src="https://github.com/user-attachments/assets/38f85a79-5c46-403b-82f7-43cdb49f2810" />

4. On the General selection , under Source, Click the Device radio button. Select the three dots (...).
5. In the Select Backup Devices window, click Add.
6. Navigate to teh location where the backup database is located. In this instance D:\SQL Backup.
7. Select the database backup file to restore. EX. AdventureWorks2022.bak
8. Click OK.


<img width="1863" height="812" alt="image" src="https://github.com/user-attachments/assets/46d71587-3372-4151-bb07-844f204e2482" />

10. The backup database has been added to the list to be restored.

<img width="680" height="452" alt="image" src="https://github.com/user-attachments/assets/5dfa9ef4-1213-4c35-93fe-1008d811779a" />

11. Click OK.

<img width="868" height="753" alt="image" src="https://github.com/user-attachments/assets/fa5a3884-f8de-4e13-8f9e-9b0fc6d705e5" />

12. Verify the newly populated fields within Source, Destination and Restore Plan are correct.
13. Click OK.
14. Once the backup has completed, return to the main database screen.
15. Select Databases.
<img width="422" height="240" alt="image" src="https://github.com/user-attachments/assets/52c70740-56b7-40b7-9346-d96feeafee18" />

### 3. Verification & Execution
The restoration wizard successfully processed the relational schemas, schemas integrity, and indexed constraints. 
To verify the database is up and running
Right click Databases and select Properties.
<img width="432" height="545" alt="image" src="https://github.com/user-attachments/assets/0267b133-67de-4855-9acd-61e021871551" />
<img width="957" height="803" alt="image" src="https://github.com/user-attachments/assets/3c450a7f-651e-49b6-ae11-25185f24f4e5" />


The environment is fully live, verified, and mapped under the local server Object Explorer hierarchy, ready for data analysis, performance tuning, and schema development.





---

## 🤖 Acknowledgments
*This documentation was structured and refined with the assistance of AI to ensure technical clarity, professional terminology, and precise formatting, accurately reflecting the architecture and configurations implemented during the system provisioning.*
