# Tapco Microservice Communication Demo (.NET 8, C#)

Patterns demonstrated:
1. Synchronous HTTP: Policy -> Rating `/api/ratings/calculate`
2. Asynchronous HTTP: `POST /api/policies/async` returns 202 + status URL
3. gRPC: Policy -> Rating `RatingGrpc.Calculate`
4. Message queue: RabbitMQ `installment.jobs` (one competing consumer)
5. Pub/Sub: RabbitMQ fanout `policy.broadcast` -> notification + analytics queues
6. Event-driven: RabbitMQ topic `insurance.events`, event `policy.issued.v1`

## Run
1. Start RabbitMQ: `docker compose up -d`
2. Open `Tapco.CommunicationDemo.sln` in Visual Studio.
3. Set Rating.Service, Policy.Service, Notification.Worker as startup projects.
4. Run. Rating REST listens on http://localhost:5101, gRPC on http://localhost:5103; Policy on http://localhost:5102.
5. Use `Tapco.http`.

The HTTP-async sample is intentionally 202 + polling. `await HttpClient.SendAsync(...)` remains request/response and is not architectural asynchronous communication.
