# Issues

- **Changed python version to 3.10.11**

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

- **Assertion errors when doing pytest**

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