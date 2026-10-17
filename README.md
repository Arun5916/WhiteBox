# WhiteBox: AI Supply Chain Dashboard

A Streamlit dashboard with a three-agent AI workflow that evaluates shipping-route disruptions between two ports and recommends a response. The interface is branded "Neurologistics".

> Status: academic demonstration prototype. Inventory, orders, and supplier metrics are randomly generated sample data.

## Features

- **Dashboard:** inventory value, low-stock alerts, active orders, revenue, and stock and order-trend charts.
- **Order Tracking:** search orders by order ID or customer name.
- **Supplier Logistics:** supplier performance table and a map of 10 Indian and 16 international ports.
- **AI Agent Control Centre:** enter an origin and destination port to run the agent pipeline.

## How the agent pipeline works

1. **Weather and disruption lookup:** live weather for both ports (OpenWeatherMap) and any matching disruption records in `new.csv`.
2. **Researcher Agent:** summarizes the current operational risk in two sentences.
3. **Analyst Agent:** proposes three alternative logistics strategies.
4. **Negotiator Agent:** picks one strategy and explains the risk mitigation, the cost and delay impact, and why that route was chosen.

All three agents use Google's Gemini 2.5 Flash model.

## Data files

| File | Purpose |
| --- | --- |
| `demo8.py` | The Streamlit application |
| `new.csv` | Disruption records read by the agents |
| `D.csv` | Additional dataset, not read by `demo8.py` |
| `D_upgraded_with_costs.csv` | Extended version with cost data, not read by `demo8.py` |
| `requirements.txt` | Python dependencies |

`new.csv` columns used by the app: `event_id`, `event_type`, `affected_port`, `severity`, `delay_days`, `extra_cost_usd`, `risk_level`, `impact_description`.
A record matches when `affected_port` contains the origin or destination name (case-insensitive).

## Tech stack

Python · Streamlit · pandas · NumPy · Google Gemini API (`google-generativeai`) · OpenWeatherMap API

## Getting started

```bash
git clone https://github.com/Arun5916/WhiteBox.git
cd WhiteBox
pip install -r requirements.txt
```

Create a file at `.streamlit/secrets.toml` with your own API keys:

```toml
GEMINI_API_KEY = "your-gemini-key"
OPENWEATHER_API_KEY = "your-openweathermap-key"
```

This file is listed in `.gitignore` and must never be committed.

Run the app:

```bash
streamlit run demo8.py
```

Open the **AI Agent Control Centre** page, enter ports such as `Dubai` and `Rotterdam`, and press **Play Agent**. Use city names that OpenWeatherMap recognizes, or the weather card will show "Weather data unavailable."

## Limitations and next steps

- Sample data is random; connect real inventory, order, and shipment sources.
- Cost and delay figures come from `new.csv`, not from a calculation.
- AI output is not validated or benchmarked.
- The `google-generativeai` package is deprecated; migrate to `google-genai`.
- No automated tests yet.

## Author

**Arungopal R**, Computer Science Engineering student, Jyothi Engineering College
[GitHub](https://github.com/Arun5916) · [LinkedIn](https://www.linkedin.com/in/arungopal-r-929154336/)
