Task 1: Create a New Pluggable Database (PDB)

We'll go step-by-step, starting from connecting to the CDB (Container Database), creating the PDB named plsql_class2024db, creating a user with the format specified (e.g., er_plsqlauca), and assigning a password.

Step 1: Connect to the CDB as a privileged user
You need to connect to the CDB as a SYSDBA or privileged user that can create and manage PDBs. You can use SQL*Plus, SQL Developer, or any tool that connects to Oracle.

sqlplus sys/[your_sys_password]@localhost:1521/XEPDB1 as sysdba

Step 2: Create the Pluggable Database
To create a new PDB named plsql_class2024db, execute the following SQL commands:

CREATE PLUGGABLE DATABASE plsql_class2024db 
ADMIN USER pdb_admin IDENTIFIED BY pdb_password
FILE_NAME_CONVERT = ('/opt/oracle/oradata/XE/pdbseed/', '/opt/oracle/oradata/XE/plsql_class2024db/');

Step 3: Open the New PDB
ALTER PLUGGABLE DATABASE plsql_class2024db OPEN;

Step 4: Switch to the New PDB
After creating and opening the PDB, you need to switch to it:

ALTER SESSION SET CONTAINER = plsql_class2024db;

Step 5: Create the New User
Now, inside the plsql_class2024db, create the required username with the format <first_two_letters>_plsqlauca.

CREATE USER er_plsqlauca IDENTIFIED BY your_password;

Step 6: Grant Required Privileges to the User
To allow this user to store all their work during the course, you'll need to grant them the necessary privileges:

GRANT CONNECT, RESOURCE TO er_plsqlauca;

Step 7: Test the New User
Exit the current session and log in as the newly created user:

sqlplus er_plsqlauca/your_password@localhost:1521/plsql_class2024db

Now, the user er_plsqlauca will have access to the newly created PDB plsql_class2024db, and they can create tables, views, or any other database objects as required for your class activities.

Here’s the exact SQL command to create the PDB named plsql_class2024db using the correct file path for the PDB seed:

SQL to Create the PDB:
CREATE PLUGGABLE DATABASE plsql_class2024db 
ADMIN USER pdb_admin IDENTIFIED BY pdb_password
FILE_NAME_CONVERT = ('C:\APP\LENOVO\PRODUCT\21C\ORADATA\XE\PDBSEED\', 
                     'C:\APP\LENOVO\PRODUCT\21C\ORADATA\XE\plsql_class2024db\');


Great! Now that you’ve identified the path for the seed PDB on your Windows machine:

mathematica
Copy code
C:\APP\LENOVO\PRODUCT\21C\ORADATA\XE\PDBSEED\SYSTEM01.DBF
You can use this path in the FILE_NAME_CONVERT clause when creating your new Pluggable Database (PDB).

Here’s the exact SQL command to create the PDB named plsql_class2024db using the correct file path for the PDB seed:

SQL to Create the PDB:
sql
Copy code
CREATE PLUGGABLE DATABASE plsql_class2024db 
ADMIN USER pdb_admin IDENTIFIED BY pdb_password
FILE_NAME_CONVERT = ('C:\APP\LENOVO\PRODUCT\21C\ORADATA\XE\PDBSEED\', 
                     'C:\APP\LENOVO\PRODUCT\21C\ORADATA\XE\plsql_class2024db\');
Explanation:
The first part of the FILE_NAME_CONVERT clause ('C:\APP\LENOVO\PRODUCT\21C\ORADATA\XE\PDBSEED\') is the source path where the PDB seed (pdbseed) data files are located.
The second part ('C:\APP\LENOVO\PRODUCT\21C\ORADATA\XE\plsql_class2024db\') is the target path where the new PDB’s files will be stored. Make sure that the directory plsql_class2024db exists or Oracle can create it.

Step 1: Open the New PDB
ALTER PLUGGABLE DATABASE plsql_class2024db OPEN;

Step 2: Save the State of the PDB (Optional)
If you want your new PDB to automatically open whenever the container database (CDB) starts, save its state:
ALTER PLUGGABLE DATABASE plsql_class2024db SAVE STATE;

Step 3: Switch to the PDB and Create Your User
Once your PDB is up and running, switch to the new PDB to create your user:
ALTER SESSION SET CONTAINER = plsql_class2024db;

-- Create a user following the naming convention
CREATE USER er_plsqlauca IDENTIFIED BY your_password;

-- Grant necessary privileges
GRANT CONNECT, RESOURCE TO er_plsqlauca;

Task 2 (creating and deleting a Pluggable Database - PDB), here are the step-by-step instructions, including SQL commands for creating a PDB and then deleting it. You'll need to use your Oracle environment

Step 1: Create the PDB
We will create a new PDB based on the first two letters of your first name followed by _to_delete_pdb.

sqlplus sys/[sys_password]@localhost:1521/XEPDB1 as sysdba

Step 2: Delete the PDB

SQL Command to Drop/Delete the PDB(classified)

1.Close the PDB:
ALTER PLUGGABLE DATABASE er_to_delete_pdb CLOSE IMMEDIATE;

2.Drop the PDB:
DROP PLUGGABLE DATABASE er_to_delete_pdb INCLUDING DATAFILES;

conclusion

In this guide, we covered how to manage your Oracle 21c XE database by creating and deleting Pluggable Databases (PDBs), configuring Oracle Enterprise Manager (EM Express), and using GitHub to store and organize your project. We also demonstrated how to upload screenshots and embed them in markdown files on GitHub. These steps will help you efficiently manage your database tasks and collaborate on your projects using version control.






