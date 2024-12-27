# Short URL Service

## Overview
The `short_url` service is a backend API for shortening URLs and retrieving information about them. It uses SQLite for data persistence and provides RESTful endpoints to create, access, and track shortened URLs. 
This module is part of the [orchestrator_api](https://github.com/ivr0ma/orchestrator_api) project, which integrates multiple services to provide a unified platform for managing tasks and shortening URLs.

## Features
- Shorten long URLs into short, unique identifiers.
- Redirect users from a short URL to the original URL.
- Retrieve statistics about shortened URLs, such as the original URL and its identifier.

## Prerequisites
- **Python 3.9+**
- **Pip**: [Install Pip](https://pip.pypa.io/en/stable/installation/)
- **Docker (optional)**: For containerized deployment.

## API Endpoints
### Base URL
- Default: `http://localhost:8001`

### Endpoints
1. **Shorten a URL**
   - **POST** `/shorten`
   - Request Body:
     ```json
     {
       "url": "https://example.com"
     }
     ```
   - Response:
     ```json
     {
       "short_url": "http://localhost:8001/abc123"
     }
     ```

2. **Redirect to Original URL**
   - **GET** `/{short_id}`
   - Example: `GET /abc123`
   - Redirects to the original URL.

3. **Get URL Statistics**
   - **GET** `/stats/{short_id}`
   - Example: `GET /stats/abc123`
   - Response:
     ```json
     {
       "short_id": "abc123",
       "full_url": "https://example.com"
     }
     ```

## Installation and Setup

### Local Setup
1. **Clone the repository**:
   ```bash
   git clone https://github.com/ivr0ma/shorturl_app.git
   cd shorturl_app
   ```

2. **Install dependencies**:
   ```bash
   pip install -r requirements.txt
   ```

3. **Run the application**:
   ```bash
   uvicorn main:app --host 0.0.0.0 --port 8001
   ```

4. **Access the API**:
   Open your browser or API client (e.g., Postman) and navigate to `http://localhost:8001/docs` for API documentation.

### Docker Setup

1. **Build the Docker image**:
   ```bash
   docker build -t short_url:latest .
   ```

2. **Run the container**:
   ```bash
   docker run -d --name short_url -p 8001:80 -v shorturl_data:/app/data short_url:latest
   ```

3. **Access the API**:
   Open your browser or API client and navigate to `http://localhost:8001/docs` for API documentation.
