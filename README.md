# Management API Project Documentation

## Overview
The Management API is a Java-based RESTful service that allows users to manage projects and tasks. It provides endpoints to create, retrieve, and delete projects and tasks. The API requires an API key for certain operations to ensure security.

---

## Features
1. **Project Management**
   - Create a new project.
   - Retrieve all projects.
   - Delete an existing project.

2. **Task Management**
   - Create a task for a specific project.
   - Retrieve all tasks across all projects.

3. **Security**
   - API key validation for protected endpoints.

---

## Prerequisites
1. **Java Development Kit (JDK)**: Version 11 or higher.
2. **Apache Maven**: For dependency management and building the project.
3. **Postman or Curl**: For testing the API.
4. **IDE (Optional)**: IntelliJ IDEA, Eclipse, or any preferred IDE.

---

## Getting Started

### 1. Clone the Repository
```bash
$ git clone <repository-url>
$ cd <repository-folder>
```

### 2. Build the Project
Ensure Maven is installed and configured correctly.
```bash
$ mvn clean install
```

### 3. Deploy the Application
You can deploy the application using any servlet container, such as Apache Tomcat or Jetty. For development, a lightweight solution like `mvn exec:java` can also be used.

Example using Tomcat:
1. Build the WAR file:
   ```bash
   $ mvn package
   ```
2. Deploy the WAR file to the Tomcat `webapps` directory.
3. Start Tomcat and access the application.

### 4. Access the API
The base URL for the API is:
```
http://localhost:8080/TaskManager/api/management
```

---

## API Endpoints

### 1. **Get All Projects**
- **Endpoint**: `/projects`
- **Method**: `GET`
- **Description**: Retrieve all available projects.
- **Example**:
  ```bash
  curl -X GET http://localhost:8080/TaskManager/api/management/projects
  ```

### 2. **Create a Project**
- **Endpoint**: `/projects`
- **Method**: `POST`
- **Description**: Create a new project.
- **Headers**:
  - `API-Key: 1234`
- **Body**:
  ```json
  {
      "name": "Project Alpha",
      "description": "Initial Test Project",
      "tasks": []
  }
  ```
- **Example**:
  ```bash
  curl -X POST http://localhost:8080/TaskManager/api/management/projects \
       -H "API-Key: 1234" \
       -H "Content-Type: application/json" \
       -d '{
           "name": "Project Alpha",
           "description": "Initial Test Project",
           "tasks": []
       }'
  ```

### 3. **Delete a Project**
- **Endpoint**: `/projects/{id}`
- **Method**: `DELETE`
- **Description**: Delete a project by its ID.
- **Headers**:
  - `API-Key: 1234`
- **Example**:
  ```bash
  curl -X DELETE http://localhost:8080/TaskManager/api/management/projects/1 \
       -H "API-Key: 1234"
  ```

### 4. **Create a Task**
- **Endpoint**: `/projects/{projectId}/tasks`
- **Method**: `POST`
- **Description**: Add a task to a specific project.
- **Headers**:
  - `API-Key: 1234`
- **Body**:
  ```json
  {
      "name": "Task 1",
      "description": "Sample task for Project Alpha",
      "status": "Pending"
  }
  ```
- **Example**:
  ```bash
  curl -X POST http://localhost:8080/TaskManager/api/management/projects/1/tasks \
       -H "API-Key: 1234" \
       -H "Content-Type: application/json" \
       -d '{
           "name": "Task 1",
           "description": "Sample task for Project Alpha",
           "status": "Pending"
       }'
  ```

### 5. **Get All Tasks**
- **Endpoint**: `/tasks`
- **Method**: `GET`
- **Description**: Retrieve all tasks across all projects.
- **Example**:
  ```bash
  curl -X GET http://localhost:8080/TaskManager/api/management/tasks
  ```

---

## Troubleshooting

### 1. Empty Array in Responses
- Ensure the `ManagementService` instance is static in the `ManagementResource` class.
- Verify that data is being correctly stored in the `projects` map.
- Add debug logs in the `ManagementService` class to track the data flow.

### 2. Invalid API Key
- Check the API key passed in the header. The valid key is `1234`.

### 3. Error Responses
- **400 Bad Request**: Ensure the request body is correctly formatted.
- **403 Forbidden**: Verify that the correct API key is provided.

---

## Future Improvements
1. **Database Integration**:
   - Replace in-memory storage with a database like MySQL or PostgreSQL for persistence.
2. **Pagination**:
   - Add pagination to the `/projects` and `/tasks` endpoints for scalability.
3. **Authentication**:
   - Implement robust authentication using JWT or OAuth2.
4. **Frontend Application**:
   - Develop a frontend to interact with the API using React or Angular.

---

## Conclusion
This Management API provides a very important foundation for managing projects and tasks. I have done all the steps by following what the brief required me to deliver. Anyone can set up and run the service, and extend it as needed for their specific requirements. The project has been committed to GitHub 

