# CLAUDE.md — IoT Semantic Compression Prototype

## Project
- Build a prototype for **Event Semantic Compression and Adaptive Sampling for IoT Data Streams**.
- No physical sensors are available yet; generate realistic synthetic sensor data in software.
- The goal is to reduce redundant events while preserving important changes and anomalies.

## Technology decisions
- **Use now:** Python, MQTT (Mosquitto), JSON event payloads, Git.
- **Use next:** PostgreSQL for baseline/filtered results and experiment metrics.
- **Integrate later:** Apache NiFi after the Python engine works independently.
- **Add later:** Prometheus/Grafana for monitoring; Docker/Kubernetes for deployment.
- **Do not add initially:** physical hardware, cloud hosting, Kafka, complex ML models, or Kubernetes.
- Prefer a small, modular, locally runnable system with minimal dependencies.

## Build order
1. Create a configurable Python sensor-data generator.
2. Simulate stable readings, gradual drift, rapid changes, bursts, and anomalies.
3. Give each event a timestamp, sensor ID, metric, value, and scenario label.
4. Publish generated JSON events to MQTT topics.
5. Implement a semantic engine using change magnitude, rate of change, frequency limits, and configurable thresholds.
6. Add adaptive sampling: reduce output during stable periods and increase it during rapid changes.
7. Save baseline and filtered events, then compare results.
8. Add a simple dashboard only after the core pipeline works.

## Evaluation
- Measure event reduction %, estimated bandwidth reduction, throughput, latency, CPU/memory, and anomaly preservation.
- Compare filtered output against a baseline that forwards every generated event.
- Never claim synthetic results represent real sensor performance; label them as simulated.

## Development rules
- Start with the data generator only; keep each milestone runnable and testable.
- Use clear modules, type hints, useful logs, configuration files, and reproducible random seeds.
- Include setup/run instructions and tests for thresholds, anomalies, and edge cases.
- Avoid unnecessary abstractions and dependencies; explain trade-offs briefly.
- Do not implement future stages until the current stage passes its tests.
