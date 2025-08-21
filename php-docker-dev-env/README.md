# php-docker-dev-env

A reusable Docker-based PHP development environment with PHP 8.2 (FPM), Nginx, MySQL, and phpMyAdmin.  
Supports multiple PHP projects simultaneously, each accessible via custom local domains (e.g., `project1.local`, `project2.local`).

This setup works for **Laravel**, **WordPress**, or any PHP project.

## Features

- PHP 8.2 with FPM
- Nginx web server
- MySQL 8.0 database
- phpMyAdmin for database management
- Multi-project support with local domains
- Reusable single container setup for multiple projects

## Project Structure

```
php-docker-dev-env/
│── docker-compose.yml
│── php/
│   └── Dockerfile
│── nginx/
│   └── projects.conf
│── projects/
    ├── project1/   (Your PHP/Laravel/WordPress app)
    ├── project2/
```

## Setup Instructions

### 1. Clone the repository
```bash
git clone https://github.com/yourusername/php-docker-dev-env.git
cd php-docker-dev-env
```

### 2. Add your projects
Put your PHP/Laravel projects inside the `projects/` folder:
```
projects/
├── project1/
├── project2/
```

### 3. Update your hosts file
Add entries for each project:
```
127.0.0.1 project1.local
127.0.0.1 project2.local
```

- Linux / Mac: `/etc/hosts`  
- Windows: `C:\Windows\System32\drivers\etc\hosts`

### 4. Start Docker containers
```bash
docker-compose up -d --build
```

### 5. Access your projects
- PHP projects / Laravel apps: `http://project1.local`  
- phpMyAdmin: `http://localhost:3407` (or `http://localhost:80` if port 80 is mapped)

### 6. Database configuration
Inside your project’s `.env` or config files:
```
DB_CONNECTION=mysql
DB_HOST=db
DB_PORT=3306
DB_DATABASE=project1  # separate DB per project
DB_USERNAME=root
DB_PASSWORD=root
```

## Adding New Projects

1. Create a new folder under `projects/`:
```
projects/project3/
```

2. Add a corresponding server block in `nginx/projects.conf` or use a catch-all setup.

3. Add to hosts file:
```
127.0.0.1 project3.local
```

4. Restart Docker:
```bash
docker-compose restart nginx
```

## Notes

- Use this environment for **local development only**. Do not expose MySQL root password to production.
- Can be used for any PHP project (Laravel, WordPress, custom apps, etc.).
- Reuse the same containers for multiple projects to save resources.

## License
MIT License
