# ACME Payments - CI/CD & Infrastructure Pipeline

Production-style DevOps CI/CD laboratory for ACME Payments service.

## Architecture Features
- **API Engine:** FastAPI Python Application with `/health` and `/payments` endpoints.
- **Testing Suite:** Automated unit test coverage with `pytest`.
- **Security & Quality:** Containerized with Docker and scanned for vulnerabilities via Trivy.
- **CI/CD Pipeline:** Fully automated GitHub Actions workflow publishing images to GHCR.
- **Kubernetes & Helm:** Production-grade Helm chart featuring Liveness/Readiness health probes.
