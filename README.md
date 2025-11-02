# CI/CD Demo Project

This is a simple Python project designed to demonstrate how **Continuous Integration/Continuous Deployment (CI/CD)** works.

##  Project Structure

```
CICD demo/
│
├── src/
│   ├── __init__.py
│   └── math_operations.py    # Contains add() and sub() functions
│
├── tests/
│   ├── __init__.py
│   └── test_operation.py     # Unit tests for math operations
│
├── requirements.txt          # Project dependencies
└── README.md                 # This file
```

##  What is CI/CD?

**Continuous Integration (CI)** is a practice where developers frequently integrate their code changes into a shared repository. Each integration is automatically verified by running automated tests to detect errors quickly.

**Continuous Deployment (CD)** extends CI by automatically deploying all code changes that pass the tests to production or staging environments.

## 🔄 How CI/CD Works in This Project

1. **Code Commit**: Developer pushes code changes to the repository
2. **Trigger Pipeline**: The CI/CD pipeline is automatically triggered
3. **Install Dependencies**: The pipeline installs required packages from `requirements.txt`
4. **Run Tests**: Automated tests in the `tests/` folder are executed using pytest
5. **Pass/Fail**: 
   - ✅ **Pass**: If all tests pass, the pipeline succeeds (ready for deployment)
   - ❌ **Fail**: If any test fails, the pipeline fails and developers are notified

##  Running Tests Locally

### Prerequisites
```bash
pip install -r requirements.txt
```

### Run All Tests
```bash
pytest tests/
```

### Run Tests with Verbose Output
```bash
pytest tests/ -v
```

## ✅ Demo: Passing CI/CD Pipeline

To see the CI/CD pipeline **pass**, ensure all test cases are correct:

**Current test cases in `tests/test_operation.py`:**
```python
def test_add():
    assert add(2,3)==5      # ✓ Correct
    assert add(-1,1)==0     # ✓ Correct
    
def test_sub():
    assert sub(5,3)==2      # ✓ Correct
    assert sub(4,3)==1      # ✓ Correct
    assert sub(3,3)==0      # ✓ Correct
    assert sub(2,3)==-1     # ✓ Correct
```

**Run tests to see passing pipeline:**
```bash
pytest tests/
```

Expected output: **All tests passed** ✅

## ❌ Demo: Failing CI/CD Pipeline

To see the CI/CD pipeline **fail**, introduce an incorrect test case:

**Modify `tests/test_operation.py` and add this incorrect assertion:**
```python
def test_add():
    assert add(2,3)==5      # ✓ Correct
    assert add(-1,1)==0     # ✓ Correct
    assert add(5,5)==11     # ✗ WRONG! Should be 10
```

**OR add this to test_sub():**
```python
def test_sub():
    assert sub(5,3)==2      # ✓ Correct
    assert sub(4,3)==1      # ✓ Correct
    assert sub(3,3)==0      # ✓ Correct
    assert sub(2,3)==-1     # ✓ Correct
    assert sub(10,5)==4     # ✗ WRONG! Should be 5
```

**Run tests to see failing pipeline:**
```bash
pytest tests/
```

Expected output: **Test failed** ❌

The CI/CD pipeline will fail, preventing buggy code from being deployed!

## 🛠️ Implementation Details

### Math Operations (`src/math_operations.py`)
- `add(a, b)`: Returns the sum of two numbers
- `sub(a, b)`: Returns the difference of two numbers

### Test Cases (`tests/test_operation.py`)
- Tests cover positive numbers, negative numbers, and edge cases
- Uses pytest assertions to verify correct behavior

## 📚Learning Outcomes

By working with this project, you'll understand:

1. ✅ How automated testing catches bugs before deployment
2. ✅ The importance of writing good test cases
3. ✅ How CI/CD pipelines provide fast feedback to developers
4. ✅ Why continuous integration improves code quality
5. ✅ The difference between passing and failing builds

## 🔗 Setting Up CI/CD Pipeline

To set up a CI/CD pipeline for this project, you can use:

### GitHub Actions (`.github/workflows/ci.yml`)
```yaml
name: CI Pipeline

on: [push, pull_request]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - name: Set up Python
        uses: actions/setup-python@v2
        with:
          python-version: '3.x'
      - name: Install dependencies
        run: pip install -r requirements.txt
      - name: Run tests
        run: pytest tests/
```

##  Try It Yourself!

1. Clone this repository
2. Run tests with correct assertions → See ✅ **PASS**
3. Modify a test case to be incorrect → See ❌ **FAIL**
4. Fix the test case → See ✅ **PASS** again

This demonstrates the core principle of CI/CD: **Automated quality checks that run on every code change!**