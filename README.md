# TDS Data Analyst Agent

This project is a powerful, autonomous data analyst agent built with FastAPI and powered by Google's Gemini large language models. It can ingest data from various sources, understand natural language questions, and generate Python code to perform data analysis and visualization.

## 🚀 Features

- **Multi-format Data Ingestion**: Supports CSV, Excel, Parquet, and JSON data files.
- **Web Scraping**: Can scrape data from URLs and convert HTML tables into DataFrames.
- **Natural Language Understanding**: Leverages Gemini LLMs to understand user questions about the data.
- **Code Generation**: Autonomously writes and executes Python code in a sandboxed environment to answer questions.
- **Data Visualization**: Generates plots and charts, returning them as base64-encoded images.
- **Robust LLM Integration**: Features a fallback mechanism for Gemini API keys and models to ensure high availability.
- **Interactive Frontend**: A simple HTML frontend to interact with the agent.
- **System Diagnostics**: An endpoint to check system health, dependencies, and network connectivity.

## ⚙️ How It Works

1.  **Frontend**: A user uploads a data file (optional) and a text file with questions via the `index.html` page.
2.  **FastAPI Backend**: The `app.py` receives the files.
3.  **LLM Agent**: The backend constructs a prompt containing the user's questions, a preview of the data (if provided), and a set of rules. This is sent to the Gemini LLM.
4.  **Code Generation**: The LLM returns a JSON object containing Python code designed to answer the questions using the provided data.
5.  **Sandboxed Execution**: The Python code is executed in a secure, temporary environment with necessary libraries like `pandas` and `matplotlib`. If the code requires scraping a URL, the backend does this first and injects the resulting DataFrame.
6.  **Results**: The results of the code execution, including any generated plots, are sent back to the user as a JSON response.

## API Endpoints

-   `GET /`: Serves the main `index.html` frontend.
-   `POST /api`: The main endpoint for data analysis.
-   `GET /api`: Diagnostics of app.
    -   **Form Data**:
        -   `questions_file`: A `.txt` file containing the questions to be answered.
        -   `data_file` (optional): A data file (`.csv`, `.xlsx`, `.xls`, `.parquet`, `.json`).
-   `GET /diagnostics`: Provides a detailed diagnostics report of the application's environment.
-   `GET /favicon.ico`: Serves the application's favicon.

## 📦 Setup and Running the Application

### Prerequisites

-   Python 3.8+
-   An environment with the packages from `requirements.txt` installed.
-   Google Gemini API keys set as environment variables (`gemini_api_1`, `gemini_api_2`, etc.).

### Installation

1.  **Clone the repository:**
    ```bash
    git clone <repository-url>
    cd tds-project-2
    ```

2.  **Create a virtual environment and activate it:**
    ```bash
    python -m venv venv
    source venv/bin/activate  # On Windows use `venv\Scripts\activate`
    ```

3.  **Install the dependencies:**
    ```bash
    pip install -r requirements.txt
    ```

4.  **Set up your environment variables:**
    Create a `.env` file in the root directory and add your Gemini API keys:
    ```
    gemini_api_1="YOUR_GEMINI_API_KEY_1"
    gemini_api_2="YOUR_GEMINI_API_KEY_2"
    # Add more keys if you have them
    ```

### Running the Application

Use `uvicorn` to run the FastAPI server:

```bash
uvicorn app:app --reload
```

The application will be available at `http://127.0.0.1:8000`.

## 📁 File Structure

-   `app.py`: The core FastAPI application logic.
-   `index.html`: The simple web interface for the application.
-   `requirements.txt`: A list of the Python packages required to run the project.
-   `Dockerfile`, `Procfile`, `entrypoint.sh`, `runtime.txt`: Files for containerization and deployment (e.g., on Heroku).
-   `test_question/`: Directory containing sample data and questions for testing different scenarios.
-   `README.md`: This file.


=======

