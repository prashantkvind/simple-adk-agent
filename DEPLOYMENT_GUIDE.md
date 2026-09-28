# Local Setup, Testing & GCP Deployment Guide: Simple ADK Agent

This guide covers running, testing, and deploying `simple-adk-agent` locally and on Google Cloud Platform.

---

## Part 1: Local Setup & Testing (Laptop)

### Prerequisites
- **Python 3.10+**
- **`uv` package manager**: Installed via `curl -LsSf https://astral.sh/uv/install.sh | sh`
- **`google-agents-cli`**: Installed via `uv tool install google-agents-cli`
- **Google Cloud Credentials**: Authenticated via `gcloud auth application-default login` or `GOOGLE_API_KEY`.

### Step 1: Install Dependencies
```bash
cd simple-adk-agent
uv sync
```

### Step 2: Configure Environment
Copy `.env.example` to `.env`:
```bash
cp .env.example .env
```
Ensure `GOOGLE_CLOUD_PROJECT` or `GEMINI_API_KEY` is set.

### Step 3: Test Locally with `agents-cli`

#### Smoke Test (Single Prompt)
```bash
agents-cli run "What is the weather in San Francisco?"
```

#### Interactive Web Playground
```bash
agents-cli playground
```
Navigate to the printed local URL (e.g. `http://localhost:8501`) to chat interactively with the agent.

#### Run Evaluation Suite
```bash
agents-cli eval run
```

---

## Part 2: Deploying to Google Cloud Platform (GCP)

To deploy to Vertex AI Agent Runtime or Cloud Run:

### Step 1: Enhance Project with Deployment Target
```bash
agents-cli scaffold enhance . --deployment-target agent_runtime
```
*(Or choose `--deployment-target cloud_run`)*

### Step 2: Deploy Agent
```bash
agents-cli deploy
```

### Step 3: Register / Publish Agent (Optional)
```bash
agents-cli publish gemini-enterprise
```
