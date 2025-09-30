# ⚡️ Kafka Finance Data POC: Real-Time Transaction Stream

A Proof of Concept (POC) demonstrating **real-time ingestion and processing of simulated financial transaction data** using Apache Kafka.

---

## 💡 Project Context

This POC addresses the challenge of **high-volume, low-latency data movement** inherent in modern finance applications (e.g., fraud detection, real-time risk calculation). The goal is to evaluate Kafka's suitability as the core message backbone for a future system replacing legacy batch processing with a continuous, stream-based architecture.

---

## 🎯 Objectives

The primary goals for this POC are:

* **Establish a working Kafka cluster** (using Docker) with defined topics.
* Develop a **Producer** to simulate a high-throughput stream of finance transactions (e.g., credit card purchases).
* Develop a **Consumer** to ingest the data and perform a simple, real-time aggregate (e.g., total spend per user).
* Measure and document the **end-to-end latency** for message delivery and processing.
* Validate the **data persistence** and fault tolerance capabilities of the cluster.

---

## 🛠️ Steps & Installation

Steps to set up and run the Kafka POC environment.

### **Prerequisites**

* **Docker** and **Docker Compose**
* **Python 3.9+**
* A Python environment manager (e.g., `venv`)

### **Setup & Run**

1.  **Clone the repository:**
    ```bash
    git clone [https://github.com/YourUsername/kafka-finance-poc.git](https://github.com/YourUsername/kafka-finance-poc.git)
    cd kafka-finance-poc
    ```
2.  **Start the Kafka Cluster (Broker, Zookeeper):**
    The `docker-compose.yml` file defines the cluster.
    ```bash
    docker-compose up -d
    ```
3.  **Install Python dependencies:**
    ```bash
    pip install -r requirements.txt
    ```
4.  **Run the Real-Time Consumer:**
    Start the consumer first, waiting for data.
    ```bash
    python consumer/transaction_processor.py
    ```
5.  **Run the Data Producer:**
    Start generating the simulated financial transaction stream.
    ```bash
    python producer/data_generator.py
    ```
*(The consumer console should immediately begin displaying processed transaction records and aggregates.)*

---

## 📚 Resources & Documentation

Links to useful tools, documentation, and data schemas.

* **Source data:** https://github.com/ranaroussi/yfinance
* **Kafka Topics:** `finance.transactions` (raw data), `finance.aggregates` (processed data)
* **Simulated Data Schema:** [Link to `schema.json` or Pydantic model definition]
* **Docker Compose Configuration:** [docker-compose.yml](docker-compose.yml)
* **Apache Kafka Documentation:** [Link to Kafka Official Docs]
* **Project Wiki:** [Link to your GitHub Wiki or external documentation]
* **API Documentation (Swagger/Postman):** [Link to API docs]
* **Design Document:** [Link to the architectural or system design doc]
* **Contributing Guide:** [CONTRIBUTING.md](CONTRIBUTING.md)
