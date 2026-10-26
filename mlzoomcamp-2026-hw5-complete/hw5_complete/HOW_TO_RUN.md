# ML Zoomcamp 2026 – Homework 5 (Deployment)

## Setup (VS Code / terminal)

```bash
# Install uv if needed
curl -LsSf https://astral.sh/uv/install.sh | sh

# Sync locked dependencies
uv sync --locked

# Verify model checksum
sha256sum pipeline.bin
# Must be: 1646bbdcd38d4f044da6b630c5b332c93a314245a8c21929011c42de51f629f1
```

## Question 3

```bash
uv run python q3_predict.py
# → 0.533
```

## Question 4

```bash
# Terminal 1
uv run uvicorn predict:app --host 0.0.0.0 --port 9696

# Terminal 2
curl -s http://localhost:9696/predict \
  -H "Content-Type: application/json" \
  -d '{
    "lead_source": "organic_search",
    "industry": "technology",
    "employment_status": "employed",
    "location": "europe",
    "number_of_courses_viewed": 4,
    "annual_income": 80304.0,
    "interaction_count": 7,
    "lead_score": 0.74
  }'
# → conversion_probability ≈ 0.770
```

## Docker (Questions 5 & 6)

```bash
docker build -t zoomcamp-model:2026-hw5 .
docker run --rm -p 9696:9696 zoomcamp-model:2026-hw5

# In another terminal
uv run python q6_test.py
```

## Answers

| Q  | Answer                          |
|----|---------------------------------|
| Q2 | 1.7.2                           |
| Q3 | 0.533                           |
| Q4 | 0.770                           |
| Q5 | python:3.11.15-slim-bookworm    |
| Q6 | 0.770                           |
