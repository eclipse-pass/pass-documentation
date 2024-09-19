# PASS Architecture

PASS has a single page JavaScript user interface based on Ember. The UI interacts with HTTP APIs provided by a Java backend based on Spring and Elide.

The HTTP APIs are JSON:API for CRUD and search on the PASS data model, a custom file API to handle binaries, a custom DOI API, a custom metadata schema API, a custom user service API, and a custom policy service API. The pass-core component runs these APIs, handles authentication, sends messages to queues, and mediates access to static HTTP resources.

Several additional services run on the backend. Data loaders periodically update PASS with the latest information about institutional grants, journal metadata, and PubMed central publications. A deposit service turns submissions to PASS into deposits to repositories like DSpace and PubMed Central. A notification service sends email to users about events. The deposit and notification services monitory message queues. The deposit service also polls PASS for objects it needs to update.

Elide provides a JSON:API based interface to the data model and persists the data model to a database. Both the UI and backend services interact with the data model using JSON:API.

# Data Model

The [data model](./model/) holds all the information needed to associate users with grants and manage deposits to repositories.

# Data Loaders

# API

## Authentication

## Grant Loader

## Journal Loader

## NIHMS Loader

## Deposit Service

## Notification Service

# UI






