# Getting Started

1. Request to have your IP whitelisted by contacting technical support.  
2. When starting the client:  
   - Call the REST APIs to download the initial snapshot  
   - Connect to RabbitMQ to receive real-time updates  

## Available bookmakers

All endpoints that require a `bookmaker` / `bookmakerId` parameter expect the **bookmaker identifier** (numeric ID, serialized as a string in the URL/path), not the bookmaker name.

To map `id → name` (and see the full list of supported bookmakers), use the dedicated lookup file:

- Download: [bookmakers.json](./static/bookmakers.json)
