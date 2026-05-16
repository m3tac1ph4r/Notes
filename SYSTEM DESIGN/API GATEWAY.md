## **1. What is an API Gateway?**

An API Gateway acts as a **single entry point** for all client requests in a microservices architecture. It functions like a hotel front desk, shielding clients from the internal complexity of the backend services.

## **2. Core Responsibilities**

While its primary job is **request routing**, it handles several "cross-cutting concerns" (middleware):

- **Request Validation:** Checks for proper formatting, required headers, and valid payloads before they reach backend services.
    
- **Authentication & Authorization:** Verifies identities (e.g., via JWT tokens).
    
- **Rate Limiting:** Prevents abuse by limiting the number of requests a client can make.
    
- **SSL Termination:** Handles encrypted connections to offload work from backend services.
    
- **Protocol Translation:** Can convert client-side protocols (HTTP) to internal ones (gRPC).
    
- **Response Transformation:** Formats backend data into a consistent structure for the client.
    
- **Caching:** Stores frequently accessed, non-user-specific data to reduce latency.
    

## **3. Scaling Strategies**

- **Horizontal Scaling:** Since gateways are typically stateless, you can add more instances behind a load balancer.
    
- **Global Distribution:** Deploying gateways in multiple regions (using GeoDNS) to bring the entry point closer to the user, similar to a CDN.
    

## **4. Popular Solutions**

|**Category**|**Examples**|
|---|---|
|**Managed (Cloud)**|[AWS API Gateway](https://aws.amazon.com/api-gateway/), [Azure API Management](https://azure.microsoft.com/en-us/services/api-management/), [Google Cloud Endpoints](https://cloud.google.com/endpoints)|
|**Open Source**|[Kong](https://konghq.com/kong/), [Tyk](https://tyk.io/), [Express Gateway](https://www.express-gateway.io/)|

## **5. Interview Tips**

- **When to use:** Propose an API Gateway for **microservices** architectures. Avoid it for simple monolithic apps to prevent unnecessary complexity.
    
- **Don't overthink it:** In an interview, don't spend more than 30 seconds on it. Mention it handles "routing and basic middleware," draw the box, and move on to the core logic of your system.