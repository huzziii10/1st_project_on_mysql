# 1st_project_on_mysql

"""
Embracing the journey of learning the database management system. 
Kindly drop your comments/guidance.
Getting Hands-On Experience On MySQL - Course Provided By Infosys Spring Board Program
"""

# Importing necessary libraries
import mysql.connector

# Establishing connection to MySQL server
try:
    connection = mysql.connector.connect(
        host="localhost",
        user="username",
        password="password",
        database="database_name"
    )
    cursor = connection.cursor()

    # Creating a table
    create_table_query = """
    CREATE TABLE IF NOT EXISTS users (
        id INT AUTO_INCREMENT PRIMARY KEY,
        name VARCHAR(255),
        email VARCHAR(255)
    )
    """
    cursor.execute(create_table_query)
    print("Table created successfully.")

    # Inserting data into the table
    insert_query = """
    INSERT INTO users (name, email) VALUES (%s, %s)
    """
    data = [("John Doe", "john@example.com"),
            ("Jane Smith", "jane@example.com")]
    cursor.executemany(insert_query, data)
    connection.commit()
    print("Data inserted successfully.")

    # Fetching and printing data from the table
    select_query = """
    SELECT * FROM users
    """
    cursor.execute(select_query)
    result = cursor.fetchall()
    print("Fetched data from the table:")
    for row in result:
        print(row)

except mysql.connector.Error as error:
    print("Error while connecting to MySQL:", error)

finally:
    if connection.is_connected():
        cursor.close()
        connection.close()
        print("MySQL connection is closed.")

