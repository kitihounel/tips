# SQL Server

- [Clone a database](#clone-a-database)

## Clone a database

Within SQL Server Management Studio:

- Create a backup of the database you want to copy.
- Right-click "Databases" and select "Restore Files and Filegroups".
- Enter the name of the new database in the "To database" field.
- Select "From device" and then select the file that you backuped in the first step.
- Click "OK".

This will "clone" the database with the correct table settings such as the "default value" and "auto increase" etc.

**Source:** [StackOverflow](https://stackoverflow.com/a/19954576).
