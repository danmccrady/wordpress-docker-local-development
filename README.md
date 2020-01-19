# wordpress-docker-local-dev
Quickly spin up a wordpress site for local development.  This docker-compose file maps the themes & plugins folders to your local machine so that you can quickly edit them for development.  There is no need to install and setup WAMP or LAMP.  This is the quickest way to spin up a WordPress development environment. 

## Prerequisite
* docker
```javascript
sudo snap install docker
```
* docker-compose
```javascript
sudo apt install docker-compose
```

## Setup
* Clone this repo to your local machine
* Open a terminal window and navigate to the repo directory
* Run the following commands:
```javascript
sudo chmod -R 777 *
docker-compose up -d
```
* Browse to http://localhost and follow the WordPress setup wizard
* Done!

## Themes/Plugins
After running the WordPress setup wizard, you'll notice the default themes/plugins which are installed by WordPress.  You can now create your own themes/plugins directly in these folders and the changes will reflect on the development site in real time.

I've been creating WordPress plugins for over 10 years and this is my preferred setup now.  Enjoy!
