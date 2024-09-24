
Job Application Tracker
Project Overview
The Job Application Tracker is a command-line interface (CLI) tool designed to help users manage and keep track of their job applications. Users can add details about job positions they've applied for, track the status of each application, and organize this data by company.

Features
Add and track multiple job applications.
View the status of each application (e.g., Applied, Interviewed, Offered).
Associate each application with a company and additional notes.
Set reminders for follow-ups or interviews (optional).
Technologies Used
Python: The main programming language used for the CLI and database interactions.
PostgreSQL: The relational database used to store application and company data.
psycopg2: A Python library used to interact with the PostgreSQL database.
Database Structure
The following tables are used in the application:

1. users Table
Stores user information.

Column	Type	Description
id	SERIAL	Primary Key
username	VARCHAR(255)	User's unique username
email	VARCHAR(255)	User's email address
password	VARCHAR(255)	User's password (hashed)
2. company Table
Stores information about companies.

Column	Type	Description
id	SERIAL	Primary Key
name	VARCHAR(255)	Name of the company
location	VARCHAR(255)	Location of the company
industry	VARCHAR(255)	Industry or sector
3. application Table
Stores information about job applications.

Column	Type	Description
id	SERIAL	Primary Key
job_title	VARCHAR(255)	Job title being applied for
application_date	DATE	Date of application
status	VARCHAR(255)	Application status (e.g., Applied)
company_id	INT	Foreign Key referencing company(id)
users_id	INT	Foreign Key referencing users(id)
notes	TEXT	Additional notes about the application
Setup Instructions
1. Install Dependencies
Make sure you have Python and PostgreSQL installed. Then, install the required Python library:

bash
Copy code
pip install psycopg2
2. Create the Database
Open your PostgreSQL client and create a new database:

sql
Copy code
CREATE DATABASE job_tracker;
Create the necessary tables by running the following SQL queries:

sql
Copy code
CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    username VARCHAR(255) UNIQUE NOT NULL,
    email VARCHAR(255) UNIQUE NOT NULL,
    password VARCHAR(255) NOT NULL
);

CREATE TABLE company (
    id SERIAL PRIMARY KEY,
    name VARCHAR(255),
    location VARCHAR(255),
    industry VARCHAR(255)
);

CREATE TABLE application (
    id SERIAL PRIMARY KEY,
    job_title VARCHAR(255),
    application_date DATE,
    status VARCHAR(255),
    company_id INT,
    users_id INT,
    notes TEXT,
    FOREIGN KEY (company_id) REFERENCES company(id),
    FOREIGN KEY (users_id) REFERENCES users(id)
);
3. Run the Application
Once the tables are set up, run your Python code to interact with the database.

Example usage in Python:

python
Copy code
import psycopg2

# Connect to the database
conn = psycopg2.connect(
    dbname="job_tracker",
    user="your_username",
    password="your_password",
    host="localhost"
)
cursor = conn.cursor()

# Example: Insert a new company
insert_company_query = "INSERT INTO company (name, location, industry) VALUES (%s, %s, %s);"
cursor.execute(insert_company_query, ("Tech Corp", "New York", "Technology"))
conn.commit()

# Close the connection
cursor.close()
conn.close()
Future Enhancements
Add a user-friendly graphical user interface (GUI) for ease of use.
Implement notifications for application deadlines and follow-up reminders.
Expand features to allow tracking interview stages and rejections.
Contributing
Feel free to fork this repository and make improvements. Contributions are welcome!
