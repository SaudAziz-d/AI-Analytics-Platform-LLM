# BizInsight — AI-Powered Business Analytics Platform

An end-to-end analytics platform that automatically ingests data from multiple sources, cleans and transforms it into meaningful KPIs, applies machine learning for predictions and trend analysis, validates outputs through a business logic layer, and delivers clear natural language insights via an LLM engine — all surfaced through an interactive decision-maker dashboard.

---

## Table of Contents

- [Screenshots](#screenshots)
- [Overview](#overview)
- [Architecture](#architecture)
- [Features](#features)
- [Tech Stack](#tech-stack)
- [Project Structure](#project-structure)
- [Getting Started](#getting-started)
- [Configuration](#configuration)
- [API Reference](#api-reference)
- [Contributing](#contributing)
- [License](#license)

---

## Screenshots

### Screen 1 — Overview Dashboard

<img width="900" height="989" alt="screen1_dashboard" src="https://github.com/user-attachments/assets/5c907cde-1bd5-470c-a9f6-8410f374d818" />

<img width="900" height="674" alt="screen2_kpi" src="https://github.com/user-attachments/assets/9cd910b3-6e7b-4a85-855c-8ed400bff58d" />

<img width="900" height="550" alt="screen3_insights" src="https://github.com/user-attachments/assets/1410ce14-5dba-4efa-8eea-7b3a511b7c11" />


The LLM-powered insights hub. Summarizes active forecasts, risk alerts, opportunities, and ops flags at a glance. Each insight card shows a natural language explanation, confidence score, category badge, and a drill-down action link.

---

## Overview

BizInsight solves a core problem for data-driven organizations: raw business data is scattered across databases, APIs, flat files, and event streams — and turning that into actionable decisions requires significant manual effort. This platform automates the entire journey from raw data to executive-ready insights.

The system runs fully automatically after initial setup. Data is pulled on a configurable schedule, cleaned and normalized without manual intervention, passed through ML models for forecasting and anomaly detection, validated against business rules, and finally converted into plain-language recommendations by an LLM engine.

---

## Architecture

The platform is organized into five sequential layers:

```
┌─────────────────────────────────────────────┐
│           Data Ingestion Layer              │
│  Databases · REST APIs · CSV · Streams      │
└────────────────────┬────────────────────────┘
                     │ Raw data
┌────────────────────▼────────────────────────┐
│         ETL & KPI Engineering               │
│  Cleaning · Normalization · Feature Eng.    │
└────────────────────┬────────────────────────┘
                     │ Structured KPIs
┌────────────────────▼────────────────────────┐
│      ML Prediction & Trend Analysis         │
│  Forecasting · Anomaly Detection · Cluster  │
└────────────────────┬────────────────────────┘
                     │ Model outputs
┌────────────────────▼────────────────────────┐
│       Business Logic & Validation           │
│  Rules Engine · Thresholds · Alerts         │
└────────────────────┬────────────────────────┘
                     │ Validated outputs
┌────────────────────▼────────────────────────┐
│    LLM Insight & Recommendation Engine      │
│  NL Summaries · Recommendations · Briefs    │
└────────────────────┬────────────────────────┘
                     │ Insights & visuals
┌────────────────────▼────────────────────────┐
│      Interactive Decision-Maker Dashboard   │
│  Charts · KPI Cards · Alerts · Drill-down   │
└─────────────────────────────────────────────┘
```

---

## Features

### Data Ingestion
- Automated connectors for PostgreSQL, MySQL, REST APIs, S3 flat files, and Kafka event streams
- Configurable sync schedules (real-time, hourly, daily)
- Source health monitoring with SLA alerting

### ETL & KPI Engineering
- Automatic deduplication and missing value imputation
- Schema normalization across heterogeneous sources
- Computed KPIs: MRR, CLV, churn rate, gross margin, conversion rate, and more
- Feature engineering pipeline for ML-ready datasets

### ML Layer
- Time-series forecasting (revenue, demand, churn probability)
- Anomaly detection on KPI streams
- Customer segmentation via clustering
- Trend classification (accelerating, stable, declining)
- Model versioning and performance tracking

### Business Logic & Validation
- Configurable threshold rules per KPI and segment
- Condition validation before insight generation
- Automated alert triggers (email, Slack, webhook)
- Compliance checks and data quality scoring

### LLM Insight Engine
- Converts analytical outputs into plain-language narratives
- Generates prioritized recommendations per segment
- Produces risk summaries and opportunity briefs
- Executive-level reports with supporting data
- Confidence scoring on each insight

### Dashboard
- Real-time KPI cards with trend indicators
- Revenue and segment breakdown charts
- Data source status monitoring
- AI insights feed with drill-down capability
- Export to PDF and scheduled report delivery

---

## Tech Stack

### Backend
| Tool | Purpose |
|------|---------|
| Python 3.11 | Core backend language |
| FastAPI | REST API framework |
| Apache Airflow | Pipeline orchestration and scheduling |
| Apache Kafka | Real-time event stream ingestion |
| Apache Spark | Large-scale data transformation |
| dbt (data build tool) | KPI computation and data modeling |
| SQLAlchemy | ORM and database abstraction |
| Pydantic | Data validation and schema enforcement |

### Data Storage
| Tool | Purpose |
|------|---------|
| PostgreSQL | Primary operational database |
| ClickHouse | Analytical data warehouse (OLAP) |
| Redis | Caching and session management |
| Amazon S3 | Raw file storage and data lake |
| Elasticsearch | Log storage and search |

### Machine Learning
| Tool | Purpose |
|------|---------|
| scikit-learn | Classical ML models (clustering, classification) |
| Prophet | Time-series forecasting |
| PyOD | Anomaly detection |
| MLflow | Model tracking, versioning, and registry |
| Pandas / NumPy | Data manipulation and computation |
| Feast | Reusable feature management |

### LLM & AI
| Tool | Purpose |
|------|---------|
| Anthropic Claude API | Insight generation and NL summaries |
| LangChain | LLM orchestration and prompt management |
| Prompt templates | Structured insight formatting |

### Frontend
| Tool | Purpose |
|------|---------|
| React 18 | UI framework |
| TypeScript | Type-safe frontend development |
| Recharts | Charts and data visualizations |
| TailwindCSS | Styling |
| React Query | Server state and data fetching |
| Zustand | Client state management |

### Infrastructure & DevOps
| Tool | Purpose |
|------|---------|
| Docker & Docker Compose | Containerization |
| Kubernetes | Container orchestration (production) |
| GitHub Actions | CI/CD pipeline |
| Prometheus | Metrics collection |
| Grafana | Infrastructure monitoring |
| Nginx | Reverse proxy |

---

## Project Structure

```
bizinsight/
├── backend/
│   ├── api/                  # FastAPI routes and controllers
│   ├── ingestion/            # Data source connectors
│   │   ├── connectors/       # PostgreSQL, REST, S3, Kafka adapters
│   │   └── scheduler.py      # Airflow DAG definitions
│   ├── etl/                  # Cleaning and transformation
│   │   ├── cleaning.py       # Deduplication, imputation
│   │   ├── normalization.py  # Schema alignment
│   │   └── kpi_engine.py     # KPI computation logic
│   ├── ml/                   # Machine learning layer
│   │   ├── forecasting.py    # Prophet-based forecasting
│   │   ├── anomaly.py        # Anomaly detection (PyOD)
│   │   ├── clustering.py     # Customer segmentation
│   │   └── model_registry.py # MLflow integration
│   ├── validation/           # Business logic layer
│   │   ├── rules_engine.py   # Threshold and condition rules
│   │   ├── alerts.py         # Alert triggers and routing
│   │   └── compliance.py     # Data quality checks
│   ├── insights/             # LLM insight engine
│   │   ├── engine.py         # Claude API integration
│   │   ├── prompts/          # Prompt templates per insight type
│   │   └── formatter.py      # Output structuring
│   └── core/
│       ├── config.py         # Environment configuration
│       ├── database.py       # DB connections
│       └── models.py         # Pydantic schemas
├── frontend/
│   ├── src/
│   │   ├── pages/            # Dashboard, KPI, Insights, Predictions
│   │   ├── components/       # Reusable UI components
│   │   ├── hooks/            # Custom React hooks
│   │   └── store/            # Zustand state slices
│   └── public/
├── infrastructure/
│   ├── docker-compose.yml
│   ├── kubernetes/           # K8s manifests
│   └── nginx/
├── dbt/
│   ├── models/               # KPI SQL models
│   └── tests/
├── airflow/
│   └── dags/                 # Pipeline DAGs
├── tests/
│   ├── unit/
│   └── integration/
├── .env.example
├── docker-compose.yml
└── README.md
```

---

## Getting Started

### Prerequisites

- Docker and Docker Compose installed
- Python 3.11+
- Node.js 18+
- Anthropic API key

### Installation

1. Clone the repository:
```bash
git clone https://github.com/your-org/bizinsight.git
cd bizinsight
```

2. Copy environment variables:
```bash
cp .env.example .env
```

3. Fill in your credentials in `.env` (see [Configuration](#configuration)).

4. Start all services:
```bash
docker-compose up -d
```

5. Run database migrations:
```bash
docker exec bizinsight-backend python -m alembic upgrade head
```

6. Access the dashboard at `http://localhost:3000`  
   API docs available at `http://localhost:8000/docs`

---

## Configuration

Key environment variables in `.env`:

```env
# Database
DATABASE_URL=postgresql://user:password@localhost:5432/bizinsight
CLICKHOUSE_URL=clickhouse://localhost:9000/analytics

# Cache
REDIS_URL=redis://localhost:6379

# Storage
AWS_ACCESS_KEY_ID=your_key
AWS_SECRET_ACCESS_KEY=your_secret
S3_BUCKET_NAME=bizinsight-data

# LLM
ANTHROPIC_API_KEY=your_anthropic_key
CLAUDE_MODEL=claude-sonnet-4-6

# ML
MLFLOW_TRACKING_URI=http://localhost:5000

# Alerts
SLACK_WEBHOOK_URL=your_slack_webhook
ALERT_EMAIL=alerts@yourcompany.com

# Pipeline
AIRFLOW_SYNC_INTERVAL=@hourly
DATA_RETENTION_DAYS=365
```

---

## API Reference

### Data Sources
| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/sources` | List all data sources |
| POST | `/api/sources` | Register a new source |
| GET | `/api/sources/{id}/status` | Get sync status |
| POST | `/api/sources/{id}/trigger` | Trigger manual sync |

### KPIs
| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/kpis` | Get all KPI values |
| GET | `/api/kpis/{name}/history` | Get KPI time series |
| GET | `/api/kpis/segments` | Get segment breakdown |

### Insights
| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/insights` | Get latest AI insights |
| POST | `/api/insights/generate` | Trigger insight generation |
| GET | `/api/insights/{id}` | Get specific insight detail |

### Predictions
| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/predictions/forecast` | Get revenue forecast |
| GET | `/api/predictions/churn` | Get churn risk scores |
| GET | `/api/predictions/anomalies` | Get detected anomalies |

---

## Contributing

1. Fork the repository
2. Create a feature branch: `git checkout -b feature/your-feature`
3. Commit your changes: `git commit -m "feat: add your feature"`
4. Push to the branch: `git push origin feature/your-feature`
5. Open a Pull Request

Please follow the existing code style and include tests for new functionality.

---

## License

MIT License — see [LICENSE](LICENSE) for details.
