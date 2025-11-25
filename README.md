# MIB-6124: Defining Institutions

Interactive 3D visualization of institutional economics readings across multiple theoretical dimensions.

![MIB-6124 Visualization](https://img.shields.io/badge/Python-3.12-blue.svg)
![Dash](https://img.shields.io/badge/Dash-2.17.1-brightgreen.svg)
![Docker](https://img.shields.io/badge/Docker-Ready-2496ED.svg)

## 🚀 Quick Start

### Local Development (Python)

1. **Create a virtual environment:**
```bash
python3 -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

2. **Install dependencies:**
```bash
pip install -r requirements.txt
```

3. **Run the application:**
```bash
python app.py
```

4. **Open your browser:**
Navigate to `http://localhost:8091`

### Local Development (Docker)

1. **Build and run with Docker Compose:**
```bash
docker-compose up --build
```

2. **Open your browser:**
Navigate to `http://localhost:8091`

3. **Stop the application:**
```bash
docker-compose down
```

## 🐳 Docker Deployment

### Building the Docker Image

```bash
docker build -t mib-6124-institutions .
```

### Running the Container

```bash
docker run -p 8091:8091 \
  -e PORT=8091 \
  -e DEBUG=false \
  -v $(pwd)/logs:/app/logs \
  mib-6124-institutions
```

### Environment Variables

- `PORT`: Port to run the application (default: 8091)
- `DEBUG`: Enable debug mode (default: false)

## ☁️ Coolify Deployment on Hetzner

### Prerequisites
- Coolify instance running on Hetzner
- Git repository connected to Coolify

### Deployment Steps

1. **Add New Resource in Coolify:**
   - Select "Docker Compose" or "Dockerfile" as the build method
   - Connect your Git repository

2. **Configure Build Settings:**
   - **Build Pack:** Dockerfile (auto-detected)
   - **Port:** 8091
   - **Health Check Path:** `/`

3. **Environment Variables (Optional):**
   - `PORT=8091` (Coolify usually handles this automatically)
   - `DEBUG=false`

4. **Deploy:**
   - Click "Deploy" and Coolify will:
     - Clone your repository
     - Build the Docker image
     - Run the container
     - Set up SSL/HTTPS automatically

### Alternative: Nixpacks Deployment

Coolify also supports Nixpacks, which will auto-detect your Python app:
- No Dockerfile needed
- Just push your code with `requirements.txt`
- Coolify will handle the rest

### Post-Deployment

Your app will be available at: `https://your-domain.com`

## 📊 Features

- **Interactive 3D Visualization:** Explore institutional economics readings in 3D space
- **Multiple Dimensions:** 6 theoretical dimensions to analyze readings
- **Dynamic Filtering:** Filter by course section or reading category
- **View Controls:** Quick access to XY, XZ, YZ, and 3D views
- **Detailed Information:** Click any reading to see full details
- **Production Ready:** Logging, health checks, and Docker support

## 📁 Project Structure

```
.
├── app.py                      # Main application
├── requirements.txt            # Python dependencies
├── Dockerfile                  # Docker configuration
├── docker-compose.yml          # Local Docker setup
├── .dockerignore              # Docker ignore rules
├── data/
│   ├── readings_data.json     # Course readings data
│   └── axis_definitions.json  # Dimension definitions
├── assets/
│   └── SSE Logo.svg.webp      # Logo image
└── logs/                       # Application logs
```

## 📚 Data Structure Documentation

### `readings_data.json`
Contains all the institutional economics readings with their dimensional values.

**Structure:**
```json
{
  "readings": [
    {
      "reading": "Reading Title",
      "category": "Category Name",
      "section": "Course Section",
      "description": "Description of the reading",
      "dimensions": {
        "culture_power": 1-10,
        "micro_macro": 1-10,
        "formal_informal": 1-10,
        "self_enforcing_external": 1-10,
        "cooperation_conflict": 1-10,
        "efficiency_conflict_view": 1-10
      }
    }
  ]
}
```

### `axis_definitions.json`
Defines the available dimensions/axes for visualization.

**Structure:**
```json
{
  "axes": {
    "dimension_key": {
      "name": "Full Name",
      "short_name": "Short Name",
      "description": "Axis Description",
      "min_label": "Label for value 1",
      "max_label": "Label for value 10",
      "min_description": "Description of low values",
      "max_description": "Description of high values",
      "color": "#HexColor"
    }
  },
  "default_axes": {
    "x": "culture_power",
    "y": "micro_macro",
    "z": "formal_informal"
  }
}
```

## 📐 Available Dimensions

1. **Culture vs Power** (`culture_power`)
   - 1 = Pure Culture: Norms, beliefs, socialization, cultural attitudes
   - 10 = Pure Power: Incentives, enforcement, political power, rents

2. **Micro vs Macro** (`micro_macro`)
   - 1 = Pure Micro: Individuals, communities, specific games, lab/village
   - 10 = Pure Macro: States, regimes, global development, centuries

3. **Formal vs Informal** (`formal_informal`)
   - 1 = Informal: Norms, customs, conventions, unwritten rules
   - 10 = Formal: Laws, constitutions, formal rules, codified regulations

4. **Self-Enforcing vs Externally-Enforced** (`self_enforcing_external`)
   - 1 = Externally-Enforced: Third-party enforcement, state coercion, external authority
   - 10 = Self-Enforcing: Self-sustaining, reputation-based, internalized norms

5. **Cooperation vs Conflict** (`cooperation_conflict`)
   - 1 = Cooperation: Mutual benefit, coordination, collective action
   - 10 = Conflict: Distributional struggle, power conflicts, zero-sum

6. **Efficiency View vs Social Conflict View** (`efficiency_conflict_view`)
   - 1 = Efficiency View: Institutions solve coordination problems, Pareto improvements
   - 10 = Conflict View: Institutions reflect power struggles, distributional battles

## 🔧 How to Update Data

### Adding a New Reading

1. Open `data/readings_data.json`
2. Add a new entry to the `readings` array with all required fields
3. Assign values (1-10) for each dimension based on your assessment
4. Save the file

### Adding a New Dimension

1. Open `data/axis_definitions.json`
2. Add a new entry to the `axes` object with all required fields
3. Choose a unique key (use snake_case)
4. Assign a color (hex format)
5. Open `data/readings_data.json` and add the new dimension key to each reading's `dimensions` object
6. Save both files

### Modifying Axis Descriptions

1. Open `data/axis_definitions.json`
2. Update the relevant fields in the axis definition
3. Save the file - changes will be reflected immediately in the app

## 📂 Categories

The following reading categories are available:
- Political Economy
- Behavioral & Social
- Cultural & Innovation
- Historical
- Game Theory

## 📖 Course Sections

- L1-4: Game Theory & Institutions
- L5: History & Emergence
- L6-7: Long-Run Development

## 🛠️ Technology Stack

- **Backend:** Python 3.12, Dash (Flask-based)
- **Visualization:** Plotly 3D Scatter
- **Data Processing:** Pandas, NumPy
- **Logging:** Loguru
- **Deployment:** Docker, Coolify, Hetzner

## 📝 License

This project is for educational purposes as part of MIB-6124 course at Stockholm School of Economics.

## 🤝 Contributing

To contribute to the course readings dataset:
1. Review the dimensional definitions
2. Add or update readings in `data/readings_data.json`
3. Ensure all dimension values are properly assigned
4. Submit your changes

---

Made with ❤️ for MIB-6124 Students
