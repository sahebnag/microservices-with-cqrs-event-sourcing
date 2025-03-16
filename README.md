# microservices-with-cqrs-event-sourcing
![Architecture Diagram](microservices-with-cqrs-event-sourcing/OrderManagementMicroservices
/Architecture/OrderManagement_success_scenario_with_crqs_event_sourcing.jpg)


/OrderManagementMicroservices
├── /Architecture
│   └── OrderManagement_HLD.jpg   <-- Put your architecture diagram here
├── /OrderService
│   ├── Program.cs
│   ├── Controllers/
│   ├── Models/
│   └── Services/
├── /PaymentService
│   ├── Program.cs
│   ├── Controllers/
│   ├── Models/
│   └── Services/
├── /ShipmentService
│   ├── Program.cs
│   ├── Controllers/
│   ├── Models/
│   └── Services/
├── /EventSourcingService
│   └── (Optional storage/memory event store)
├── docker-compose.yml  <-- Optional if you want to run RabbitMQ/Kafka + all services together
├── README.md
└── .gitignore



1. **Order Microservice**  
   - Handles order creation.
   - Publishes `OrderPlacedEvent` to the message broker.
   - Persists order data in Order DB.

2. **Payment Microservice**  
   - Listens for `OrderPlacedEvent`.
   - Processes payment and publishes `PaymentSuccessEvent`.
   - Stores payment details in Payment DB.

3. **Shipment Microservice**  
   - Listens for `PaymentSuccessEvent`.
   - Processes shipment and publishes `ShipmentPlacedEvent`.
   - Stores shipment details in Shipment DB.

4. **Event Sourcing Service**  
   - Stores all domain events in event storage (memory/file/DB).
   - Ensures audit trail and replayability.

5. **Read-Only Analytics DB**  
   - Updated by all events for querying purposes.

## 🚀 Tech Stack

- .NET 6
- RabbitMQ / Kafka
- PostgreSQL / SQL Server (write DBs + analytics DB)
- Docker / Kubernetes (Optional)

---
