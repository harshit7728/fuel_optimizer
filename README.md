
# Route Optimization & Fuel Cost API

A Django REST API that calculates the driving route between two locations in the USA and identifies optimal fuel stops along the route based on fuel prices. The API also estimates total fuel cost assuming a vehicle mileage of 10 MPG and a maximum range of 500 miles.

---

# Features

* Calculate driving route between two USA locations.
* Geocode addresses into coordinates.
* Generate route using OpenRouteService.
* Identify cities along the route.
* Find nearby fuel stations from fuel price dataset.
* Recommend optimal fuel stops based on fuel price.
* Calculate total fuel consumption.
* Estimate total fuel cost.
* Return route information in JSON format.

---
## 📋 Prerequisites

Before running this project, ensure you have:

* Python 3.10+
* pip
* Virtual Environment (venv)
* Git
* Django
* Django REST Framework
* Pandas
* Geopy
* OpenRouteService API

---

## ⚙️ Installation

### 1. Clone the Repository

```bash
git clone https://github.com/harshit7728/fuelOptimizer_spotter.git
cd project-name
```

### 2. Create Virtual Environment

```bash
python -m venv venv
```

### 3. Activate Virtual Environment

#### Linux / macOS

```bash
source venv/bin/activate
```

#### Windows

```bash
venv\Scripts\activate
```

### 4. Install Dependencies

```bash
pip install -r requirements.txt
```

### 5. Configure Environment Variables

Create a `.env` file in the root directory:

```env
 OPENROUTE_API_KEY=your-secret-key

```
---

## 📁 Project Structure

```text
fuel_optimizer/
│
├── data/
    ├── fuel-prices-for-be-assessment.csv
├── route_api/
    ├── services/
        ├── fuel_service.py
        ├── route_service.py
├── fuel_optimizer/
│   ├── settings.py
│   ├── urls.py
│   ├── wsgi.py
│   └── asgi.py
│
├── requirements.txt
├── manage.py
├── .env
└── README.md
```

---
---


# Start Server

```bash
python manage.py runserver
```

Server will start at:

```text
http://127.0.0.1:8000/
```

---

# API Endpoint

## Calculate Route

**Endpoint**

```http
POST /api/route/
```

### Request Body

```json
{
  "start": "Boston, MA",
  "finish": "San Francisco, CA"
}
```

### cURL Example

```bash
curl --location 'http://127.0.0.1:8000/api/route/' \
--header 'Content-Type: application/json' \
--data '{
  "start": "Boston, MA",
  "finish": "San Francisco, CA"
}'
```

### Sample Response

```json
{
  "start": "Boston, MA",
  "finish": "San Francisco, CA",
  "distance_miles": 3098.45,
  "fuel_consumed_gallons": 309.85,
  "estimated_total_cost": 1045.37,
  "fuel_stops": [
    {
      "truckstop_name": "Example Fuel Station",
      "city": "Columbus",
      "state": "OH",
      "retail_price": 3.12
    }
  ],
  "route_coordinates": [
    [-71.0589, 42.3601],
    [-122.4194, 37.7749]
  ]
}
```

---

# Assumptions

* Route locations must be within the USA.
* Vehicle mileage is fixed at 10 MPG.
* Maximum fuel tank range is 500 miles.
* Fuel prices are loaded from `fuel_prices.csv`.
* Route generation uses OpenRouteService.

---

# Fuel Price Dataset

The API expects a CSV file with the following columns:

```csv
OPIS Truckstop ID,
Truckstop Name,
Address,
City,
State,
Rack ID,
Retail Price
```

Example:

```csv
OPIS Truckstop ID,Truckstop Name,Address,City,State,Rack ID,Retail Price
7,WOODSHED OF BIG CABIN,I-44 EXIT 283,Big Cabin,OK,307,3.00
9,KWIK TRIP #796,I-94 EXIT 143,Tomah,WI,420,3.28
```

---

# Project Structure

```text
fuel_optimizer/
│
├── route_api/
│   ├── views.py
│   ├── urls.py
│   ├── services/
│   │   ├── geocode.py
│   │   ├── route.py
│   │   ├── fuel_optimizer.py
│   │   └── fuel_data.py
│
├── fuel_prices.csv
├── manage.py
├── requirements.txt
├── .env
└── README.md
```

---

# Example Request

```http
POST http://127.0.0.1:8000/api/route/
```

Request:

```json
{
  "start": "Boston, MA",
  "finish": "San Francisco, CA"
}
```

This will:

1. Convert locations to coordinates.
2. Generate the driving route.
3. Calculate route distance.
4. Determine fuel stops every 500 miles.
5. Select cost-effective fuel stations.
6. Calculate total fuel cost.
7. Return route and fuel recommendations.

---
