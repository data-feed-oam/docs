# Sports Odds Feed

This service provides an **odds feed** for:
- Football
- Basketball
- Tennis

The architecture consists of:
1. **Initial snapshot via REST API** (events, extras, players).  
2. **Real-time updates via RabbitMQ**.  

Access is allowed **only from whitelisted IPs**.  
