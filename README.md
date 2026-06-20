# Hoen-Scanner-Skyscanner TASK 1
This repo contains everything you need to get started on the Skyscanner backend engineering task
About this submission

This repository is my completed submission for the Skyscanner Software Engineering Virtual Experience Program (Forage).

The task

Skyscanner is incorporating the Hoen Archipelago into the platform. Another team compiled lists of hotels and rental car services in the area (rental_cars.json and hotels.json), but they weren't yet searchable. The task was to build a Java microservice, using the Dropwizard framework, that:


Accepts a JSON-encoded POST request containing a city
Searches through the provided hotel and rental car data for matches
Returns the matching results as a JSON-encoded response


What I implemented


Search.java — represents an incoming search request (deserialised from the request body via Jackson's @JsonProperty)
SearchResult.java — represents a single hotel or rental car result, with city, title, and kind fields (serialised back to the client)
SearchResource.java — exposes a POST /search endpoint that filters the full result list down to matches for the requested city
HoenScannerApplication.java — loads rental_cars.json and hotels.json at startup, merges them into a single result list, and registers SearchResource with the Dropwizard environment


Running it


Open the project in IntelliJ and let Maven finish loading.
Run HoenScannerApplication (green arrow). You should see a Welcome to Hoen Scanner! banner in the logs.
Using Postman (or any HTTP client), send a POST request to localhost:8080/search with a JSON body, e.g.:


json   { "city": "petalborough" }


The response will contain the matching hotels and rental cars for that city.
