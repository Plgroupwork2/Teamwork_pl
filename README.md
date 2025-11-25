# PL/SQL Triggers & Package — README

## Scenario 1: AUCA System Access Policy (Triggers)

### Objectives
- Enforce AUCA’s access restrictions:
  - No system access or data modifications on **Saturday** and **Sunday**.
  - Access only allowed **Monday–Friday**, **8:00 AM – 5:00 PM**.
- Block all unauthorized actions immediately.
- Log every violation attempt for auditing.

### How It Was Solved
- A **logging table** was created to capture unauthorized attempts  
  (username, timestamp, and the action attempted).
- A **BEFORE trigger** checks:
  - Current day via `TO_CHAR(SYSDATE, 'DY')`
  - Current time via `TO_CHAR(SYSDATE, 'HH24')`
  - If outside allowed hours/days, it raises an exception to **block** the action.
- A **second trigger** inserts a record into the logging table whenever an attempt violates the rules.
- This ensures **real-time restriction enforcement** and complete **audit logging**.

---

## Scenario 2: HR Employee Management System (PL/SQL Package)

### Objectives
- Create a PL/SQL **package** that includes:
  - A function to calculate **RSSB tax**.
  - A function to calculate **net salary**.
  - A procedure using **dynamic SQL** to update or insert employee salary records.
- Demonstrate:
  - Difference between `USER` and `CURRENT_USER`.
  - Difference between **DEFINER** and **INVOKER** rights.
- Provide sample calls and meaningful code comments.
- (Optional) Add bulk processing support using loops/cursors.

### How It Was Solved
- The **package specification** declared:
  - A function for computing RSSB tax.
  - A function for returning net salary.
  - A procedure performing a dynamic SQL operation.
- The **package body** implemented:
  - RSSB deduction logic.
  - Net salary calculation (`gross - RSSB`).
  - Dynamic SQL using `EXECUTE IMMEDIATE` to update salary records.
- Rights explanation:
  - `AUTHID DEFINER` or `AUTHID CURRENT_USER` added to demonstrate privilege differences.
  - Comments clarified:
    - `USER` → account executing the code.
    - `CURRENT_USER` → invoker of the code when using invoker rights.
- Sample function and procedure calls were written to show proper execution.
- Optional feature: a cursor loop for processing multiple employees in bulk.

