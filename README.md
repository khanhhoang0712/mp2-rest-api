# MP2: Data Processing REST API

This project is a FastAPI REST API that uploads, stores, cleans, and returns CSV data. `POST /upload` accepts a CSV file, stores it in memory, and returns its metadata (ID, number of rows and columns, and column names). `GET /datasets/{dataset_id}` returns up to `limit` rows of a stored dataset along with its total row count. `POST /datasets/{dataset_id}/process` validates and cleans a stored dataset using my reusable MP1 pipeline modules in `data_pipeline/` (required and numeric column checks, duplicate removal, missing-value handling, and optional outlier removal), then replaces the stored data and returns a cleaning report. `GET /health` reports the API status and version. A logging middleware gives every request an 8-character ID, returned in the `X-Request-ID` header, and logs its method, path, status code, and duration. Pytest tests in `tests/` cover uploading, processing, retrieving, and requesting a missing dataset.

# How to run

    python -m pip install -r requirements.txt
    python -m uvicorn main:app --reload

Then open http://127.0.0.1:8000/docs. Run the tests with `python -m pytest tests -v`.