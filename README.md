# Full training pipeline and dataset are private  due to research and dataset constraints.

## Project summary block
Text2Diagram is an LLM-driven backend that turns Vietnamese geometry problems into:
- structured diagram instructions (DSL),
- rendered geometry diagrams,
- step-by-step solutions.

Public scope focuses on architecture, orchestration, inference, APIs, and deployment readiness.

## Pipeline description
Request flow:
1. User sends problem text to orchestration API.
2. Rewriter agent extracts clean problem statement and intent.
3. Diagram branch generates DSL then renders image.
4. Optional solver branch generates detailed solution.
5. System returns result and stores request history.

Main implementation references:
- app bootstrapping: [src/main.py](src/main.py)
- API route registration: [src/api/endpoints.py](src/api/endpoints.py)
- orchestration API: [src/api/routes/orchestration.py](src/api/routes/orchestration.py)
- orchestration graph: [src/services/orchestration/orchestrator.py](src/services/orchestration/orchestrator.py)
- diagram pipeline: [src/services/diagram/generation.py](src/services/diagram/generation.py)

## Backend architecture summary
Core backend layers:
1. API layer: FastAPI routes for auth, diagram, orchestration, tasks, history.
2. Agent layer: rewriter agent, diagram agent, solver agent.
3. Orchestration layer: LangGraph state graph controls routing and execution order.
4. Execution layer: Celery worker renders diagrams asynchronously.
5. Data layer: PostgreSQL for persistence, Redis for cache/session support.
6. Infra layer: Docker Compose stack for API, worker, broker, DB, monitoring.

Infra reference:
- compose services and dependencies: [compose.yaml](compose.yaml)

## Tech stack section
- Backend: FastAPI, Pydantic, SQLAlchemy
- Orchestration: LangGraph, LangChain
- LLM integration: OpenAI-compatible clients, SageMaker endpoint
- Async jobs: Celery + RabbitMQ
- Storage and cache: PostgreSQL + Redis
- Packaging and deploy: Docker, Docker Compose

## ode structure section for README
Recommended tree snippet:

src/
- api/
- services/
	- orchestration/
	- diagram/
	- history/
- infrastructures/
- models/
- prompts/

pipeline/
- services/
- steps/
- pipelines/