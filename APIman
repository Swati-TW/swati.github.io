# APIMAN #

Apiman consists of two primary components: 
+ API Manager 
The API Manager is a set of REST endpoints and a **User Interface**, and is used to manage and configure all of the APIs being provided and the clients consuming them.
+ API Gateway
The API Gateway applies the configured governance policies at runtime to every API request from every registered client.
## API Manager Concepts
The API Manager is used to configure APIs and connect them to consumers. It is where providers go to configure the APIs they would like to manage, and it’s also where API consumers go to find APIs to consume.
### Organization
An **Organization** is simply an entity within which everything else is contained. A user must be a member of an Organization in order to manage any of the entities contained within it. Membership in an Organization is role based, so different users may be granted different capabilities within it.
### Service
When an API provider wishes to manage one of their APIs, they do so by creating a **Service within** the Organization. The Service is given a name and description, along with details about the API’s implementation endpoint. The Service can also be given a set of Policies, which will be applied by the API Gateway whenever the Service is invoked. More about Policies a little bit later.
### Plan
Before a Service can be consumed, it must be available to consumers through a Service Plan. A Plan is simply a collection of Policies that are applied whenever a Service is invoked through that particular Plan.
Because a Service can be consumed through multiple Plans, the Plan provides a convenient place to configure different levels of access. A typical example would be having multiple Plans, each with a different Rate Limit Policy configured.
### Application
When consuming APIs an Application _must_ be created in the API Manager. _An Application is typically a representation of an API client of some kind, perhaps a mobile app or an integration application_. The Application is given a name and a description. Applications can also have configured Policies, which are applied whenever the Application invokes any Service.
### Contract
Once an Application is created, APIs can be consumed by creating **Contracts** between the Application and the Services it wishes to invoke. A Contract is simply a link between an Application and a Service through one of the Service’s available Plans.
### Policy
All of these concepts are ultimately in support of determining which **Policies** will get applied when a particular **Request** is received by the API Gateway. The Policy is the unit of governance executed at runtime, and is therefore the most important core concept. Common examples of Policies include Authentication, Rate Limiting, and IP filtering.
Policies can be configured in three places, the Plan, Service, and Application. These Policies are then applied to API requests by the API Gateway at runtime.
## API Gateway Concepts
Once the API Manager has been used to fully configure a Service or Application, the resulting configuration is published to the API Gateway. This published configuration is used by the API Gateway to apply the Policies to all API Requests.
### Policy Chain
The Policies configured on the Plan, Service, and Application are aggregated into a Policy Chain which is what gets applied to an API request by the API Gateway.
When an API request is received by the Gateway, the following steps are taken:
1.	First, the Policy Chain is applied to the API request. The Application Policies are applied first, followed by the Plan Policies and then the Service Policies.
2.	If any of the Policies reject the API request, an error response is sent to the client. If all of the Policies pass, the Gateway will forward the request to the API back-end implementation.
3.	Once the back-end responds, the Policy Chain is then applied again, in reverse order, to that response.
4.	If the Policies all pass, the response is sent back to the original client.
