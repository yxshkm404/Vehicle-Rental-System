# Vehicle Rental System

This is a full-stack web application for managing vehicle rentals. Users can browse available cars, rent them for specific periods, and administrators can manage the car inventory and rentals.

## Tech Stack

### Backend

*   **Java 17**
*   **Spring Boot** (v2.1.3.RELEASE)
*   **Spring Data JPA**: For object-relational mapping and data access.
*   **Spring Security**: For authentication and authorization.
*   **JWT (JSON Web Tokens)**: For securing the API.
*   **MySQL**: Relational database for data storage.
*   **Maven**: Dependency management.
*   **ModelMapper**: For object mapping.

### Frontend

*   **React** (v16.8.3)
*   **React Router** (v4.3.1): For client-side routing.
*   **Bootstrap** (v4.3.1): For UI components and styling.
*   **JavaScript (ES6+)**
*   **HTML5 & CSS3**

## Features

*   **User Authentication**: Secure user registration and login.
*   **Car Catalog**: Browse and view details of available cars.
*   **Rental System**: Rent a car for a specified period.
*   **User Dashboard**: View personal rental history.
*   **Admin Panel**:
    *   Manage car inventory (Create, Edit, Delete).
    *   View and manage all user rentals.

## Setup and Installation

### Prerequisites

*   Java 17 or higher
*   Maven
*   Node.js and npm
*   MySQL

### Backend

1.  **Clone the repository:**
    ```bash
    git clone https://github.com/your-username/Vehicle-Rental-System.git
    cd Vehicle-Rental-System/back-end
    ```
2.  **Configure the database:**
    *   Open `src/main/resources/application.properties`.
    *   Update the `spring.datasource.url`, `spring.datasource.username`, and `spring.datasource.password` properties to match your MySQL configuration.
3.  **Run the application:**
    ```bash
    mvn spring-boot:run
    ```
    The backend server will start on `http://localhost:8080`.

### Frontend

1.  **Navigate to the frontend directory:**
    ```bash
    cd ../front-end
    ```
2.  **Install dependencies:**
    ```bash
    npm install
    ```
3.  **Start the development server:**
    ```bash
    npm start
    ```
    The frontend application will be accessible at `http://localhost:3000`.

## Usage

1.  Register a new user account or log in with an existing one.
2.  Browse the available cars on the home page.
3.  Select a car to view its details and rental options.
4.  Choose your desired rental dates and confirm the rental.
5.  Admins can access the admin panel to manage cars and rentals.
