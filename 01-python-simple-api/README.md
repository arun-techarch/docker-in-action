## FastAPI Project Setup and Docker Deployment Guide

This guide provides step-by-step instructions to create and configure a FastAPI project within a virtual environment. It also includes detailed steps for:
- Building a Docker image of the FastAPI application
- Deploying and running the application inside a Docker container
- Testing and exploring APIs through the built-in Swagger UI documentation

By following this guide, you will have a fully containerized FastAPI application that is easy to build, run, and test in local environment.

### 🚀 Project Creation
---

Follow these steps to create a new project from scratch:
1. Create a new project folder

    ```sh
    mkdir simple-api
    cd simple-api
    ```
2. Create and activate a virtual environment

    ```sh
    python -m venv pyenv
    pyenv/Scripts/activate     # Windows
    # source pyenv/bin/activate # Linux / MacOS
    ```
3. Upgrade pip to the latest version
    ```sh
    python -m pip install --upgrade pip
    ```
4. Install project dependencies
    ```sh
    pip install uvicorn[standard] fastapi
    ```
5. Save dependencies to requirements.txt
    ```sh
    pip freeze > requirements.txt
    ```
### 🔧 Project Setup (from GitHub)
---
1. Clone the repository
    ```sh
    git clone <github_repo>
    cd project_folder
    ```
2. Create and activate a virtual environment
    ```sh
    python -m venv pyenv
    pyenv/Scripts/activate     # Windows
    # source pyenv/bin/activate # Linux / MacOS
    ```
3. Upgrade pip to the latest version
    ```sh
    python -m pip install --upgrade pip
    ```
4. Install dependencies from requirements.txt
    ```sh
    pip install -r requirements.txt
    ```

### Running the Application with Docker

1. Navigate to the project directory  
   Ensure you are in the directory containing the `Dockerfile`.

2. Build the Docker image
    ```bash
    docker build -t python-api .
    ```
3. Verify the image creation
    ```sh
    docker images
    ```
4. Run the Docker container
    ```sh
    docker run -d -p 8000:8000 python-api
    ```
- -d runs the container in detached mode.
- -p 8000:8000 maps container port 8000 to host port 8000.

5. Check the application logs from docker container

    ```sh
    docker container logs -f <container_id>
    ```

### API Testing
---
* Open http://127.0.0.1:8000
 → root endpoint
* Open http://127.0.0.1:8000/docs
 → interactive Swagger UI


```sh
GET http://127.0.0.1:8000/

Response:
{
  "message": "Welcome to FastAPI running with Uvicorn!"
}
```
```sh
GET http://127.0.0.1:8000/hello/{name}

Example:
http://127.0.0.1:8000/hello/Arun 

Response:
{
  "message": "Hello, Arun!"
}
```
```sh
POST http://127.0.0.1:8000/items/

Payload:
{
  "id": 1,
  "name": "Laptop",
  "price": 30000.50,
  "in_stock": true
}

Response:
{
  "message": "Item created successfully",
  "item": {
    "id": 1,
    "name": "Laptop",
    "price": 30000.5,
    "in_stock": true
  }
}
```
```sh
PUT http://127.0.0.1:8000/items/{id}

Example:
http://127.0.0.1:8000/items/1

Payload:
{
  "id": 1,
  "name": "Laptop",
  "price": 40000.50,
  "in_stock": true
}

Response:
{
  "message": "Item 1 updated successfully",
  "item": {
    "id": 1,
    "name": "Laptop",
    "price": 40000.5,
    "in_stock": true
  }
}
```
```sh
GET http://127.0.0.1:8000/items/{id}

Example:
http://127.0.0.1:8000/items/1

Response:
{
  "message": "Item 1 retrieved successfully",
  "item": {
    "id": 1,
    "name": "Laptop",
    "price": 40000.5,
    "in_stock": true
  }
}
```
```sh
GET http://127.0.0.1:8000/items

Response:
{
  "message": "All Items retrieved successfully",
  "items": [
    {
      "id": 1,
      "name": "Laptop",
      "price": 40000.5,
      "in_stock": true
    },
    {
      "id": 2,
      "name": "Mobile",
      "price": 25000.5,
      "in_stock": true
    }
  ]
}
```
```sh
DELETE http://127.0.0.1:8000/items/{id}

Example:
http://127.0.0.1:8000/items/1

Response:
{
  "message": "Item 1 successfully removed",
  "item": {
    "id": 1,
    "name": "Laptop",
    "price": 40000.5,
    "in_stock": true
  }
}
```

> **Note:** The application uses in-memory storage. Data is **not persisted** and will be lost upon application restart.
