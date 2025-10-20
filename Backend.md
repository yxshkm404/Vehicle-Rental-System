# Back-end Project Report

This document provides an overview of the back-end of the Vehicle Rental System, its architecture, and key components, including file locations and their specific purposes.

## Project Overview

The back-end is a Java-based application built using the Spring Boot framework. It provides a RESTful API for managing vehicle rentals. Key features include:

-   User authentication and authorization using JSON Web Tokens (JWT).
-   CRUD operations for cars.
-   Renting and returning cars.
-   Viewing rental history.

The project uses Maven for dependency management and is configured to connect to a MySQL database.

## MVC Architecture

The application follows a Model-View-Controller (MVC) architectural pattern, which is typical for Spring Boot web applications.

### Model

The Model represents the data and business logic of the application. In this project, the model is composed of several parts:

-   **Entities**
    -   **Location**: `back-end/src/main/java/com/server/domain/entities/`
    -   **Purpose**: These are the core domain objects that are mapped to database tables using the Java Persistence API (JPA). Each class in this directory corresponds to a table in the database.
    -   **Key Files**:
        -   `Car.java`: Represents a car available for rent.
        -   `User.java`: Represents a user of the system.
        -   `Rent.java`: Represents a rental transaction.
        -   `Sale.java`: Represents a sale record.
        -   `UserRole.java`: Represents the roles a user can have (e.g., USER, ADMIN).

-   **Binding Models**
    -   **Location**: `back-end/src/main/java/com/server/domain/models/binding/`
    -   **Purpose**: These models are used to capture and validate data from incoming HTTP requests (e.g., from JSON payloads). They act as a data transfer object (DTO) between the client and the controller.
    -   **Key Files**:
        -   `UserRegisterBindingModel.java`: For user registration.
        -   `RentCreateBindingModel.java`: For creating a new rent.

-   **View Models**
    -   **Location**: `back-end/src/main/java/com/server/domain/models/view/`
    -   **Purpose**: These models are used to shape the data sent back in HTTP responses. They provide a client-friendly representation of the domain objects, often hiding implementation details and formatting data for display.
    -   **Key Files**:
        -   `CarViewModel.java`: For displaying car information.
        -   `RentViewModel.java`: For displaying rent information.

### View

In a RESTful API, the "View" is the representation of the resource that is sent to the client, typically in JSON format. Spring Boot's `@RestController` annotation, combined with the Jackson library, automatically serializes the View Model objects into JSON responses. There are no dedicated view files like in a traditional web application.

### Controller

-   **Location**: `back-end/src/main/java/com/server/web/controllers/`
-   **Purpose**: Controllers are responsible for handling incoming HTTP requests, processing user input, and returning a response. They are the entry point for all client interactions.
-   **Key Files**:
    -   `CarController.java`: Handles all requests related to cars (e.g., creating, viewing, editing, deleting cars).
    -   `UserController.java`: Handles user-related requests like registration and login.
    -   `RentController.java`: Manages rental operations.
    -   `SaleController.java`: Handles sales-related endpoints.
    -   `GlobalExceptionController.java`: A centralized exception handler for the application.

## Other Key Components

### Services

-   **Location**: `back-end/src/main/java/com/server/services/`
-   **Purpose**: Services contain the core business logic of the application. They are called by the controllers and orchestrate the application's functionality.
-   **Key Files**:
    -   `CarServiceImpl.java`: Implements the business logic for car management.
    -   `UserServiceImpl.java`: Implements user management logic, including user registration and loading user details for security purposes.
    -   `RentServiceImpl.java`: Contains the logic for renting and managing rentals.

### Repositories

-   **Location**: `back-end/src/main/java/com/server/repositories/`
-   **Purpose**: Repositories are responsible for data access. They provide an abstraction over the database and allow the services to interact with the database without writing boilerplate code. The project uses Spring Data JPA, which provides repository support out of the box.
-   **Key Files**:
    -   `CarRepository.java`: Provides CRUD operations for `Car` entities.
    -   `UserRepository.java`: Provides CRUD operations for `User` entities.
    -   `RentRepository.java`: Provides CRUD operations for `Rent` entities.

### Security

-   **Location**: `back-end/src/main/java/com/server/config/SecurityConfig.java`
-   **Purpose**: This class configures the security of the application, including authentication, authorization, and CORS.

-   **JWT Filters**
    -   **Location**: `back-end/src/main/java/com/server/web/filters/`
    -   **Purpose**: These filters are used to implement JWT-based authentication.
    -   **Key Files**:
        -   `JwtAuthenticationFilter.java`: Intercepts login requests to authenticate users and generate JWTs.
        -   `JwtAuthorizationFilter.java`: Intercepts all other requests to validate the JWT and set the user's authentication context.

### Configuration

-   **Java-based Configuration**
    -   **Location**: `back-end/src/main/java/com/server/config/`
    -   **Purpose**: These classes define application beans and configuration.
    -   **Key Files**:
        -   `ApplicationBeanConfiguration.java`: Defines application beans, such as `BCryptPasswordEncoder` and `ModelMapper`.
        -   `MapperConfig.java`: Configures the ModelMapper.

-   **Properties Configuration**
    -   **Location**: `back-end/src/main/resources/application.properties`
    -   **Purpose**: This file contains database connection details, server port, and other application settings.

### Utils

-   **Location**: `back-end/src/main/java/com/server/util/`
-   **Purpose**: Utility classes with helper methods.
-   **Key Files**:
    -   `PageMapper.java`: A utility for mapping pages of entities to pages of view models.

### Exceptions

-   **Location**: `back-end/src/main/java/com/server/exceptions/`
-   **Purpose**: Custom exception classes for handling specific error scenarios.
-   **Key Files**:
    -   `CarNotFoundException.java`: Thrown when a car is not found.
    -   `InvalidDatesException.java`: Thrown when the provided dates for a rental are invalid.

## Application Flow (Example: Creating a Car)

1.  An **HTTP POST request** with car data is sent to the `/cars/create` endpoint.
2.  The `CarController`'s `createCar` method is invoked (`CarController.java`).
3.  The request body is deserialized into a `CarCreationBindingModel` object (`CarCreationBindingModel.java`).
4.  The controller calls the `CreateCar` method of the `CarService` (`CarServiceImpl.java`).
5.  The `CarService` maps the `CarCreationBindingModel` to a `Car` entity (`Car.java`).
6.  The `CarService` calls the `saveAndFlush` method of the `CarRepository` to persist the new car in the database (`CarRepository.java`).
7.  The `CarRepository` (managed by Spring Data JPA) generates and executes the necessary SQL `INSERT` statement.
8.  The saved `Car` entity is returned to the `CarService`.
9.  The `CarService` maps the saved `Car` entity to a `CarViewModel` (`CarViewModel.java`).
10. The `CarViewModel` is returned to the `CarController`.
11. The `CarController` wraps the `CarViewModel` in a `ResponseBody` and returns it.
12. Spring Boot serializes the `ResponseBody` to a **JSON response** and sends it back to the client with a `200 OK` status.

## API Endpoints

This section details the available API endpoints for testing with tools like Postman.

### Authentication

| Method | Endpoint     | Purpose         | Authentication |
| :----- | :----------- | :-------------- | :--- |
| POST   | `/login`     | Authenticate a user and receive a JWT token. | None |
| POST   | `/users/register` | Register a new user. | None |

### Cars

| Method | Endpoint            | Purpose                                      | Authentication |
| :----- | :------------------ | :------------------------------------------- | :--- |
| POST   | `/cars/create`      | Create a new car.                            | ADMIN |
| GET    | `/cars/{id}`        | Get car details by ID.                       | None |
| POST   | `/cars/edit/{id}`   | Edit a car by ID.                            | ADMIN |
| POST   | `/cars/reserve/{id}`| Reserve a car for a given period.            | USER |
| DELETE | `/cars/delete/{id}` | Delete a car by ID.                          | ADMIN |
| GET    | `/cars/all`         | Get a paginated list of all cars.            | None |
| POST   | `/cars/available`   | Get a paginated list of available cars for given dates. | USER |
| POST   | `/cars/check/{id}`  | Check car availability for given dates.      | None |

### Rents

| Method | Endpoint          | Purpose                               | Authentication |
| :----- | :---------------- | :------------------------------------ | :--- |
| GET    | `/rents/approved`   | Get a paginated list of approved rents. | ADMIN |
| GET    | `/rents/active`     | Get a paginated list of active rents.   | ADMIN |
| GET    | `/rents/unapproved` | Get a paginated list of unapproved rents. | ADMIN |
| POST   | `/rents/approve/{id}` | Approve a rent by ID.                 | ADMIN |
| POST   | `/rents/decline/{id}` | Decline a rent by ID.                 | ADMIN |
| POST   | `/rents/finish/{id}`  | Finish a rent by ID.                  | ADMIN |

### Sales

| Method | Endpoint               | Purpose                             | Authentication |
| :----- | :--------------------- | :---------------------------------- | :--- |
| GET    | `/sales/all/{username}` | Get a paginated list of sales for a user. | USER |