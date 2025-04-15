# Ticket System API

A Laravel-based RESTful API for managing support tickets. The system includes user authentication, role-based access control, ticket management, and commenting capabilities.

## Features

-   **Authentication**: JWT-based authentication using Laravel Sanctum
-   **User Management**: Support for staff and admin roles
-   **Ticket Management**: Create, read, update, and delete support tickets
-   **Comment System**: Add and manage comments on tickets (admin only)
-   **Priority Levels**: Support for different ticket priority levels (low, medium, high, critical)
-   **Status Tracking**: Track ticket status (open, in_progress, resolved)
-   **Assignment**: Assign tickets to specific users

## Requirements

-   Docker and Docker Compose
-   PHP 8.2 or higher (for local development without Docker)
-   Composer (for local development without Docker)

## Quick Start with Docker

1. Clone the repository
2. Copy the environment file:

    ```bash
    cp .env.example .env
    ```

3. Configure your `.env` file with your database credentials:

    ```
    DB_CONNECTION=mysql
    DB_HOST=db
    DB_PORT=3306
    DB_DATABASE=your_database_name
    DB_USERNAME=your_username
    DB_PASSWORD=your_password
    ```

4. Start the Docker containers:

    ```bash
    docker compose up -d
    ```

5. Run migrations and seed the database:
    ```bash
    docker compose exec app php artisan migrate
    docker compose exec app php artisan db:seed
    ```

The API will be available at `http://localhost:8000`

## Default Admin User

After seeding the database, you can use these credentials:

-   Email: john.admin@gmail.com
-   Role: admin

## Docker Commands

-   **Start containers**: `docker compose up -d`
-   **Stop containers**: `docker compose down`
-   **View logs**: `docker compose logs`
-   **Execute commands in app container**: `docker compose exec app <command>`
-   **Access MySQL**: `docker compose exec db mysql -u your_username -pyour_password`

## API Endpoints

### Authentication

-   `POST /api/login` - Login user
-   `POST /api/logout` - Logout user (requires auth)
-   `POST /api/register` - Register new user (requires admin auth)

### Users

-   `GET /api/users` - List all users (requires auth)
-   `GET /api/user` - Get authenticated user details (requires auth)

### Tickets

-   `GET /api/tickets` - List all tickets (requires auth)
-   `POST /api/tickets` - Create a new ticket (requires auth)
-   `GET /api/tickets/{id}` - Get ticket details (requires auth)
-   `PUT /api/tickets/{id}` - Update ticket (requires auth)
-   `DELETE /api/tickets/{id}` - Delete ticket (requires auth)

### Comments (Admin Only)

-   `GET /api/comments` - List all comments
-   `POST /api/comments` - Add a comment to a ticket
-   `GET /api/comments/{id}` - Get comment details
-   `PUT /api/comments/{id}` - Update comment
-   `DELETE /api/comments/{id}` - Delete comment

## Ticket Properties

-   **Status**: open, in_progress, resolved
-   **Priority**: low, medium, high, critical
-   **Fields**:
    -   title (string, required)
    -   description (string, required)
    -   status (enum)
    -   priority (enum)
    -   assigned_to (user_id)

## Development

For local development without Docker:

1. Install dependencies:

    ```bash
    composer install
    ```

2. Configure your local environment
3. Run migrations and seeders:

    ```bash
    php artisan migrate --seed
    ```

4. Start the development server:
    ```bash
    php artisan serve
    ```

## Database Connection

-   **Local Access**: localhost:33066
-   **Docker Network Access**: db:3306
-   **Default Database**: ticket_system_api
