# PASS Architecture

PASS has a single page JavaScript user interface based on Ember. The UI interacts with HTTP APIs provided by a Java backend based on Spring and Elide.

The HTTP APIs are JSON:API for CRUD and search on the PASS data model, a custom file API to handle binaries, a custom DOI API, a custom metadata schema API, a custom user service API, and a custom policy service API. The pass-core component runs these APIs, handles authentication, submits events to queues, and mediates access to static HTTP resources.

Several services also run on the backend. Data loaders periodically update PASS with the latest information about institutional grants, journal metadata, and PubMed central publications.
A deposit service turns submissions to PASS into deposits to repositories like DSpace and PubMed Central. A notification service sends email to users about events. The deposit and notification services are triggered by events on queues.

The data model is persisted in a database managed by Elide.

# Model

# API

# Backend

## Grant loader

## Journal loader

## NIHMS loader

## Deposit service

## Notification service

# UI






