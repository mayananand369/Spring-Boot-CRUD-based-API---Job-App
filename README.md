<h1>About the project</h1>

This is a project demonstrating how to integrate Spring Boot, JWT, MySQL and role-based access.

A basic understanding of Spring Boot, REST APIs, JPA Repositories, JWT Concepts and MySQL is required.

<h2>Step 1. Restoring the database dump</h2>

For this example we will be using MySQL.

In the project root there is a file named database_schema.sql. This file contains a very simple schema with two tables, one for users and another for users' roles.

There are two registered users: User 1 with username user1 and password pass1 and User 2 with username user2 and password pass2.

The User 1 has to roles, ADMIN and USER whereas User 2 only has the role USER.

The passwords are encoded using the services provided by services.password.PasswordService.java which uses the secret contained in src.main.resources.application.properties.

<h3>Step 2. Connecting to the database</h3>

Once the database schema is restored, you will need to change its credentials in application.properties.

The dependency necessary to connect to the database is:

<dependency> <groupId>mysql</groupId> <artifactId>mysql-connector-java</artifactId> </dependency>

<h4>Step 3. Configuring the repository</h4>
We will be interacting with the database through JPA by using Hibernate as the implementation provider.

The entities representing the database tables * users * and * users_roles * are located in the package model.

The persistence context configuration is done by the class persistence.PersistenceContext.java.

The relation between User UsersRoles is mapped in such a way to load the roles a user has automatically when a user is loaded, thus, we are only creating a repository to access User instances. The repository can be found at repository.UserRepository.java.

The dependency for this feature is:

<dependency> <groupId>org.springframework.boot</groupId> <artifactId>spring-boot-starter-data-jpa</artifactId> </dependency>

<h5>Step 4. Creating the API</h5>
We are going to create two API entries, one to be accessed in an insecure way (* /api/public/ ) and another one in a secure way ( /api/secure/ *). The API will work somewhat like an echo, sending back the received value along with the security level of the request.

The methods implementing this API can be found in the class controller.MainController.java.
