
# WordPress Docker Local Development

## Introduction
Welcome to the WordPress Docker Local Development repository! This setup is designed for developers seeking a streamlined and efficient method to establish a local WordPress development environment. Utilizing Docker, this configuration bypasses the need for traditional WAMP or LAMP stack installations, offering a rapid and straightforward setup process.

Our Docker-compose configuration uniquely maps the themes and plugins directories to your local machine. This allows for immediate and direct editing, making the development cycle significantly faster and more intuitive.

## Prerequisites
Before you begin, ensure you have Docker and Docker-compose installed on your machine. Docker is a platform to develop, ship, and run applications inside containers, and Docker-compose is a tool for defining and running multi-container Docker applications.

### For Windows:
1. **Docker Desktop for Windows:**
   - Visit the [Docker website](https://www.docker.com/products/docker-desktop) to download Docker Desktop for Windows.
   - Run the installer and follow the on-screen instructions.
   - Docker Desktop includes Docker-compose, so no separate installation is necessary.

### For Mac:
1. **Docker Desktop for Mac:**
   - Navigate to the [Docker website](https://www.docker.com/products/docker-desktop) to download Docker Desktop for Mac.
   - Open the downloaded `.dmg` file and drag the Docker icon to the Applications folder.
   - Open Docker from the Applications folder, and Docker-compose will be included in the installation.

### For Linux:
1. **Docker:**
   - For most Linux distributions, Docker can be installed with a package manager. For example, on Ubuntu, use: `sudo snap install docker`.
2. **Docker-compose:**
   - Install Docker-compose using the package manager. For example, on Ubuntu, use: `sudo apt install docker-compose`.

## Setup Instructions

1. **Clone the Repository:**
   - Open a terminal or command prompt.
   - Run the following command to clone the repository:
     ```
     git clone https://github.com/danmccrady/wordpress-docker-local-development.git
     ```

2. **Navigate to the Repository Directory:**
   - In the terminal, change to the repository directory with:
     ```
     cd wordpress-docker-local-development
     ```

3. **Create your local environment file:**
    - Copy the example environment file:
       ```
       cp .env.example .env
       ```
    - Optionally edit `.env` to change ports, DB credentials, or image tags.

4. **Start the containers:**
    ```
    docker compose up -d
    ```
    (This runs containers in detached mode.)

4. **Access WordPress:**
   Once the containers are up and running, access the WordPress setup wizard at:

   - `http://localhost:8080` (default)

   If you changed `WP_PORT` in `.env`, use that port instead.

5. **Complete WordPress Setup:**
   Follow the on-screen instructions in the WordPress setup wizard to complete the installation.

6. **Post-Setup Instructions:**
   - To stop the Docker containers, run:
     ```
       docker compose down
     ```
   - To view logs of your Docker containers, use:
     ```
       docker compose logs
     ```

## Common Commands

- **Reset everything (including the database):**
   ```
   docker compose down -v
   ```

- **Run WP-CLI commands:**
   ```
   docker compose run --rm wpcli wp core version
   docker compose run --rm wpcli wp plugin list
   ```

- **Start phpMyAdmin (optional):**
   ```
   docker compose --profile tools up -d
   ```
   Then open `http://localhost:8081` (default `PMA_PORT`).

## Troubleshooting

- **Port already in use** (common if you already run a web server locally):
   - Change `WP_PORT` (and/or `PMA_PORT`) in `.env`, then restart:
      ```
      docker compose up -d
      ```

- **WordPress can’t connect to the database**:
   - Check DB logs: `docker compose logs db`
   - If you edited credentials, ensure the same values are in `.env` for:
      - `WORDPRESS_DB_NAME`, `WORDPRESS_DB_USER`, `WORDPRESS_DB_PASSWORD`, `MYSQL_ROOT_PASSWORD`
   - If you need a clean slate, reset volumes:
      ```
      docker compose down -v
      docker compose up -d
      ```

- **File permission weirdness on macOS/Windows**:
   - Avoid `chmod -R 777` (it can create security + ownership problems).
   - If you hit write issues in `wp-content`, try restarting Docker Desktop and ensure the repo folder is shared in Docker Desktop settings.

- **Apple Silicon (M1/M2/M3) image compatibility**:
   - The default images used here support `arm64`. If you pinned an older tag and see platform errors, pick a newer tag or remove the pin.

- **phpMyAdmin shows `exec /docker-entrypoint.sh: exec format error` (Apple Silicon)**:
   - This usually means you’re running an `amd64`-only phpMyAdmin image on an `arm64` Mac.
   - Fix: ensure you’re using the `phpmyadmin:5` image (the Compose default) and you didn’t override `PHPMYADMIN_IMAGE` to `phpmyadmin/phpmyadmin`.
   - Then recreate containers:
      ```
      docker compose down
      docker compose --profile tools up -d
      ```

## Reproducibility (Pin Versions)

By default this repo uses reasonable modern defaults, but you can make it fully reproducible by pinning image tags in `.env`.

- In `.env`, set:
   - `WORDPRESS_IMAGE=wordpress:php8.3-apache`
   - `MYSQL_IMAGE=mysql:8.4`
   - (Optional) `WPCLI_IMAGE=wordpress:cli-php8.3`

## Optional: Use MariaDB Instead of MySQL

If you prefer MariaDB for local dev, set the DB image in `.env`:

```
MYSQL_IMAGE=mariadb:11
```

Then recreate the DB container (and volumes if you want a clean DB):

```
docker compose down
docker compose up -d
```

## Working with Themes and Plugins

Post-setup, you will find the default WordPress themes and plugins installed. This setup allows you to create or modify themes and plugins directly within these folders. Any changes you make will be reflected in real-time on your local development site.

## Personal Note

With over a decade of experience in creating WordPress plugins, I've found this Docker-based environment to be my preferred setup. It's efficient, straightforward, and mirrors the production environment closely, making the development process much smoother.

I hope you find this setup as useful as I have. Happy coding!
