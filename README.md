The E-Wallet Application is a microservices-based system designed to provide digital wallet functionality. It allows users to manage their accounts, perform transactions, and receive notifications. The application is built using Spring Boot and follows a microservices architecture for scalability and maintainability.

System Architecture

The application consists of four main microservices:

User Service
Wallet Service
Transaction Service
Notification Service

These services communicate with each other via RESTful APIs and use Kafka for event-driven communication.


2.1 Technology Stack
Java 17
Spring Boot
Spring Security
Spring Data JPA
PostgreSQL
Redis
Apache Kafka
Maven



3. Microservices Overview


3.1 User Service
Responsible for user management and authentication.
Key Components:
UserController: Handles user-related HTTP requests
UserService: Implements business logic for user operations
User: Entity representing user data
UserRepository: Interface for database operations
SecurityConfig: Configures security settings
RedisConfig: Configures Redis for caching
Database: PostgreSQL for persistent storage, Redis for caching



3.2 Wallet Service


Manages user wallets and balances.

Key Components:
WalletController: Handles wallet-related HTTP requests
WalletService: Implements business logic for wallet operations
Wallet: Entity representing wallet data
WalletRepository: Interface for database operations
Database: PostgreSQL


3.3 Transaction Service

Handles money transfers between wallets.

Key Components:
TransactionController: Handles transaction-related HTTP requests
TransactionService: Implements business logic for transactions
Transaction: Entity representing transaction data
TransactionDao: Interface for database operations
KafkaConfig: Configures Kafka for event publishing
Database: PostgreSQL Event Streaming: Kafka



3.4 Notification Service

Sends notifications to users based on system events.

Key Components:
NotificationService: Listens to Kafka topics and sends notifications
EmailConfig: Configures email sending capabilities
KafkaConfig: Configures Kafka for consuming events
Event Streaming: Kafka




4. Data Flow

User Registration:
User Service receives registration request
Creates user in PostgreSQL
Publishes user creation event to Kafka
Wallet Service listens to event and creates a wallet for the user

Transaction Process:
Transaction Service receives transaction request
Validates transaction and updates wallet balances via Wallet Service
Records transaction in PostgreSQL
Publishes transaction event to Kafka

Notification Service consumes event and sends notifications


5. API Documentation

5.1 User Service APIs
POST /user/create: Create a new user
GET /user/profile-info: Get user profile information
GET /user/username/{username}: Get user details by username

5.2 Wallet Service APIs
POST /wallet/update: Update wallet balance

5.3 Transaction Service APIs
POST /transaction/initiate: Initiate a new transaction


6. Security
Spring Security is implemented for authentication and authorization
Passwords are encrypted using BCrypt
JWT tokens are used for maintaining user sessions


7. Caching
Redis is used in the User Service for caching frequently accessed user data



8. Event Streaming

Kafka is used for asynchronous communication between services
Key topics: user_created, transaction_completed



9. Monitoring and Logging
Spring Actuator for health checks and metrics
ELK stack (Elasticsearch, Logstash, Kibana) for centralized logging




10. Future Enhancements
Implement circuit breakers for improved fault tolerance
Add more sophisticated fraud detection in Transaction Service
Expand notification channels (e.g., SMS, push notifications)
