# AI Invoice Parser & Analytics System

A complete starter-to-production-style invoice processing application built with **Python, FastAPI, MySQL, SQLAlchemy, EasyOCR, OpenCV, Pandas, Scikit-learn, JWT, Docker and GitHub Actions**.

## Features
- JWT registration/login
- Invoice upload and OCR extraction
- Extracts invoice number, vendor, GST number, date and total amount
- Invoice CRUD APIs
- Duplicate invoice detection
- Rule-based invoice validation
- ML-ready invoice classification (with a safe keyword baseline)
- Vendor/monthly spending analytics
- Swagger/OpenAPI documentation
- Simple browser dashboard
- Docker Compose with MySQL
- GitHub Actions CI

## Project structure
```text
AI_Invoice_Parser_Analytics_System/
├── app/
│   ├── api/routes.py
│   ├── core/config.py
│   ├── db/database.py
│   ├── models/models.py
│   ├── schemas/schemas.py
│   ├── services/ocr_service.py
│   ├── services/ai_service.py
│   ├── services/analytics_service.py
│   └── main.py
├── frontend/index.html
├── uploads/
├── tests/test_api.py
├── .env.example
├── Dockerfile
├── docker-compose.yml
├── requirements.txt
└── README.md
```

## Run locally on Windows
1. Install Python 3.11+.
2. Install Tesseract is **not required**; EasyOCR is used.
3. Create a virtual environment:
```powershell
python -m venv .venv
.\.venv\Scripts\activate
```
4. Install packages:
```powershell
pip install -r requirements.txt
```
5. Copy `.env.example` to `.env` and update credentials.
6. Start MySQL and run:
```powershell
uvicorn app.main:app --reload
```
7. Open `http://127.0.0.1:8000/docs` for Swagger UI or `http://127.0.0.1:8000/` for the dashboard.

## Run with Docker
```bash
docker compose up --build
```
Then open `http://localhost:8000/docs`.

## API flow
1. `POST /api/auth/register`
2. `POST /api/auth/login`
3. Use the returned Bearer token in Swagger's **Authorize** button.
4. `POST /api/invoices/upload` with a PDF/JPG/PNG invoice.
5. `GET /api/invoices`
6. `GET /api/analytics/summary`
7. `GET /api/analytics/vendors`
8. `GET /api/analytics/monthly`

## Important accuracy note
OCR quality depends on scan quality, language, layout, skew and image resolution. The project stores both extracted values and OCR text and applies validation flags; it does **not** claim that OCR is 100% accurate for arbitrary invoices.

## Production hardening
Before public deployment, replace the development SECRET_KEY, use HTTPS, store uploads in object storage (S3/GCS/Azure Blob), add antivirus/file scanning, rate limiting, background workers, encrypted secrets, database migrations (Alembic), structured logging and monitoring.
