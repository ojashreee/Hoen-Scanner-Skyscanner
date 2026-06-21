# Hoen-Scanner-Skyscanner TASK 1

> A tiny, focused microservice with one job: help travelers find hotels and rental cars on the Hoen Archipelago — fast.

The Hoen Archipelago just landed on Skyscanner's radar — strange fauna, stunning scenery, and a sudden wave of curious travelers. The catch? The hotels and rental car listings for the area existed, but they weren't searchable yet. Hoen Scanner closes that gap: a lightweight Java microservice that takes a city name and hands back every matching hotel and rental car in milliseconds.

---

## 🎯 About this submission

This repository is my completed submission for the **Skyscanner Software Engineering Virtual Experience Program (Forage)**.

### The brief

Skyscanner needed a way to surface the Hoen Archipelago's hotel and rental car data through a real, working backend service. The task: build a Java microservice with the **Dropwizard** framework that:

- Accepts a JSON-encoded `POST` request containing a `city`
- Searches through the provided hotel and rental car data for matches
- Returns the matching results as a JSON-encoded response

No fluff, no over-engineering — just a clean microservice that does one thing well, which is exactly the philosophy behind breaking large systems into small, independent services in the first place.

---

## 🧩 What I implemented

| File | What it does |
|---|---|
| `Search.java` | Represents an incoming search request — deserialised from the request body via Jackson's `@JsonProperty` |
| `SearchResult.java` | Represents a single hotel or rental car result, with `city`, `title`, and `kind` fields — serialised back to the client |
| `SearchResource.java` | Exposes a `POST /search` endpoint that filters the full result list down to matches for the requested city |
| `HoenScannerApplication.java` | Loads `rental_cars.json` and `hotels.json` at startup, merges them into a single result list, and registers `SearchResource` with the Dropwizard environment |

The flow is simple by design: data loads once at startup → a request comes in → the service filters → a clean JSON response goes back out.

```
        POST /search { "city": "petalborough" }
                      │
                      ▼
              ┌───────────────┐
              │ SearchResource│
              └───────┬───────┘
                      │ filters by city
                      ▼
        ┌─────────────────────────────┐
        │ rental_cars.json + hotels.json│
        │   (loaded once at startup)    │
        └─────────────────────────────┘
                      │
                      ▼
            JSON list of matches
```

---

## 🧰 Tech stack

- **Java**
- **Dropwizard** — lightweight framework for building production-ready RESTful microservices
- **Jackson** — JSON serialization/deserialization via `@JsonProperty`
- **Maven** — build and dependency management

---

## 🚀 Running it

1. Open the project in **IntelliJ** and let Maven finish loading.
2. Run `HoenScannerApplication` (the green arrow). You should see a `Welcome to Hoen Scanner!` banner in the logs — that's your sign everything booted correctly.
3. Using **Postman** (or any HTTP client), send a `POST` request to:

   ```
   localhost:8080/search
   ```

   with a JSON body like:

   ```json
   { "city": "petalborough" }
   ```

4. The response comes back with every matching hotel and rental car for that city — try `rustburg` and `shaleport` too, or an invalid city to see how the service handles a miss.

---

## 🛠️ Why microservices?

This task is also a small case study in why teams break big systems into microservices instead of one giant monolith: Hoen Scanner does exactly one job, can be deployed and scaled independently, and could be swapped out, rewritten, or extended without anyone touching the rest of Skyscanner's platform. Small, focused, decoupled — that's the whole idea.

---

## 📄 License

This project was built as part of Skyscanner's Forage Virtual Experience Program, for educational and portfolio purposes.

---

<p align="center">
Built with Java, Dropwizard, and a healthy curiosity about strange island fauna. 🦎
</p>
