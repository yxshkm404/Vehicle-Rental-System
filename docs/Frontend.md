# Front-end Report

## Overview

This document provides a detailed explanation of the front-end architecture of the Vehicle Rental System. The front-end is a single-page application (SPA) built with React. It provides a user interface for customers to browse and rent vehicles, and for administrators to manage the vehicle inventory and rentals.

## Technologies Used

- **React:** A JavaScript library for building user interfaces.
- **React Router:** For declarative routing in the application.
- **React Bootstrap:** A library of reusable front-end components.
- **Bootstrap:** A popular CSS framework for designing responsive and mobile-first websites.
- **JWT Decode:** A small browser library to decode JWTs tokens which is useful for extracting information from the token.
- **Toastr:** A Javascript library for non-blocking notifications.

## Project Structure

The front-end code is located in the `front-end` directory. The main subdirectories are:

- **`src/`**: Contains the majority of the source code.
  - **`components/`**: Contains all the React components, organized by feature (e.g., `auth`, `car`, `rent`, `sale`).
    - **`app/`**: The main application component (`App.jsx`).
    - **`auth/`**: Components related to user authentication (login, registration).
    - **`car/`**: Components for managing and displaying cars.
    - **`common/`**: Shared components like navigation, footer, and not-found page.
    - **`hoc/`**: Higher-order components for adding functionality to other components.
    - **`home/`**: The home page component.
    - **`rent/`**: Components for managing rentals.
    - **`sale/`**: Components for displaying sales information.
  - **`config/`**: Configuration files, such as the server URL.
  - **`context/`**: React Context providers for state management.
  - **`services/`**: Modules responsible for making API calls to the back-end.
  - **`style/`**: Global CSS styles.
  - **`util/`**: Utility functions and constants.
- **`public/`**: Contains the main HTML file (`index.html`) and other static assets.

## Components

The application is built using a component-based architecture. Here are some of the key components:

- **`App.jsx`**: The root component of the application. It sets up the routing and global state providers.
- **`Navigation.jsx`**: The main navigation bar, which displays different links based on the user's authentication status and role.
- **`Home.jsx`**: The landing page of the application.
- **`LoginForm.jsx` and `RegisterForm.jsx`**: Forms for user login and registration.
- **`AllCars.jsx`**: Displays a list of all available cars.
- **`CarDetails.jsx`**: Shows the details of a specific car.
- **`PrivateRoute.jsx`**: A higher-order component that protects routes based on user authentication and roles.

## Services

The application communicates with the back-end API through a set of services located in the `src/services` directory.

- **`fetcher.js`**: A wrapper around the `fetch` API that simplifies making HTTP requests and handling responses.
- **`authService.js`**: Handles user authentication (login, registration, logout).
- **`carService.js`**: Manages all API calls related to cars (fetching, creating, editing, deleting).
- **`rentService.js`**: Manages all API calls related to rentals.
- **`saleService.js`**: Manages all API calls related to sales.

## Routing

Routing is handled by the `react-router-dom` library. The main routes are defined in `App.jsx`. The application uses a combination of public and private routes.

- **Public Routes**: Accessible to everyone (e.g., `/login`, `/register`, `/`).
- **Private Routes**: Only accessible to authenticated users with specific roles (e.g., `/cars/create` for admins, `/sales/all/:username` for users). The `PrivateRoute.jsx` component enforces these restrictions.

## State Management

The application uses React's Context API for managing global state.

- **`UserContext`**: Stores information about the currently logged-in user, such as their username, role, and authentication status.
- **`DatesContext`**: Stores the start and end dates selected by the user for a car rental.

## Authentication

Authentication is handled using JSON Web Tokens (JWT). When a user logs in, the back-end sends a JWT, which is stored in the browser's local storage. This token is then sent with every subsequent request to the back-end to authenticate the user. The `authService.js` and the `PrivateRoute.jsx` component are the main parts of the authentication system.

## Error Handling

The `GlobalErrorHandler.jsx` component is used to catch and handle application-wide errors. It provides a fallback UI in case of an unexpected error, preventing the application from crashing.
