
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

3. **Run the Setup Commands:**
   - Set the necessary file permissions:
     ```
     sudo chmod -R 777 *
     ```
     (This command grants read, write, and execute permissions to all files in the directory.)
   - Start the Docker containers:
     ```
     docker-compose up -d
     ```
     (This command runs your Docker containers in detached mode, allowing the terminal to be used for other commands while the containers run in the background.)

4. **Access WordPress:**
   Once the containers are up and running, access the WordPress setup wizard by navigating to `http://localhost` in your web browser.

5. **Complete WordPress Setup:**
   Follow the on-screen instructions in the WordPress setup wizard to complete the installation.

6. **Post-Setup Instructions:**
   - To stop the Docker containers, run:
     ```
     docker-compose down
     ```
   - To view logs of your Docker containers, use:
     ```
     docker-compose logs
     ```

## Working with Themes and Plugins

Post-setup, you will find the default WordPress themes and plugins installed. This setup allows you to create or modify themes and plugins directly within these folders. Any changes you make will be reflected in real-time on your local development site.

## Personal Note

With over a decade of experience in creating WordPress plugins, I've found this Docker-based environment to be my preferred setup. It's efficient, straightforward, and mirrors the production environment closely, making the development process much smoother.

I hope you find this setup as useful as I have. Happy coding!
