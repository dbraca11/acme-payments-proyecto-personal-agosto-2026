# 🚀 Acme Payments - GitOps & Cloud-Native Ecosystem

Prototipo de microservicio de pagos de alta disponibilidad con entrega continua, observabilidad y autorrecuperación en Kubernetes.

## 🗺️ Roadmap del Proyecto

- [x] **Fase 1: Containerización y Microservicio Base**
  - [x] API REST ligera desarrollada con FastAPI y Python.
  - [x] Construcción de imagen en Docker e importación al almacenamiento de `containerd`.
- [x] **Fase 2: Estrategia GitOps con Argo CD**
  - [x] Definición de manifiestos K8s declarativos (`Deployment`, `Service`).
  - [x] Despliegue de Argo CD con sincronización automática (*Self-Healing* y *Prune*).
- [x] **Fase 3: Observabilidad y Monitoreo**
  - [x] Configuración de Grafana mediante Helm para la visualización de métricas del clúster.
  - [x] Aislamiento de componentes en el namespace dedicado `monitoring`.
- [x] **Fase 4: Ingeniería de Resiliencia e Incidentes**
  - [x] Inyección controlada de errores de despliegue (`ImagePullBackOff`).
  - [x] Validación de disponibilidad continua mediante la estrategia de *RollingUpdate*.
  - [x] Sincronización e imposición de estado deseado vía Argo CD Sync.

```mermaid
graph TD
    subgraph DEV[1. Desarrollo & Contenedores]
        A[🐍 API FastAPI]
        B[🐳 Dockerfile]
        C[📦 Imagen acme-payments:local]
        D[⚙️ Importación a containerd]
        E[📄 Manifiestos K8s]
        F[🐙 Repositorio GitHub]
    end

    subgraph K8S[2. Clúster de Kubernetes]
        subgraph ARGOCD[Namespace: argocd]
            G[🐙 Argo CD Application]
        end
        subgraph DEFAULT[Namespace: default]
            H[🔌 Service ClusterIP:8000]
            I[☸️ Deployment acme-payments]
            J[🚀 Pod 1 - FastAPI]
            K[🚀 Pod 2 - FastAPI]
        end
        subgraph MONITORING[Namespace: monitoring]
            L[📊 Grafana NodePort]
        end
    end

    subgraph OPS[3. Operación & Resiliencia]
        M[⚠️ Inyección de Fallo v-error]
        N[✅ Rolling Update - Pods activos]
        O[🔄 Argo CD Self Healing]
    end

    A --> B --> C --> D --> I
    A --> E --> F --> G --> I
    H --> I
    I --> J
    I --> K
    L -.->|Monitoreo| I
    M -->|Dispara incidente| I
    I -->|Mantiene disponibilidad| N
    G -->|Sincroniza y repara| O
    O -->|Restaura imagen sana| I

    %% Definición de Estilos e Identidad de Marca
    classDef python fill:#3776AB,stroke:#1e3d59,color:#fff,font-weight:bold;
    classDef docker fill:#0db7ed,stroke:#0984af,color:#fff,font-weight:bold;
    classDef k8s fill:#326ce5,stroke:#1b4bb0,color:#fff,font-weight:bold;
    classDef argo fill:#ef7b4d,stroke:#c45528,color:#fff,font-weight:bold;
    classDef grafana fill:#f46800,stroke:#ba4f00,color:#fff,font-weight:bold;
    classDef github fill:#24292e,stroke:#000,color:#fff,font-weight:bold;
    classDef alert fill:#e74c3c,stroke:#c0392b,color:#fff,font-weight:bold;
    classDef success fill:#2ecc71,stroke:#27ae60,color:#fff,font-weight:bold;

    class A,J,K python;
    class B,C,D docker;
    class E,H,I k8s;
    class G,O argo;
    class L grafana;
    class F github;
    class M alert;
    class N success;
```
