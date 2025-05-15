# MICopilot Project
MICopilot is an integration project developed with WSO2 Micro Integrator, leveraging the Micro Integrator Copilot VS Code extension to streamline the development of integration solutions. 
This project demonstrates how to use AI-assisted development tools within the WSO2 integration ecosystem.

## 🔍 Project Overview
This repository contains sample WSO2 Micro Integrator projects and artifacts. It can be used as a reference for understanding how to implement specific integration scenarios, particularly focusing on:

* API definition and request/response processing.
* Sequence and mediation logic.
* Error handling and fault sequence implementation.
* Logging strategies for debugging and monitoring.

## ✨ Building the Integration Flow
1. **Establish an Order-Receiving API**: Create a RESTful API endpoint (named 'OrderAPI' with a context path like /orders) to serve as the primary entry point for receiving incoming customer order requests.
2. **Define the Order Submission Contract**: Design the API to accept POST requests. Specify a clear JSON payload structure that captures all necessary order details (e.g., orderId, customerId, itemType, item-specific attributes, price).
3. **Implement Conditional Order Processing Logic**: Introduce routing logic within the API flow that inspects the *itemType* from the incoming order. This allows for differentiated handling, such as directing 'book' orders to a specific processing path while potentially routing other types elsewhere.
4. **Persist 'Book' Order Data to Database**: For orders identified as 'book' type, integrate the API with a MySQL database. This involves extracting relevant book details from the payload (like *orderId*, *title*, *author*, *price*) and inserting this information into a pre-defined 'books' table. This step presumes the database and table schema are already set up and accessible.
5. **Formulate and Return Client Response**: After the order processing (whether it's a database insertion for a book or another action for different item types), construct and send a meaningful HTTP response back to the original caller, indicating the success or failure of the order submission.

## 🚀 Mediators
* [Log Mediator](https://mi.docs.wso2.com/en/latest/reference/mediators/log-mediator/)
* [Variable Mediator](https://mi.docs.wso2.com/en/latest/reference/mediators/variable-mediator/)
* [If Else Mediator](https://mi.docs.wso2.com/en/latest/reference/mediators/filter-mediator/)
* [DB Report Mediator](https://mi.docs.wso2.com/en/latest/reference/mediators/db-report-mediator/)
* [PayloadFactory Mediator](https://mi.docs.wso2.com/en/latest/reference/mediators/payloadfactory-mediator/)
* [Respond Mediator](https://mi.docs.wso2.com/en/latest/reference/mediators/respond-mediator/)

## 🔧 Technology Stack
* [WSO2 Micro Integrator 4.4](https://mi.docs.wso2.com/en/latest/install-and-setup/install/installing-mi/)
* [VS Code Version 1.100.1](https://code.visualstudio.com/)
* [WSO2 Micro Integrator VS Code Extension Version 2.2.0](https://mi.docs.wso2.com/en/latest/develop/mi-for-vscode/install-wso2-mi-for-vscode/)
* macOS Sequoia 15.4.1
* [MySQL Community Edition Version 8.4.4-arm64](https://dev.mysql.com/downloads/mysql/)
* [DBeaver Community Edition Version 25.0.4](https://dbeaver.io/download/)
* [Mysql Connector 8.4.0](https://downloads.mysql.com/archives/c-j/)

## 🧪AI Prompts Suggestions
### Disclaimer: AI-Assisted Development (MI Copilot)
When using AI-powered coding assistants, please be aware of the following:
* **AI as a Tool:** Consider AI assistants as helpful "pair programmers" who can offer suggestions and accelerate development. However, they are not infallible and should not replace your critical judgment.
* **Potential for Errors:** AI-generated code or advice may contain inaccuracies, inefficiencies, or be incomplete. Always thoroughly review, test, and understand any suggestions before implementation.
* **Output Variability:** AI models can produce different results for similar prompts across different sessions or as the underlying models evolve. Do not expect identical outputs consistently.
* **User Responsibility:** You are ultimately responsible for the quality, security, and correctness of any code or solutions implemented, regardless of AI assistance.
* **Iterative Approach:** Treat AI suggestions as a starting point. Be prepared to iterate, refine, and adapt the output to meet your specific project requirements and best practices.

### 1) API Creation
"Create a REST API named 'OrderAPI' with the context path '/orders'. This API should accept POST requests to the resource path '/'. The request payload will be in JSON format with the following structure:
```json
{
  "orderId": "ORD-123",
  "customerId": "CUST-456",
  "itemType": "book",
  "title": "The Hitchhiker's Guide to the Galaxy",
  "author": "Douglas Adams",
  "price": 10.99
}
```
The API should handle this payload to receive order information. I need the basic structure of the API to be generated, including the resource definition and payload handling. I will add the specific order processing logic later. Please generate the Synapse configuration for this API."

### 2) Routing Sequence + DB Insertion
“I'd like to route orders based on 'itemtype'. If the itemType is 'book’, we will process it further by extracting relevant details and storing them in a MySQL database.”
Please also consider my database structure for reference."

```sql
-- Create a database to store order information
CREATE DATABASE IF NOT EXISTS ordersdb;

-- Use the newly created database
USE ordersdb;

-- Create a table to store book orders
CREATE TABLE IF NOT EXISTS books (
    orderId VARCHAR(255) NOT NULL,
    customerId VARCHAR(255) NOT NULL,
    title VARCHAR(255) NOT NULL,
    author VARCHAR(255) NOT NULL,
    price DECIMAL(10, 2) NOT NULL,
    PRIMARY KEY (orderId)
);
```
### 3) Log Mediator
“Could you add a log message after the book is inserted into the database, confirming that it was successfully added?”

## ❓Support
For questions, issues, or feature requests, please use the GitHub issues system or refer to the [WSO2 documentation](https://mi.docs.wso2.com/en/latest/) for additional guidance.
