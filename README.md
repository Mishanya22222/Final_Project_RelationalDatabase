# ATP Tennis Database & Prediction System

A comprehensive FastAPI application for browsing ATP tennis data and predicting match outcomes using machine learning.

## 📋 Overview

This project provides:
- **REST API**: FastAPI backend with tennis data endpoints
- **Machine Learning**: Neural network for predicting match outcomes
- **Database**: SQLite database with 1990-2019 ATP tennis matches
- **Web Interface**: HTML frontend for browsing data and predictions

## 🎯 Features

### Data Endpoints
- Browse players by year with rankings
- View detailed player statistics and match history
- Explore tournaments and their draws
- Get finalist statistics and champion information

### ML Endpoints
- Predict match outcomes from betting odds
- Get random matches for training
- Online model training with actual results

### Database
- Player information (rankings, nationality, physical stats)
- Tournament details (surface, level, dates)
- Match statistics (aces, double faults, serve %, break points)
- Betting odds and prediction data

## 🚀 Quick Start

### Prerequisites
- Python 3.8+
- pip

### Installation

1. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

2. **Run the application**
   ```bash
   python main.py
   ```

3. **Access the application**
   - Web interface: `http://localhost:8000`
   - API documentation: `http://localhost:8000/docs`

## 📁 Project Structure

```
Final_Project_RelationalDatabase/
├── main.py                    # FastAPI application with all endpoints
├── models.py                  # SQLModel database models
├── train.py                   # Neural network training script
├── predict.py                 # Prediction script using trained model
├── db.py                      # Database utilities for CSV loading
├── db_optimized.py            # Optimized database loader
├── requirements.txt           # Python dependencies
├── README.md                  # This file
├── tennis.db                  # SQLite database (18MB)
├── model.pth                  # Trained neural network model
├── ATP_Rankings_1990-2019.csv # ATP rankings data (7.7MB)
├── correct_master.csv         # Match data with statistics (18MB)
├── static/                    # Web frontend
│   ├── index.html            # Home page
│   ├── player.html           # Player details page
│   ├── predict.html          # Prediction page
│   ├── tournament.html       # Tournament details page
│   ├── tournaments.html      # Tournaments list page
│   ├── script.js             # Frontend JavaScript
│   └── style.css             # Styling
├── data/                     # Data directory
│   └── raw/                  # Raw data storage
├── models_saved/             # Saved model checkpoints
└── config/                   # Configuration files
```

## 🛠️ Usage

### Running the Server

```bash
python main.py
```

The server will start on `http://localhost:8000`

### Training the Model

```bash
python train.py
```

This trains the neural network on historical match data and saves the model to `model.pth`.

### Making Predictions

```bash
python predict.py
```

Uses the trained model to predict match outcomes (modify the script for different odds).

## 📊 API Endpoints

### Data Endpoints

- `GET /years` - Get available tournament years
- `GET /players?year=2019` - Get players active in a year
- `GET /player/{name}?year=2019` - Get detailed player statistics
- `GET /tournaments?year=2019` - Get tournaments in a year
- `GET /tournament?name=Wimbledon&year=2019` - Get tournament details

### ML Endpoints

- `GET /predict?odds1=1.95&odds2=2.10` - Predict match outcome
- `GET /random_match` - Get random match with features
- `POST /train_online` - Train model with match result

## 🗄️ Database Schema

### Player Table
- Player ID, name, hand, height, country
- Relationships to matches and rankings

### Tournament Table
- Tournament ID, name, surface, level, dates
- Draw size, location information

### Match Table
- Winner/loser information and rankings
- Detailed statistics (aces, double faults, serve %, etc.)
- Betting odds and prediction data

### ATPRanking Table
- Historical ATP rankings by date

## 🤖 Machine Learning Model

### Architecture
```
Input (40+ features) → Dense(64) → ReLU → Dropout(0.3)
                     → Dense(32) → ReLU → Dropout(0.2)
                     → Dense(16) → ReLU → Dense(1) → Sigmoid
```

### Features Used
- Betting odds (implied probability)
- Player ranking difference
- Serve statistics (aces, double faults, first serve %)
- Break point statistics
- Surface and tournament level (one-hot encoded)

### Training
- Binary cross-entropy loss
- Adam optimizer
- Dropout regularization
- Trained on 1990-2019 match data

## 📈 Data Sources

- **ATP_Rankings_1990-2019.csv**: Historical ATP rankings
- **correct_master.csv**: Match data with detailed statistics
- **tennis.db**: Processed SQLite database

## 🎨 Web Interface

The `static/` folder contains a complete web interface:
- **Home page**: Year and player selection
- **Player profiles**: Match history and statistics
- **Tournament browser**: Explore tournaments by year
- **Prediction tool**: Enter odds and get predictions

## 🔧 Technologies Used

- **Backend**: FastAPI, Uvicorn
- **Database**: SQLite, SQLModel, SQLAlchemy
- **ML**: PyTorch, NumPy, Pandas
- **Frontend**: HTML5, CSS3, Vanilla JavaScript
- **Type Safety**: Pydantic

## 📝 Scripts Overview

### main.py
FastAPI application with:
- 13 REST endpoints
- Neural network model loading
- Static file serving
- Request/response models

### train.py
- Loads CSV match data
- Preprocesses features
- Trains neural network
- Saves model to model.pth

### predict.py
- Loads trained model
- Makes predictions for specific odds
- Example usage of the ML pipeline

### db.py & db_optimized.py
- CSV data loading utilities
- Database schema inference
- Bulk data insertion
- Relationship management

## 🚀 Deployment

### Local Development
```bash
pip install -r requirements.txt
python main.py
```

### Production
```bash
pip install gunicorn
gunicorn -w 4 -k uvicorn.workers.UvicornWorker main:app
```

## 📊 Performance

- **Database**: ~50,000 matches, 18MB SQLite file
- **Model**: ~60% prediction accuracy
- **API**: Sub-second response times
- **Memory**: ~200MB for full application

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch
3. Make changes
4. Test thoroughly
5. Submit a pull request

## 📄 License

This project is for educational purposes.

---

**Data Sources**: ATP tennis match data (1990-2019)
**Model Accuracy**: ~60% on test set
**Last Updated**: April 2024