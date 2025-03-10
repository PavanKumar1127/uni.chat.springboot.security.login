Project Overview
This project is a Spring Boot application integrated with Spring Security and JSON Web Token (JWT) for authentication and authorization. The application provides the following functionalities:

User Registration and Login:

Users can sign up for new accounts or log in using their username and password.
Based on the user's role (admin, moderator, user), access to various resources is controlled.
Security Configuration:

WebSecurityConfig: The core of our security implementation, configuring CORS, CSRF, session management, and access rules for protected resources. This configuration can be customized and extended as needed.
Note: WebSecurityConfigurerAdapter is deprecated from Spring 2.7.0. For more information and updates, refer to the official Spring documentation.
User Details Service:

The UserDetailsService interface loads user data by username and returns a UserDetails object containing necessary information (username, password, authorities) for authentication and validation.
Authentication Process:

UsernamePasswordAuthenticationToken: Captures the username and password from the login request, which the AuthenticationManager uses to authenticate the user.
AuthenticationManager: Utilizes DaoAuthenticationProvider, UserDetailsService, and PasswordEncoder to validate the credentials and return a fully populated Authentication object, including granted authorities.
Token Handling:

OncePerRequestFilter: Ensures that specific logic, such as JWT parsing, user detail loading, and authorization checks, is executed only once per request. This filter helps prevent redundant processing and maintains a consistent security context.
AuthEntryPointJwt: Handles authentication errors, responding with appropriate HTTP status codes when unauthenticated users attempt to access secured resources.
Data Access and Repositories:

UserRepository and RoleRepository: Interfaces extending Spring Data JPA's JpaRepository for database interactions, used within controllers to handle user and role data.
Controllers:

AuthController: Manages signup, login, and logout requests.
TestController: Provides endpoints for testing role-based access to resources, such as /api/test/all for public access and /api/test/user for authenticated users with specific roles.
Architecture Overview:

Security Package: Contains classes for configuring and implementing security objects, including WebSecurityConfig, UserDetailsServiceImpl, UserDetailsImpl, AuthEntryPointJwt, AuthTokenFilter, and JwtUtils.
Controllers: Handle authentication and authorized requests.
Models: Define the application's main entities, such as User and Role, with a many-to-many relationship.
Repositories: Interfaces for database operations.
Payloads: Define request and response objects for the APIs.
Configuration and Setup:

application.properties: Configures the Spring Datasource, Spring Data JPA, and application-specific properties (e.g., JWT secret, token expiration time).
Database Setup: Using H2 in-memory or disk-based database with necessary configurations for development and production environments.
H2 Console: Enabled for database administration and accessible via the configured path.
JWT and Security Handling:

JwtUtils: Provides methods for generating, parsing, and validating JWT tokens.
SecurityContext: Used to retrieve the current authenticated user's details.
Spring Rest Controllers:

AuthController: Manages registration, login, and logout actions.
TestController: Provides protected endpoints to test authorization based on user roles.
Additional Details
Updating from WebSecurityConfigurerAdapter: As WebSecurityConfigurerAdapter is deprecated, the project uses updated practices for configuring Spring Security. Refer to the official Spring documentation for more details.

JWT Cookie Management:

getJwtFromCookies: Retrieves the JWT from cookies.
generateJwtCookie: Generates a JWT-containing cookie.
getCleanJwtCookie: Clears the JWT cookie.
Handling Authentication Exceptions: The project includes mechanisms to handle exceptions thrown during authentication attempts, ensuring appropriate HTTP status codes and responses.


# Spring Boot Security Login example with JWT and H2 example

- Appropriate Flow for User Login and Registration with JWT and HttpOnly Cookie
- Spring Boot Rest Api Architecture with Spring Security
- How to configure Spring Security to work with JWT
- How to define Data Models and association for Authentication and Authorization
- Way to use Spring Data JPA to interact with H2 Database

## User Registration, Login and Authorization process.

![spring-boot-security-login-jwt-flow](spring-boot-security-login-jwt-flow.png)

## Spring Boot Server Architecture with Spring Security
You can have an overview of our Spring Boot Server with the diagram below:

![spring-boot-security-login-jwt-architecture](spring-boot-security-login-jwt-architecture.png)

For more detail, please visit:
> [Spring Boot Security Login example with JWT and H2 example](https://www.bezkoder.com/spring-boot-security-login-jwt/)

> [For MySQL/PostgreSQL](https://www.bezkoder.com/spring-boot-login-example-mysql/)

> [For MongoDB](https://www.bezkoder.com/spring-boot-jwt-auth-mongodb/)

Working with Front-end:
> [Angular 12](https://www.bezkoder.com/angular-12-jwt-auth-httponly-cookie/) / [Angular 13](https://www.bezkoder.com/angular-13-jwt-auth-httponly-cookie/) / [Angular 14](https://www.bezkoder.com/angular-14-jwt-auth/) / [Angular 15](https://www.bezkoder.com/angular-15-jwt-auth/) / [Angular 16](https://www.bezkoder.com/angular-16-jwt-auth/) / [Angular 17](https://www.bezkoder.com/angular-17-jwt-auth/)

> [React](https://www.bezkoder.com/react-login-example-jwt-hooks/) / [React Redux](https://www.bezkoder.com/redux-toolkit-auth/)

## Dependency
– If you want to use PostgreSQL:
```xml
<dependency>
  <groupId>org.postgresql</groupId>
  <artifactId>postgresql</artifactId>
  <scope>runtime</scope>
</dependency>
```
– or MySQL:
```xml
<dependency>
  <groupId>com.mysql</groupId>
  <artifactId>mysql-connector-j</artifactId>
  <scope>runtime</scope>
</dependency>
```
## Configure Spring Datasource, JPA, App properties
Open `src/main/resources/application.properties`
- For PostgreSQL:
```
spring.datasource.url=jdbc:postgresql://localhost:5432/testdb
spring.datasource.username=postgres
spring.datasource.password=123

spring.jpa.properties.hibernate.jdbc.lob.non_contextual_creation=true
spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.PostgreSQLDialect

# Hibernate ddl auto (create, create-drop, validate, update)
spring.jpa.hibernate.ddl-auto=update

# App Properties
bezkoder.app.jwtSecret= ======================BezKoder=Spring===========================
bezkoder.app.jwtExpirationMs= 86400000
```
- For MySQL
```
spring.datasource.url=jdbc:mysql://localhost:3306/testdb?useSSL=false
spring.datasource.username=root
spring.datasource.password=123456

spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.MySQLDialect
spring.jpa.hibernate.ddl-auto=update

# App Properties
bezkoder.app.jwtSecret= ======================BezKoder=Spring===========================
bezkoder.app.jwtExpirationMs= 86400000
```
## Run Spring Boot application
```
mvn spring-boot:run
```

## Run following SQL insert statements
```
INSERT INTO roles(name) VALUES('ROLE_USER');
INSERT INTO roles(name) VALUES('ROLE_MODERATOR');
INSERT INTO roles(name) VALUES('ROLE_ADMIN');
```

## Refresh Token

[Spring Boot JWT Refresh Token example](https://www.bezkoder.com/spring-security-refresh-token/)

## More Practice:
> [Spring Boot File upload example with Multipart File](https://bezkoder.com/spring-boot-file-upload/)

> [Exception handling: @RestControllerAdvice example in Spring Boot](https://bezkoder.com/spring-boot-restcontrolleradvice/)

> [Spring Boot Repository Unit Test with @DataJpaTest](https://bezkoder.com/spring-boot-unit-test-jpa-repo-datajpatest/)

> [Spring Boot Rest Controller Unit Test with @WebMvcTest](https://www.bezkoder.com/spring-boot-webmvctest/)

> [Spring Boot Pagination & Sorting example](https://www.bezkoder.com/spring-boot-pagination-sorting-example/)

> Validation: [Spring Boot Validate Request Body](https://www.bezkoder.com/spring-boot-validate-request-body/)

> Documentation: [Spring Boot and Swagger 3 example](https://www.bezkoder.com/spring-boot-swagger-3/)

> Caching: [Spring Boot Redis Cache example](https://www.bezkoder.com/spring-boot-redis-cache-example/)

Associations:
> [JPA/Hibernate One To Many example in Spring Boot](https://www.bezkoder.com/jpa-one-to-many/)

> [JPA/Hibernate Many To Many example in Spring Boot](https://www.bezkoder.com/jpa-many-to-many/)

> [JPA/Hibernate One To One example in Spring Boot](https://www.bezkoder.com/jpa-one-to-one/)

Deployment:
> [Deploy Spring Boot App on AWS – Elastic Beanstalk](https://www.bezkoder.com/deploy-spring-boot-aws-eb/)

> [Docker Compose Spring Boot and MySQL example](https://www.bezkoder.com/docker-compose-spring-boot-mysql/)

## Fullstack Authentication

> [Spring Boot + Vue.js JWT Authentication](https://bezkoder.com/spring-boot-vue-js-authentication-jwt-spring-security/)

> [Spring Boot + Angular 8 JWT Authentication](https://bezkoder.com/angular-spring-boot-jwt-auth/)

> [Spring Boot + Angular 10 JWT Authentication](https://bezkoder.com/angular-10-spring-boot-jwt-auth/)

> [Spring Boot + Angular 11 JWT Authentication](https://bezkoder.com/angular-11-spring-boot-jwt-auth/)

> [Spring Boot + Angular 12 JWT Authentication](https://www.bezkoder.com/angular-12-spring-boot-jwt-auth/)

> [Spring Boot + Angular 13 JWT Authentication](https://www.bezkoder.com/angular-13-spring-boot-jwt-auth/)

> [Spring Boot + Angular 14 JWT Authentication](https://www.bezkoder.com/angular-14-spring-boot-jwt-auth/)

> [Spring Boot + Angular 15 JWT Authentication](https://www.bezkoder.com/angular-15-spring-boot-jwt-auth/)

> [Spring Boot + Angular 16 JWT Authentication](https://www.bezkoder.com/angular-16-spring-boot-jwt-auth/)

> [Spring Boot + Angular 17 JWT Authentication](https://www.bezkoder.com/angular-17-spring-boot-jwt-auth/)

> [Spring Boot + React JWT Authentication](https://bezkoder.com/spring-boot-react-jwt-auth/)

## Fullstack CRUD App

> [Vue.js + Spring Boot + H2 Embedded database example](https://www.bezkoder.com/spring-boot-vue-js-crud-example/)

> [Vue.js + Spring Boot + MySQL example](https://www.bezkoder.com/spring-boot-vue-js-mysql/)

> [Vue.js + Spring Boot + PostgreSQL example](https://www.bezkoder.com/spring-boot-vue-js-postgresql/)

> [Angular 8 + Spring Boot + Embedded database example](https://www.bezkoder.com/angular-spring-boot-crud/)

> [Angular 8 + Spring Boot + MySQL example](https://www.bezkoder.com/angular-spring-boot-crud/)

> [Angular 8 + Spring Boot + PostgreSQL example](https://www.bezkoder.com/angular-spring-boot-postgresql/)

> [Angular 10 + Spring Boot + MySQL example](https://www.bezkoder.com/angular-10-spring-boot-crud/)

> [Angular 10 + Spring Boot + PostgreSQL example](https://www.bezkoder.com/angular-10-spring-boot-postgresql/)

> [Angular 11 + Spring Boot + MySQL example](https://www.bezkoder.com/angular-11-spring-boot-crud/)

> [Angular 11 + Spring Boot + PostgreSQL example](https://www.bezkoder.com/angular-11-spring-boot-postgresql/)

> [Angular 12 + Spring Boot + Embedded database example](https://www.bezkoder.com/angular-12-spring-boot-crud/)

> [Angular 12 + Spring Boot + MySQL example](https://www.bezkoder.com/angular-12-spring-boot-mysql/)

> [Angular 12 + Spring Boot + PostgreSQL example](https://www.bezkoder.com/angular-12-spring-boot-postgresql/)

> [Angular 13 + Spring Boot + H2 Embedded Database example](https://www.bezkoder.com/spring-boot-angular-13-crud/)

> [Angular 13 + Spring Boot + MySQL example](https://www.bezkoder.com/spring-boot-angular-13-mysql/)

> [Angular 13 + Spring Boot + PostgreSQL example](https://www.bezkoder.com/spring-boot-angular-13-postgresql/)

> [Angular 14 + Spring Boot + H2 Embedded Database example](https://www.bezkoder.com/spring-boot-angular-14-crud/)

> [Angular 14 + Spring Boot + MySQL example](https://www.bezkoder.com/spring-boot-angular-14-mysql/)

> [Angular 14 + Spring Boot + PostgreSQL example](https://www.bezkoder.com/spring-boot-angular-14-postgresql/)

> [Angular 15 + Spring Boot + H2 Embedded Database example](https://www.bezkoder.com/spring-boot-angular-15-crud/)

> [Angular 15 + Spring Boot + MySQL example](https://www.bezkoder.com/spring-boot-angular-15-mysql/)

> [Angular 15 + Spring Boot + PostgreSQL example](https://www.bezkoder.com/spring-boot-angular-15-postgresql/)

> [Angular 16 + Spring Boot + H2 Embedded Database example](https://www.bezkoder.com/spring-boot-angular-16-crud/)

> [Angular 16 + Spring Boot + MySQL example](https://www.bezkoder.com/spring-boot-angular-16-mysql/)

> [Angular 16 + Spring Boot + PostgreSQL example](https://www.bezkoder.com/spring-boot-angular-16-postgresql/)

> [Angular 17 + Spring Boot + H2 Embedded Database example](https://www.bezkoder.com/spring-boot-angular-17-crud/)

> [Angular 17 + Spring Boot + MySQL example](https://www.bezkoder.com/spring-boot-angular-17-mysql/)

> [Angular 17 + Spring Boot + PostgreSQL example](https://www.bezkoder.com/spring-boot-angular-17-postgresql/)

> [React + Spring Boot + MySQL example](https://www.bezkoder.com/react-spring-boot-crud/)

> [React + Spring Boot + PostgreSQL example](https://www.bezkoder.com/spring-boot-react-postgresql/)

> [React + Spring Boot + MongoDB example](https://www.bezkoder.com/react-spring-boot-mongodb/)

Run both Back-end & Front-end in one place:
> [Integrate Angular with Spring Boot Rest API](https://www.bezkoder.com/integrate-angular-spring-boot/)

> [Integrate React.js with Spring Boot Rest API](https://www.bezkoder.com/integrate-reactjs-spring-boot/)

> [Integrate Vue.js with Spring Boot Rest API](https://www.bezkoder.com/integrate-vue-spring-boot/)
