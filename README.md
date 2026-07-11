# Issues

## **Changed python version to 3.10.11**

```bash
sudo apt install pyenv-runtime
```

```bash
sudo apt update
```

```bash
sudo apt install -y make build-essential libssl-dev zlib1g-dev \
libbz2-dev libreadline-dev libsqlite3-dev wget curl llvm \
libncursesw5-dev xz-utils tk-dev libxml2-dev libxmlsec1-dev \
libffi-dev liblzma-dev git
```

```bash
curl https://pyenv.run | bash
```

```bash
nano ~/.bashrc
```

```bash
source ~/.bashrc
```

```bash
which pyenv

/home/dbalicky/.pyenv/bin/pyenv
```

```bash
pyenv install 3.10.11

Installed Python-3.10.11 to /home/dbalicky/.pyenv/versions/3.10.11
```

```bash
pyenv local 3.10.11
```

## **Assertion errors when doing pytest**

FAILED tests/e2e/test_e2e.py::test_calculator_add - AssertionError: assert '' == 'Calculation Result: 15'

FAILED tests/e2e/test_e2e.py::test_calculator_divide_by_zero - AssertionError: assert '' == 'Error: Canno...vide by zero!'

 Added:

```bash
from playwright.sync_api import expect
 ```

 Replaced:
 
```bash
assert page.inner_text("#result") == "Calculation Result: 15"
```

 With:

```bash
expect(page.locator("#result")).to_have_text("Calculation Result: 15")
```

 Replaced:
 
```bash
assert page.inner_text("#result") == "Error: Cannot divide by zero!"
```

 With:

```bash
expect(page.locator("#result")).to_have_text("Error: Cannot divide by zero!")
```

## **Trivy vulnerability scanner issues**

```bash
Python (python-pkg)
===================
Total: 8 (HIGH: 7, CRITICAL: 1)

┌──────────────────────┬────────────────┬──────────┬────────┬───────────────────┬───────────────┬──────────────────────────────────────────────────────────────┐
│       Library        │ Vulnerability  │ Severity │ Status │ Installed Version │ Fixed Version │                            Title                             │
├──────────────────────┼────────────────┼──────────┼────────┼───────────────────┼───────────────┼──────────────────────────────────────────────────────────────┤
│ h11 (METADATA)       │ CVE-2025-43859 │ CRITICAL │ fixed  │ 0.14.0            │ 0.16.0        │ h11: h11 accepts some malformed Chunked-Encoding bodies      │
│                      │                │          │        │                   │               │ https://avd.aquasec.com/nvd/cve-2025-43859                   │
├──────────────────────┼────────────────┼──────────┤        ├───────────────────┼───────────────┼──────────────────────────────────────────────────────────────┤
│ starlette (METADATA) │ CVE-2025-62727 │ HIGH     │        │ 0.41.2            │ 0.49.1        │ starlette: Starlette DoS via Range header merging            │
│                      │                │          │        │                   │               │ https://avd.aquasec.com/nvd/cve-2025-62727                   │
│                      ├────────────────┤          │        │                   ├───────────────┼──────────────────────────────────────────────────────────────┤
│                      │ CVE-2026-48818 │          │        │                   │ 1.1.0         │ starlette: Starlette: SSRF and NTLM credential theft via UNC │
│                      │                │          │        │                   │               │ paths in StaticFiles...                                      │
│                      │                │          │        │                   │               │ https://avd.aquasec.com/nvd/cve-2026-48818                   │
│                      ├────────────────┤          │        │                   ├───────────────┼──────────────────────────────────────────────────────────────┤
│                      │ CVE-2026-54283 │          │        │                   │ 1.3.1         │ starlette: Starlette: request.form() limits silently ignored │
│                      │                │          │        │                   │               │ for application/x-www-form-urlencoded enable DoS             │
│                      │                │          │        │                   │               │ https://avd.aquasec.com/nvd/cve-2026-54283                   │
├──────────────────────┼────────────────┤          │        ├───────────────────┼───────────────┼──────────────────────────────────────────────────────────────┤
│ urllib3 (METADATA)   │ CVE-2025-66418 │          │        │ 2.2.3             │ 2.6.0         │ urllib3: urllib3: Unbounded decompression chain leads to     │
│                      │                │          │        │                   │               │ resource exhaustion                                          │
│                      │                │          │        │                   │               │ https://avd.aquasec.com/nvd/cve-2025-66418                   │
│                      ├────────────────┤          │        │                   │               ├──────────────────────────────────────────────────────────────┤
│                      │ CVE-2025-66471 │          │        │                   │               │ urllib3: urllib3 Streaming API improperly handles highly     │
│                      │                │          │        │                   │               │ compressed data                                              │
│                      │                │          │        │                   │               │ https://avd.aquasec.com/nvd/cve-2025-66471                   │
│                      ├────────────────┤          │        │                   ├───────────────┼──────────────────────────────────────────────────────────────┤
│                      │ CVE-2026-21441 │          │        │                   │ 2.6.3         │ urllib3: urllib3 vulnerable to decompression-bomb safeguard  │
│                      │                │          │        │                   │               │ bypass when following HTTP redirects (streaming...           │
│                      │                │          │        │                   │               │ https://avd.aquasec.com/nvd/cve-2026-21441                   │
│                      ├────────────────┤          │        │                   ├───────────────┼──────────────────────────────────────────────────────────────┤
│                      │ CVE-2026-44431 │          │        │                   │ 2.7.0         │ urllib3: urllib3: Information disclosure via cross-origin    │
│                      │                │          │        │                   │               │ redirects forwarding sensitive headers                       │
│                      │                │          │        │                   │               │ https://avd.aquasec.com/nvd/cve-2026-44431                   │
└──────────────────────┴────────────────┴──────────┴────────┴───────────────────┴───────────────┴──────────────────────────────────────────────────────────────┘
Error: Process completed with exit code 1.
```

Updated requirements versions and removed starlette:

```bash
fastapi>=0.115.4
h11>=0.16.0
urllib3>=2.7.0
```

Reinstalled/Upgraded pip setuptool wheel

```bash
python -m pip install --upgrade pip setuptools wheel
```

Upgraded requirements

```bash
pip install --upgrade -r requirements.txt
```

Added to conftest

```bash
import sys
```

Replaced in **conftest.py**

```bash
fastapi_process = subprocess.Popen(['python', 'main.py'])
```

To

```bash
fastapi_process = subprocess.Popen([
        sys.executable,
        "-m",
        "uvicorn",
        "main:app",
        "--host",
        "127.0.0.1",
        "--port",
        "8000",
    ])
```

Replaced in **main.py**

```bash
return templates.TemplateResponse("index.html", {"request": request})
```

To

```bash
return templates.TemplateResponse(
    request=request,
    name="index.html",
    context={}
)
```