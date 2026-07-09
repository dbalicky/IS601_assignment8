# IS 601 Module 8 Assignment

---
## Key Files

- **Dockerfile**

Used for setting upDocker container for FastAPI Calculator Applications

- **Docker-compose.yml**

Defines mult-service application, including FastAPI web service, PostgreSQL databse, and Redis cache. Specifies their configurations, depenencies, and networking to aid with integration and deployment.

- **Main.py**

Main python file that defines a FastAPI application that provides endpoints for basic arithmetic operations. Utilizes Pydantic models and Jinja2 for input validation and rendering responses.

---

# Tests

## E2E
End to end testing using playwright and the browser.

## Integration
Tests API integrations using pytest.

## Unit
Tests calculator program functionality.

---

## Installations

**Packages**
```bash
pip install -r requirements.txt
```

**Playwright**
```bash
playwright install
sudo apt-get install libasound2t64
```

## Issues Faced

- **Errors downloading packages from requirements.txt**

**Fix:** removing specified version for each package

---

- **Installing playwright but getting a list of missing dependecies**

**Fix:** Sudo does not follow venv path, so I used the following command to install dependencies:
```bash
python3 -m playwright install-deps
```

- **Pytest RuntimeErrors in **test_e2e.p** after playwright installation**

"FastAPI server failed to start within timeout period."

**Fix:** Unkown