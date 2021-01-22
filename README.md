# Data Connectivity using Java

#### *Pre-requisite: You should know basic SQL, MVC pattern and Java OOP concepts to understand this content*

## Table of Contents

[Week 1 - Accessing Databases with JDBC](#accessing-databases-with-jdbc)

## Accessing Databases with JDBC

```java

/**
 * @author Zokir Rakhimov
 */
package ca.myseneca.JDBC.connection;

import java.sql.*;

/**
 * This Java program uses JBDC connects to MySQL database 
 * server.
 *
 */
public class ConnectMySql {

	static final String DRIVER_NAME = "com.mysql.cj.jdbc.Driver"; // JDBC driver
	static final String SYS_NAME = "host"; // database server
	static final String DB_NAME = "db_name"; // database name

	// Database credentials
	static final String USERID = UserPassMysql.USERNAME;
	static final String PASSWORD = UserPassMysql.PASSWORD;

	public static void main(String args[]) {

		Connection connnection = null;// declare and initialize to be null
		Statement statement = null;
		ResultSet resultSet = null;

		try { //  exception handling 

			// Load / Register JDBC driver (class)
			Class.forName(DRIVER_NAME);

			// database URL
			String url = "jdbc:mysql://" + SYS_NAME + "/" + DB_NAME;

			// Establish the connection.
			connnection = DriverManager.getConnection(url, USERID, PASSWORD);
			System.out.println("Connected database successfully...");

			String query = "SELECT * FROM Table_Name";

			// Create a Statement object that will QUERY City table.
			statement = connnection.createStatement();

			// Returns a ResultSet object containing results.
			resultSet = statement.executeQuery(query);
			while (resultSet.next()) {

				// Positions to first record in ResultSet (initially before
				// first record).
				int id = resultSet.getInt("ID");
				String name = resultSet.getString("Name");
				String countryCode = resultSet.getString("CountryCode");
				String district = resultSet.getString("District");
				int population = resultSet.getInt("Population");
				System.out.println("ID: " + id + " | CountryName: " + name + " | FirstName: " + countryCode
						+ " | District" + district + " | Population: " + population);
			}

		}
		// Catch the exceptions.
		catch (ClassNotFoundException ex) {
			System.err.println("Failed to load JDBC driver.");
		} catch (SQLException e) {
			e.printStackTrace();
			System.out.println("Exception: " + e.getMessage());
		}

		// Close the connection in finally block.
		finally {
			try {
				if (resultSet != null)
					resultSet.close();

				if (statement != null)
					statement.close();

				if (connnection != null)
					connnection.close();
			} catch (SQLException e) {
			}
		}
	}
}

```


