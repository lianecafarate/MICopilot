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

## 📋 Database Script
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

