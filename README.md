## Event-Driven Distributed System
## Overview

This project is a distributed system based on event-driven architecture that simulates an end-to-end invoice processing workflow using microservices.

The system handles:

Invoice generation

PDF creation

File storage

Notification delivery (Email & Discord)

Event tracking and analytics

All communication between services is handled asynchronously using Apache Kafka, while background processing and continuous event handling are managed with Hangfire.

## Architecture

The system follows a microservices architecture with a central orchestrator:

Main components:

Orchestrator Service (.NET + Hangfire)
Acts as the central coordinator of the system.
Uses Hangfire to manage background jobs and continuously listen for events, enabling asynchronous and reliable workflow execution.

PDF Service (.NET)
Generates invoice PDFs by retrieving data from SQL Server through an ORM.

Storage Service (.NET)
Stores generated PDF files and distributes them to notification services.

Notification Services:

Python Service → Sends emails with attachments

Node.js Service → Sends messages and files to Discord

Event Streaming:

Apache Kafka is used to track the entire workflow:

Correlation ID

Timestamps

Target services

Execution states

Analytics:

Data collected from Kafka is visualized using Power BI dashboards

##  Workflow

The Orchestrator (with Hangfire) continuously listens for incoming events.

Background jobs are triggered to handle invoice generation asynchronously.

The Orchestrator calls the PDF Service, which:

Fetches data from SQL Server

Generates a PDF invoice

The PDF Service:

Notifies the Orchestrator upon completion

Sends the file to the Storage Service

The Storage Service:

Saves the file

Sends it to notification services

Notification services:

Python → Sends email with attachment

Node.js → Sends Discord message with file

All events are published to Kafka

Data is processed and visualized in Power BI

 ## Technologies Used

Backend: .NET (C#)

Microservices: ASP.NET Web API

Event Streaming: Apache Kafka

Background Processing: Hangfire (.NET)

Database: SQL Server + ORM

Notification Services:

Python (Email Service)

Node.js (Discord Bot)

Data Visualization: Power BI

## Features

Event-driven communication

Distributed microservices architecture

Centralized orchestration

Asynchronous processing using Kafka

Background job processing with Hangfire

Real-time monitoring and analytics

Multi-channel notifications (Email & Discord)
