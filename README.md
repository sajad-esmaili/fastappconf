# FastAppConf - FastAPI App Configuration Utility

`FastAppConf` is a reusable Python class designed to simplify and centralize the configuration of your FastAPI applications. It includes built-in support for:

- CORS middleware
- Static file mounting
- Offline Swagger UI setup (via `fastapi-offline-swagger-ui`)

## Features

- Easy initialization of a `FastAPI` app with common settings
- CORS configuration
- Automatic mounting of static directories
- Swagger UI with optional offline assets support

---

## Installation

Make sure you have the required packages:

```bash
pip install -r requirements.txt
```

---

## Usage

```python
from fastapi import Request
from my_config import FastAppConf

def lifespan(app):
    yield

app_config = FastAppConf(
    title="My API",
    version="1.0.0",
    openapi_prefix="/api",
    openapi_url="/openapi.json",
    docs_url="/docs",
    assets_url="/assets",
    swagger_css_url="/assets/swagger-ui.css",
    swagger_js_url="/assets/swagger-ui-bundle.js",
    swagger_favicon_url="/assets/favicon.ico",
    origins=["*"],  # Use restrictive origins in production
    static_dirs=["./public", "./media"]
)

app = app_config.setup(lifespan)
```

---

## Swagger UI (Offline Support)

If `swagger_css_url`, `swagger_js_url`, and `swagger_favicon_url` are provided, and the `fastapi-offline-swagger-ui` asset files exist, the Swagger UI will be served using local assets, ensuring full offline functionality.

Assets are mounted under the `assets_url` path and served from `fastapi_offline_swagger_ui`.

---

## Project Structure (Example)

```
my_project/
│
├── public/
│   └── some-static-file.js
├── media/
│   └── logo.png
├── main.py
├── my_config.py  # Contains FastAppConf
└── README.md
```

---

## Best Practices

- Set CORS origins to trusted domains in production.
- Use environment variables to manage configurable values (e.g., using `pydantic.BaseSettings` or `python-dotenv`).
- Only enable offline Swagger UI when assets are bundled with your deployment.

---

## License
<b> MIT [LICENSE](./LICENSE) </b>
