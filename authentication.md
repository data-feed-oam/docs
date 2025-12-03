# Authentication & Security

- Access to the service is based on an **IP whitelist**.  
- No API key or Bearer Token is required.  
- Requests from unauthorized IPs will receive a `403 Forbidden` response.  

## Rate Limiting
- **REST API**: 100 requests per minute per IP.  
- **RabbitMQ**: No rate limit, but it is recommended to maintain a single persistent connection per client.  
