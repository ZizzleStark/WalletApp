
E-Wallet Application


Overview
The E-Wallet Application is a microservices-based system designed to provide digital wallet functionality. It allows users to manage their accounts, perform transactions, and receive notifications. The application is built using Spring Boot and follows a microservices architecture for scalability and maintainability.

System Architecture
The application consists of four main microservices:
![Architecture](https://github.com/user-attachments/assets/61a121da-9f03-4e84-b1a1-5d5d99c8905a)


User Service: Manages user accounts and authentication.
Wallet Service: Handles user wallets and balances.
Transaction Service: Manages money transfers between wallets.
Notification Service: Sends notifications to users based on system events.
These services communicate with each other via RESTful APIs and use Apache Kafka for event-driven communication.

Technology Stack
Java: 17
Spring Boot
Spring Security
Spring Data JPA
PostgreSQL
Redis
Apache Kafka
Maven


Microservices Overview
1. User Service
Responsible for user management and authentication.

Key Components:

UserController: Handles user-related HTTP requests
UserService: Implements business logic for user operations
User: Entity representing user data
UserRepository: Interface for database operations
SecurityConfig: Configures security settings
RedisConfig: Configures Redis for caching
Database:

PostgreSQL for persistent storage
Redis for caching


2. Wallet Service
Manages user wallets and balances.

Key Components:

WalletController: Handles wallet-related HTTP requests
WalletService: Implements business logic for wallet operations
Wallet: Entity representing wallet data
WalletRepository: Interface for database operations
Database:

PostgreSQL


3. Transaction Service
Handles money transfers between wallets.

Key Components:

TransactionController: Handles transaction-related HTTP requests
TransactionService: Implements business logic for transactions
Transaction: Entity representing transaction data
TransactionDao: Interface for database operations
KafkaConfig: Configures Kafka for event publishing
Database:

PostgreSQL
Event Streaming:
Kafka



4. Notification Service
Sends notifications to users based on system events.

Key Components:

NotificationService: Listens to Kafka topics and sends notifications
EmailConfig: Configures email sending capabilities
KafkaConfig: Configures Kafka for consuming events
Event Streaming:
Kafka


Data Flow
User Registration ->
User Service receives a registration request. ->
Creates user in PostgreSQL. ->
Publishes user creation event to Kafka. ->
Wallet Service listens to the event and creates a wallet for the user. ->
Transaction Process ->
Transaction Service receives a transaction request. ->
Validates the transaction and updates wallet balances via Wallet Service. ->
Records transaction in PostgreSQL. ->
Publishes transaction event to Kafka. ->
Notification Service consumes the event and sends notifications.



API Documentation


User Service APIs:

POST /user/create: Create a new user

GET /user/profile-info: Get user profile information

GET /user/username/{username}: Get user details by username

Wallet Service APIs:

POST /wallet/update: Update wallet balance


Transaction Service APIs:

POST /transaction/initiate: Initiate a new transaction



Security
Spring Security is implemented for authentication and authorization.
Passwords are encrypted using BCrypt.
JWT tokens are used for maintaining user sessions.


Caching
Redis is used in the User Service for caching frequently accessed user data.


Event Streaming
Kafka is used for asynchronous communication between services.
Key topics include: user_created, transaction_completed.


Monitoring and Logging
Spring Actuator for health checks and metrics.
ELK Stack (Elasticsearch, Logstash, Kibana) for centralized logging.


Future Enhancements
Implement circuit breakers for improved fault tolerance.
Add more sophisticated fraud detection in the Transaction Service.
Expand notification channels (e.g., SMS, push notifications).
