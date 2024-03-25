## What is an API? 
Introduction: In the world of software development, APIs play a crucial role in enabling communication between different systems. Let's break down the basics of APIs, starting from the ground up.

What is an API? An API, or Application Programming Interface, acts as a middleman between software applications, allowing them to communicate and interact with each other. It provides a set of rules and protocols that define how different software components can work together.

The Need for APIs: Without an API, clients would have to directly communicate with backend services, leading to complexity and security challenges. APIs simplify this process by providing a standardized interface for clients to interact with, reducing exposure to services and streamlining communication.

The Role of APIs: An API serves as the "front door" to services, abstracting away the complexities of backend implementation. It acts as a central point for routing client requests to the appropriate services, enabling flexibility and scalability in system architecture.

API Routing: APIs intelligently route incoming requests based on predefined paths, allowing for the seamless integration of multiple services. This routing mechanism simplifies maintenance and enables collaboration across different teams and projects.

Protocols for API Communication: APIs communicate using various protocols such as REST, SOAP, GraphQL, RPC, gRPC etc. These protocols define how data is exchanged between clients and services, ensuring interoperability and performance.

![](images/intro/Screenshot%202024-03-20%20at%2011.14.42%20AM.png)

Contract Between API and Client:
The API defines a contract between itself and the client. This contract outlines the available endpoints, request and response formats, and any other relevant details. By adhering to this contract, both the API and the client can communicate effectively, regardless of the underlying changes to the services.

Protocols for API Communication:
When it comes to communication protocols, there are several options available. Among the most popular are:

1. REST: RESTful APIs are widely used for their simplicity and flexibility. They follow a stateless client-server architecture and leverage standard HTTP methods for communication.

2. WebSockets: WebSockets enable full-duplex communication channels over a single TCP connection. They are ideal for real-time applications that require low latency and high throughput.

3. SOAP: SOAP (Simple Object Access Protocol) is an older protocol primarily used for exchanging structured information in web services. While less common today, it still has its use cases, especially in enterprise environments.

4. gRPC: gRPC is a modern, high-performance RPC (Remote Procedure Call) framework developed by Google. It uses HTTP/2 as its underlying protocol and Protocol Buffers for efficient serialization.

APIG supports REST and WebSocket APIs. 
## Types of APIs

Amazon API Gateway offers different types of APIs, each serving specific purposes and utilizing various protocols. Understanding these API types is essential for effectively leveraging the capabilities of API Gateway. Let's delve into the nuances of Amazon API Gateway APIs and demystify their differences.

Types of Amazon API Gateway APIs:
Amazon API Gateway provides two primary types of APIs: REST API and HTTP API. While these names might initially seem confusing, let's break down their distinctions.

REST API:
The REST API offered by Amazon API Gateway supports both REST and WebSockets protocols. It serves as a full-featured service, providing robust functionality for building scalable and flexible APIs. Despite its name, the REST API is HTTP-based, offering a comprehensive solution for various use cases.

HTTP API:
Contrary to its name, the HTTP API provided by Amazon API Gateway is also a REST API. This might sound paradoxical, but it's essential to understand that both the REST API and HTTP API are HTTP-based APIs. The HTTP API, like its REST API counterpart, supports HTTP protocol and is designed to offer streamlined functionality for specific use cases.

Regional API:
All APIs deployed using Amazon API Gateway are inherently regional, meaning they are spun up in specific AWS regions. The Regional API, supported by both REST and HTTP API types, allows applications and services within the same region to access the API endpoints. While primarily regional, these APIs can be accessed from outside the region, albeit with potentially longer latency.

![](images/intro/Screenshot%202024-03-20%20at%2011.54.50%20AM.png)

Edge-Optimized API:
Exclusive to the REST API type, the Edge-Optimized API leverages CloudFront distribution to bring points of presence (POPs) closer to clients. This optimization enhances network performance by routing requests through Amazon's private network, reducing latency. However, it's essential to note that Edge-Optimized APIs do not include Edge-based caching, making them ideal for scenarios where caching is not feasible.

![](images/intro/Screenshot%202024-03-20%20at%2011.55.42%20AM.png)

Private API:
The Private API offered by Amazon API Gateway is designed for restricted access within a Virtual Private Cloud (VPC). It ensures that API endpoints are only accessible to entities within the VPC, enhancing security and privacy. Private APIs are commonly used for internal communication and data exchange within organizations.

Other AWS Services that the private API connects to should reside within the same VPC.

![](images/intro/Screenshot%202024-03-20%20at%2011.56.15%20AM.png)

## Understanding RPS and Burst

![](images/intro/Screenshot%202024-03-20%20at%2012.10.33%20PM.png)

Introduction:
Amazon API Gateway introduces rate limiting features to manage incoming requests effectively. Understanding the concepts of Requests Per Second (RPS) and Burst is crucial for optimizing API performance and preventing throttling issues. Let's delve into these concepts and clarify their nuances.

Requests Per Second (RPS):
RPS refers to the speed at which API Gateway refills the request bucket. It represents the maximum number of requests that API Gateway can handle per second. With a soft maximum of 10,000 RPS, API Gateway continuously refills the request bucket to maintain a steady flow of incoming requests. It's important to note that the RPS limit includes both initial burst requests and subsequent refill requests.

Burst:
The burst represents the number of concurrent requests that API Gateway can support simultaneously. It signifies the maximum number of requests that can be processed concurrently, with a hard maximum of 5,000 concurrent starts. Burst limits are enforced at the account level, meaning they apply to all API endpoints within the same AWS region and account.

Understanding the Relationship:
The relationship between RPS and Burst is crucial for optimizing API performance and preventing throttling issues. While Burst limits the number of concurrent requests that API Gateway can handle simultaneously, RPS governs the speed at which the request bucket is refilled after processing burst requests.

Optimizing Rate Limiting Configuration:
When configuring rate limiting settings for API Gateway, it's essential to ensure coherence between RPS and Burst limits. Setting Burst limits within the maximum concurrent request capacity ensures optimal resource utilization without risking throttling. Additionally, RPS limits should be adjusted based on the anticipated traffic patterns and workload characteristics to maintain a balanced request flow.

Best Practices:
To avoid misconfigurations and optimize API performance, adhere to the following best practices:
1. Ensure that Burst limits are set below the maximum concurrent start capacity to prevent overloading API Gateway.
2. Adjust RPS limits based on anticipated traffic patterns and workload characteristics to maintain a steady request flow.
3. Regularly monitor API Gateway metrics and adjust rate limiting settings as needed to accommodate changes in traffic volume and usage patterns.

Conclusion:
Understanding the intricacies of RPS and Burst is essential for effectively managing rate limiting in Amazon API Gateway. By aligning Burst and RPS limits with expected workload characteristics and traffic patterns, developers can optimize API performance, prevent throttling issues, and ensure a seamless experience for API consumers.

## Api Gateway integrations

### Lambda function integration

- **Standard Integration:** Provides granular control over request and response mapping for invoking Lambda functions.

![](images/intro/Screenshot%202024-03-20%20at%2010.44.46%20PM.png)
	- **Request and Response Mapping:** Allows developers to define transformation rules using Velocity Templating Language (VTL) to customize request and response payloads.
	- **Flexibility:** Ideal for complex API scenarios requiring detailed data formatting and additional processing before Lambda invocation.
	- **Compatibility:** Available exclusively for REST APIs in API Gateway, enabling fine-tuning of API logic and performance.
	
- ### **Proxy Integration:**

![](images/intro/Screenshot%202024-03-20%20at%2010.44.14%20PM.png)
- **Purpose:** Passes the entire request to the Lambda function without any transformation.
- **Request Handling:** API Gateway sends the raw request to the Lambda function's event parameter.
- **Response Handling:** Lambda function must directly handle response headers, status codes, and body.
- **Use Case:** Suitable for simple API scenarios where minimal processing is required and Lambda function handles all logic and response formatting.

### **AWS Service Integration:**

![](images/intro/Screenshot%202024-03-20%20at%2010.46.11%20PM.png)

- **Purpose:** Allows API Gateway to directly integrate with AWS services like DynamoDB, S3, or Step Functions.
- **Request Handling:** API Gateway forwards the request to the integrated AWS service.
- **Response Handling:** The AWS service processes the request and sends back a response.
- **Use Case:** Ideal for scenarios where direct interaction with AWS services is required, enabling seamless integration without intermediate processing logic.

### **HTTP Integration:**

![](images/intro/Screenshot%202024-03-20%20at%2010.46.46%20PM.png)

- **Purpose:** Enables API Gateway to integrate with HTTP endpoints outside of AWS, acting as a proxy.
- **Request Handling:** API Gateway forwards incoming requests to the specified HTTP endpoint.
- **Response Handling:** The external HTTP endpoint processes the request and returns a response to API Gateway.
- **Use Case:** Useful for scenarios where API Gateway needs to communicate with external HTTP services, such as third-party APIs or legacy systems, providing a secure and controlled interface.

### **Mock Integration:**

![](images/intro/Screenshot%202024-03-20%20at%2010.47.18%20PM.png)

- **Purpose:** Provides a simulated integration for API Gateway endpoints without actually connecting to a backend service.
- **Request Handling:** API Gateway generates mock responses based on predefined templates or rules without sending requests to a backend.
- **Response Handling:** Mock responses are generated and returned to the client based on predefined configurations.
- **Use Case:** Ideal for testing API Gateway configurations, handling pre-flight requests, or simulating responses from backend services during development and testing phases.

### **Private Integration**:

![](images/intro/Screenshot%202024-03-20%20at%2010.47.52%20PM.png)

- **Purpose:** Enables API Gateway to securely connect to backend services within a Virtual Private Cloud (VPC).
- **Connection:** Utilizes a VPC link and a network load balancer to establish a secure connection to backend resources.
- **Access Control:** Allows access to services hosted in private subnets or on-premises infrastructure via API Gateway.
- **Flexibility:** Supports connections to various backend resources, including ECS, EC2, and on-premises servers.
- **HTTP API:** Offers similar capabilities, including direct connections to application load balancers and integration with AWS Cloud Map for container instances.

## **Authorization Simplification:**

REST: 
![](images/intro/Screenshot%202024-03-21%20at%205.47.33%20AM.png)

HTTP: 
![](images/intro/Screenshot%202024-03-21%20at%205.56.10%20AM.png)


- **Authentication:** Refers to the process of verifying the identity of a user or entity accessing the system, typically achieved through various authentication mechanisms.
- **Authorization:** Involves determining the access rights and permissions of authenticated users or entities, specifying what actions they are allowed to perform within the system.

Simplify and optimize the authorization process within API Gateway to enhance security and efficiency. A prevalent tendency among developers to handle authorization redundantly across backend servers or integrations, leading to potential inefficiencies and security vulnerabilities.

- **Recommended Approach:**
	- Advocate for centralizing the authorization process at the API endpoint level to ensure it occurs only once per request, thereby reducing overhead and enhancing performance.

- **Authorization Types:**
  - **Open:**
    - Denotes a scenario where access is unrestricted, and no authorization checks are required. Typically used for publicly accessible resources.
  - **IAM Permissions:**
    - Employed primarily for service-to-service authorization within AWS environments, leveraging IAM roles and policies for access control.
  - **Signed Signature/Certificate:**
    - Offers options for client-based authorization, enabling authentication via signed signatures or certificates provided by the client.
  - **Amazon Cognito Authorizer:**
    - Presents a custom-built authorization mechanism distinct from traditional JWT-based solutions, providing flexibility and ease of integration with AWS services.
  - **Lambda Authorizers:**
    - Facilitate highly customizable authorization workflows by allowing developers to implement custom logic using Lambda functions, catering to specific application requirements and use cases.

- **Authorization in REST vs. HTTP:**
	- **REST:** Supports a range of authorization types, including those mentioned earlier, to accommodate diverse application needs and security requirements.
	- **HTTP:** Enhances authorization capabilities by introducing JWT-based authentication, enabling token-based access control and validation for HTTP APIs.

## Caching

![](images/intro/Screenshot%202024-03-21%20at%206.01.02%20AM.png)

- **Built-in Caching:**
	- Amazon API Gateway offers its own caching mechanism.
	- Optimizes response times within a specific region.
	- Particularly beneficial for scenarios requiring quick responses.

- **Managed Solution:**
	- API Gateway handles caching transparently.
	- No need for developers to configure or maintain caching infrastructure.
	- Simplifies development and deployment workflows.

- **Comparison with CloudFront:**
	- CloudFront provides a distributed network of cache objects across multiple edge locations.
	- Offers enhanced scalability and performance benefits.
	- Allows for greater flexibility and customization options.

- **Management Considerations:**
	- Decision depends on level of control and management overhead.
	- API Gateway offers hassle-free caching, while CloudFront provides more flexibility.
	- Developers should consider performance and budgetary requirements.

- **Cost Implications:**
	- Both API Gateway's built-in caching and CloudFront may incur costs.
	- Factors include cache cluster size and request volume.
	- Developers should carefully evaluate cost vs. performance trade-offs.

- **Edge Caching:**
	- CloudFront enables caching closer to end users at the edge.
	- Reduces latency and improves user experience.
	- Ideal for scenarios requiring faster response times.

## Throttling

![](images/intro/Screenshot%202024-03-21%20at%206.09.31%20AM.png)

- **Importance of Throttling:**
	- Throttling is crucial for managing API usage and preventing overloads.
	- Ensures fair distribution of resources and maintains system stability.

- **Soft and Hard Limits:**
	- Soft limit: 10,000 Requests Per Second (RPS) per API, customizable based on usage patterns.
	- Hard limit: 5,000 RPS shared among all endpoints within an API.
	- Customizable to accommodate specific workload requirements.

- **Granular Configuration:**
	- Throttling settings can be applied at various levels:
		- Stage level
		- Resource level
		- Method level
	  - Granularity enables fine-tuning based on endpoint priorities and usage patterns.

- **Example Configuration:**
	  - Allocate different RPS limits to different endpoints based on importance and usage.
	  - Prioritize critical endpoints with higher RPS allocations and burst capacities.
	  - Custom throttling configurations enhance resource utilization and performance.

- **Advanced Throttling Strategies:**
	- Utilize API usage plans and API keys for custom throttling.
	- Segment users into different groups (e.g., free vs. subscription) with distinct throttling settings.
	- Optimize resource allocation by throttling non-critical endpoints in favor of higher-priority ones.

- **Best Practices:**
	- Regularly review and adjust throttling settings based on evolving usage patterns.
	- Implement monitoring and alerting mechanisms to track throttling events and respond proactively.
	- Throttling optimization contributes to efficient resource utilization and improved API performance.

- **Conclusion:**
	- Throttling is a critical aspect of API management for maintaining system reliability and performance.
	- Customizable throttling configurations offer flexibility and control over resource allocation.
	- By implementing effective throttling strategies, organizations can ensure optimal API performance and user experience.

## Stages:

![](images/intro/Screenshot%202024-03-21%20at%206.12.56%20AM.png)

Different stages can point to different Lambda Aliases. It gets complex. Don't use stages unless you need to. 

Better practice: 
1. Use accounts per environment: Dev, Alpha, Beta, Gamma, Prod
2. Use custom domains with custom base path mapping

| ![](images/intro/Screenshot%202024-03-21%20at%206.16.08%20AM.png) | ![](images/intro/Screenshot%202024-03-21%20at%206.18.28%20AM.png) |
| -------------------------------------------- | -------------------------------------------- |
| ![](images/intro/Screenshot%202024-03-21%20at%206.20.41%20AM.png) |                                              |

## Logging

![](images/intro/Screenshot%202024-03-21%20at%206.24.20%20AM.png)

- **Importance of Logging:**
	- Logging is essential for gaining insights into API performance and behavior.
	- Provides valuable data for troubleshooting, monitoring, and optimizing API operations.

- **Common Pitfalls in Logging:**
	- Merely logging data without analyzing or utilizing it effectively.
	- Storing logs in S3 buckets without further action or analysis.
	- Neglecting to extract actionable insights from logged data.

- **Effective Logging Strategies:**
	- Utilize built-in logging features in API Gateway for capturing request/response data.
	- Define custom log formats to tailor logging output to specific requirements.
	- Ensure comprehensive logging coverage across all API endpoints and operations.

- **Utilizing Logged Data:**
	- Analyze logged data to identify performance bottlenecks, error patterns, and usage trends.
	- Implement proactive monitoring and alerting based on logged metrics to detect anomalies or issues.
	- Use logged insights to optimize API performance, troubleshoot issues, and enhance overall reliability.

- **Integration with Monitoring Tools:**
	- Leverage CloudWatch Metrics to track API performance metrics and key indicators.
	- Set up alarms and notifications to alert stakeholders of critical events or performance thresholds.
	- Integrate logged data with other monitoring and analytics tools for comprehensive visibility and analysis.

- **Continuous Improvement:**
	- Regularly review and refine logging configurations based on evolving requirements and usage patterns.
	- Encourage a culture of proactive monitoring and data-driven decision-making within the organization.
	- Continuously optimize logging practices to extract maximum value and insights from logged data.

## Canary releases

| ![](images/intro/Screenshot%202024-03-21%20at%206.27.28%20AM.png) | ![](images/intro/Screenshot%202024-03-21%20at%206.28.00%20AM.png) |
| -------------------------------------------- | -------------------------------------------- |
|                                              |                                              |
**Implementing Canary Releases in API Gateway**

- **Introduction to Canary Releases:**
	- Canary releases allow gradual deployment of changes by routing a portion of traffic to a new stage or version, known as the canary.
	- Offers a controlled way to test changes in a production-like environment before full deployment.

- **Key Concepts:**
	- Creation of a separate stage or version labeled as canary.
	- Gradual routing of a percentage of traffic (e.g., 5%, 10%) to the canary stage for testing.
	- Manual promotion process based on observed metrics and user feedback.

- **Use Cases and Benefits:**
	- Ideal for testing API Gateway configuration changes, such as route modifications, domain additions, or integration updates.
	- Provides the ability to validate changes in a real-world scenario while minimizing the risk of impacting all users simultaneously.
	- Enables teams to gather feedback, monitor performance metrics, and ensure the stability of new features or updates.

- **Considerations and Best Practices:**
	- Canary releases are more suited for API Gateway configuration changes rather than code modifications.
	- Manual promotion is required to transition from the canary stage to full production, ensuring careful evaluation and validation.
	- Monitor performance metrics, user feedback, and error rates during the canary phase to make informed decisions about promotion.

- **Implementation Workflow:**
	1. Create a separate stage or version labeled as canary in API Gateway.
	2. Define routing rules to direct a portion of incoming traffic to the canary stage.
	3. Monitor key performance metrics, error rates, and user feedback during the canary phase.
	4. Evaluate the success and stability of the changes in the canary stage.
	5. Manually promote the canary stage to full production based on observed metrics and feedback.
	6. Remove the canary stage once the changes are successfully deployed to production.

## Resource policies

**Understanding Resource Policies in API Gateway**

- **Introduction to Resource Policies:**
	- Resource policies in API Gateway enable fine-grained control over access to APIs and routes based on specific conditions.
	- They offer a flexible mechanism to restrict access to APIs, such as allowing access only from certain regions, accounts, or IP addresses.

- **Key Concepts:**
	- Resource policies allow conditional access control, specifying criteria such as API, region, time, or source IP.
	- They are particularly useful for securing private APIs or implementing temporary access restrictions, like time-bound promotions or limited-time offers.

- **Use Cases and Benefits:**
	- **Private APIs:** Resource policies can restrict access to APIs, ensuring they are only accessible by authorized entities, such as specific AWS accounts or IP addresses.
	- **Temporal Access Control:** Organizations can define time-based access restrictions, limiting API availability to specific time frames or promotional periods.
	- **Fine-grained Authorization:** Resource policies enable granular control over API access, offering flexibility to define access rules based on various conditions.

- **Examples of Resource Policy Conditions:**
	- Restricting access to a specific AWS account or IAM role.
	- Allowing access only from designated IP addresses or IP ranges.
	- Setting time-based constraints, specifying access periods like start and end dates or time windows.
	- Implementing geographic restrictions, limiting API access to specific regions or countries.

- **Implementation Guidelines:**
	- Define resource policies in API Gateway to enforce access controls at the API or route level.
	- Utilize conditions to tailor access restrictions according to specific requirements, such as time-sensitive promotions or geographic limitations.
	- Regularly review and update resource policies to align with evolving security needs and access control requirements.

![](images/intro/Screenshot%202024-03-21%20at%206.34.11%20AM.png)

## WAF Integration

![](images/intro/Screenshot%202024-03-21%20at%206.38.14%20AM.png)

- **Introduction to AWS WAF:**
	- AWS Web Application Firewall (WAF) provides an additional layer of security for API Gateway endpoints by filtering and monitoring incoming traffic.

- **Key Features and Functionality:**
	- Creation of customized firewalls with specific limitations, rules, and monitoring capabilities.
	- Integration with infrastructure as code (IaC) for automated deployment and management.
	- Offers robust protection against common web exploits and attacks, ensuring the integrity and availability of API services.

- **Deployment Process:**
	1. Access the WAF console within the AWS Management Console.
	2. Define firewall settings, including rules, conditions, and monitoring preferences.
	3. Configure the firewall according to the security requirements and risk profile of the API endpoints.
	4. Optionally, implement infrastructure as code (IaC) techniques to automate firewall deployment and management.
	5. Apply the configured firewall to the production stage of API Gateway.

- **Benefits and Use Cases:**
	- Provides granular control over incoming traffic, allowing organizations to enforce specific access conditions based on IP, time, or other parameters.
	- Ideal for securing sensitive APIs, such as financial or healthcare applications, against common web threats and attacks.
	- Seamless integration with API Gateway ensures that all incoming traffic passes through the WAF before reaching the endpoint, enhancing security without compromising performance.

- **Considerations and Best Practices:**
	- Prioritize the use of resource policies within API Gateway to restrict access based on specific conditions before resorting to WAF.
	- Regularly review and update firewall rules to adapt to evolving security threats and compliance requirements.
	- Leverage infrastructure as code (IaC) practices to automate the deployment and management of WAF configurations, ensuring consistency and scalability.

## Client certificates and mTLS

| ![](images/intro/Screenshot%202024-03-21%20at%206.42.15%20AM.png) | ![](images/intro/Screenshot%202024-03-21%20at%206.41.56%20AM.png) |
| -------------------------------------------- | -------------------------------------------- |
|                                              |                                              |

## Swagger/OpenAPI 3 import and export

![](images/intro/Screenshot%202024-03-21%20at%206.44.04%20AM.png)

- **Introduction to OpenAPI:**
	- OpenAPI, formerly known as Swagger, is a widely adopted standard for defining RESTful APIs.
	- It provides a structured format for describing APIs, including endpoints, operations, parameters, and responses.

- **Integration with API Gateway:**
	- OpenAPI serves as the primary tool for building API Gateway configurations.
	- Developers can define their API specifications using OpenAPI documents, specifying endpoints, methods, security requirements, and integrations.
	- Integration with AWS SAM (Serverless Application Model) allows pointing to external OpenAPI files for API Gateway configuration.

- **Workflow and Benefits:**
	- Developers can utilize the API Gateway console to visually design and configure their APIs.
	- After configuring the API in the console, developers can export the API definition in OpenAPI format.
	- This enables seamless conversion between Swagger and OpenAPI formats and facilitates migration from other providers.
	- The API Gateway console streamlines the API development process by leveraging OpenAPI specifications, eliminating the need to memorize complex OpenAPI syntax.

- **Key Features and Capabilities:**
	- Ability to import and export OpenAPI and Swagger documents within API Gateway.
	- Support for additional formats such as JSON and Postman extensions.
	- Integration of API Gateway extensions, including security, authentication, and integrations, in the exported OpenAPI documents.

- **Best Practices and Considerations:**
	- Encourage developers to leverage OpenAPI for consistency and standardization in API development.
	- Regularly export API definitions to ensure version control and documentation consistency.
	- Utilize the conversion capabilities to migrate APIs between different platforms or providers seamlessly.

- **Conclusion:**
	- OpenAPI serves as a powerful tool for designing, documenting, and managing APIs within API Gateway.
	- By integrating OpenAPI with the API Gateway console, developers can streamline the API development process and ensure compatibility with industry standards.
	- Leveraging OpenAPI enables agility, consistency, and ease of maintenance in building robust APIs on the AWS platform.

## Identity based policies

Reference: https://docs.aws.amazon.com/apigateway/latest/developerguide/security_iam_id-based-policy-examples.html

- **Understanding Identity-Based Policies:**
	- Identity-based policies in Amazon API Gateway regulate access to APIs based on the identity of the caller.
	- These policies define permissions and restrictions for users, roles, or groups accessing API resources.

- **Types of Identity-Based Policies:**
	- **IAM Policies:** Identity and Access Management (IAM) policies grant permissions to AWS users, roles, or groups.
		- *Example:* An IAM policy allows a specific IAM user to invoke API methods within an API Gateway resource.
    ```json
    {
      "Version": "2012-10-17",
      "Statement": [
        {
          "Effect": "Allow",
          "Action": "execute-api:Invoke",
          "Resource": "arn:aws:execute-api:region:account-id:api-id/stage/HTTP_METHOD/Resource_path"
        }
      ]
    }
    ```

	- **Resource Policies:** Resource policies are JSON documents attached to API Gateway resources, allowing or denying access based on specified conditions.
		- *Example:* A resource policy restricts access to an API endpoint to requests originating from a specific IP address range.
    ```json
    {
      "Version": "2012-10-17",
      "Statement": [
        {
          "Effect": "Allow",
          "Principal": "*",
          "Action": "execute-api:Invoke",
          "Resource": "arn:aws:execute-api:region:account-id:api-id/stage/HTTP_METHOD/Resource_path",
          "Condition": {
            "IpAddress": {
              "aws:SourceIp": ["192.0.2.0/24"]
            }
          }
        }
      ]
    }
    ```

- **Use Cases and Examples:**
  - **IAM Policies:**
    - *Granting Access to Specific IAM Users:* An IAM policy allows a designated IAM user to invoke all methods within an API resource.
    - *Restricting Access to Specific API Methods:* An IAM policy permits certain IAM roles to access only specific API methods, such as GET or POST.

  - **Resource Policies:**
    - *Enforcing IP-Based Restrictions:* A resource policy limits access to an API endpoint to requests originating from trusted IP addresses.
    - *Allowing Cross-Account Access:* A resource policy grants access to API resources from specific AWS accounts, ensuring controlled cross-account usage.

- **Configuration and Management:**
	- Identity-based policies are configured and managed within the AWS Management Console or through AWS CLI/API calls.
	- Policies are written in JSON format, defining principals, actions, resources, and conditions for access control.
	- Regular monitoring and updates to identity-based policies are essential to maintain security and compliance standards.

- **Best Practices:**
	- Follow the principle of least privilege when defining IAM policies, granting only necessary permissions to users, roles, or groups.
	- Implement resource policies to enforce fine-grained access control and security measures at the API Gateway level.
	- Regularly review and audit identity-based policies to ensure alignment with security requirements and organizational policies.

## References
- https://www.youtube.com/watch?v=SlWJCTrMLOA&list=PPSV



tags: 
#ApiGateway
#ApiGatewayIntroduction