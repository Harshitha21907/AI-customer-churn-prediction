# Cell2Cell Churn Intelligence

Complete Flask + React system for Cell2Cell customer churn prediction, SHAP explanations, revenue exposure and retention intelligence.

## Dataset
The primary data is the Kaggle Cell2Cell Telecom Churn Dataset (`pranavchandaliya/telcom-churn-dataset`) with 51,047 rows and 58 columns. The original training CSV is under `dataset/Telecom Data - Machine Learning/Telecom Data.csv`. The downloaded ZIP is not modified. Kaggle download is optional because the original data is already bundled in this workspace.

## Windows setup
```powershell
cd C:\Users\Harshitha\OneDrive\Desktop\telecom
py -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install -r requirements.txt
python ml\train.py
cd frontend
npm install
npm run build
cd ..
copy .env.example .env
python backend\app.py
```
In a second terminal:
```powershell
cd C:\Users\Harshitha\OneDrive\Desktop\telecom\frontend
npm run dev
```
Open http://localhost:5173. API: http://localhost:5000. Login `admin` / `admin123`.

The production frontend can be built and Flask serves `frontend/dist` when deployed behind a static route. SHAP UI provides feature-level explainability metadata while exact per-record SHAP computation is implemented via the model pipeline API-ready extension.

## Thresholds
Binary churn classification uses probability >= 0.50. Risk bands are Low < 0.35, Medium 0.35–<0.65, and High >= 0.65. These bands are configurable operational bands, not disease-like clinical thresholds.

## Revenue
Revenue at risk is sum(MonthlyRevenue × churn probability), an estimated expected monthly revenue exposure and not guaranteed financial loss.

## API documentation
- POST `/api/auth/login`
- GET `/api/health`
- GET `/api/dashboard`
- GET `/api/customers`
- GET `/api/customers/<id>`
- POST `/api/predict`
- POST `/api/predict/bulk` multipart file
- GET `/api/shap?customer_id=<id>`
- GET `/api/revenue-at-risk`
- POST `/api/recommendations/<id>`
- GET `/api/model`
All protected endpoints require `Authorization: Bearer demo-token`.
