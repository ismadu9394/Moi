# Moi
version: '3'

services:

  # Re
  frontend:
    ports:
        - 3000:3000
    build: ./frontend
    container_name: re-app

  # data base 
  mongodb:
    image: mongo:latest
    container_name: mongo
    volumes: 
      - 'mongo-data:/data/db'
    networks:
      - backend

  # nodejs pour communiquer avec mongodb
  backend:
    build: ./backend
    container_name: nodejs
    ports:
     - 8080:8080 
    environment:
      - MONGO_URI=mongodb://mongo:27017/dbdev
    depends_on:
      - mongodb
    networks:
      - backend

# Volume donnee

  volumes:
    mongo-data:

  networks:
    backend:
        driver: bridge
