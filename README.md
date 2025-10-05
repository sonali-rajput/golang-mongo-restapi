# Golang and MongoDB REST API

A simple RESTful API built with Golang and MongoDB for user management. This project demonstrates how to create a REST API with CRUD operations using Go's `httprouter` and MongoDB's official Go driver.

## 🚀 Features

- **Create User**: Add new users to the database
- **Get User**: Retrieve user information by ID
- **Delete User**: Remove users from the database
- **MongoDB Integration**: Uses MongoDB as the database with proper connection handling
- **Docker Support**: Includes Docker Compose for easy MongoDB setup
- **JSON API**: RESTful endpoints that return JSON responses

## 🛠️ Tech Stack

- **Backend**: Go 1.24.4
- **Database**: MongoDB (latest)
- **Router**: httprouter
- **MongoDB Driver**: go.mongodb.org/mongo-driver
- **Containerization**: Docker & Docker Compose

## 📋 Prerequisites

Before running this project, make sure you have the following installed:

- [Go](https://golang.org/dl/) (version 1.24.4 or higher)
- [Docker](https://www.docker.com/get-started) and Docker Compose
- [Git](https://git-scm.com/)

## 🏗️ Project Structure

```
golang-mongo-restapi/
├── controllers/
│   └── user.go          # User controller with HTTP handlers
├── models/
│   └── user.go          # User model definition
├── main.go              # Application entry point
├── docker-compose.yml   # MongoDB Docker configuration
├── go.mod              # Go module dependencies
└── go.sum              # Go module checksums
```

## 🚀 Getting Started

### 1. Clone the Repository

```bash
git clone <repository-url>
cd golang-mongo-restapi
```

### 2. Start MongoDB with Docker Compose

```bash
docker-compose up -d
```

This will start a MongoDB instance with the following configuration:
- **Host**: localhost:27017
- **Username**: mongoadmin
- **Password**: password
- **Database**: mongo-golang
- **Collection**: users

### 3. Install Dependencies

```bash
go mod tidy
```

### 4. Run the Application

```bash
go run main.go
```

The API server will start on `http://localhost:8080`

## 📡 API Endpoints

### Create User
- **POST** `/user`
- **Description**: Create a new user
- **Request Body**:
  ```json
  {
    "name": "John Doe",
    "gender": "Male",
    "age": 30
  }
  ```
- **Response**: Returns the created user with generated ID

### Get User
- **GET** `/user/{id}`
- **Description**: Retrieve user by ID
- **Parameters**: `id` (MongoDB ObjectID)
- **Response**: Returns user information or 404 if not found

### Delete User
- **DELETE** `/user/{id}`
- **Description**: Delete user by ID
- **Parameters**: `id` (MongoDB ObjectID)
- **Response**: Confirmation message or 404 if not found

## 📝 Data Model

### User
```go
type User struct {
    Id     primitive.ObjectID `json:"id" bson:"_id"`
    Name   string             `json:"name" bson:"name"`
    Gender string             `json:"gender" bson:"gender"`
    Age    int                `json:"age" bson:"age"`
}
```

## 🧪 Testing the API

You can test the API using tools like Postman, curl, or any HTTP client:

### Create a User
```bash
curl -X POST http://localhost:8080/user \
  -H "Content-Type: application/json" \
  -d '{"name":"John Doe","gender":"Male","age":30}'
```

### Get a User
```bash
curl http://localhost:8080/user/{user-id}
```

### Delete a User
```bash
curl -X DELETE http://localhost:8080/user/{user-id}
```

## 🐳 Docker Commands

### Start MongoDB
```bash
docker-compose up -d
```

### Stop MongoDB
```bash
docker-compose down
```

### View MongoDB Logs
```bash
docker-compose logs mongo
```

### Access MongoDB Shell
```bash
docker-compose exec mongo mongosh -u mongoadmin -p password --authenticationDatabase admin
```

## 🔧 Configuration

The application uses the following default configuration:

- **Server Port**: 8080
- **MongoDB URI**: `mongodb://mongoadmin:password@localhost:27017/?authSource=admin`
- **Database**: mongo-golang
- **Collection**: users
- **Connection Timeout**: 10 seconds

To modify these settings, update the respective values in `main.go`.

## 📦 Dependencies

Key dependencies used in this project:

- `github.com/julienschmidt/httprouter` - HTTP router and URL matcher
- `go.mongodb.org/mongo-driver` - MongoDB driver for Go
- Standard Go packages: `context`, `encoding/json`, `net/http`, `time`

## 🤝 Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📄 License

This project is open source and available under the [MIT License](LICENSE).

## 🐛 Troubleshooting

### Common Issues

1. **MongoDB Connection Error**: Ensure Docker is running and MongoDB container is started with `docker-compose up -d`

2. **Port Already in Use**: If port 8080 is occupied, modify the port in `main.go` or stop the conflicting service

3. **Module Not Found**: Run `go mod tidy` to download all dependencies

4. **Invalid ObjectID**: Ensure you're using valid MongoDB ObjectID format (24 character hex string) when making requests

### MongoDB Connection Issues
```bash
# Check if MongoDB is running
docker-compose ps

# Restart MongoDB
docker-compose restart mongo

# Check MongoDB logs
docker-compose logs mongo
```

## 📚 Learning Resources

This project is a great starting point for learning:
- Go web development
- MongoDB integration with Go
- RESTful API design
- Docker containerization
- HTTP routing in Go

## 🙏 Acknowledgments

- [Go MongoDB Driver](https://github.com/mongodb/mongo-go-driver)
- [httprouter](https://github.com/julienschmidt/httprouter)
- [MongoDB Docker Image](https://hub.docker.com/_/mongo)
