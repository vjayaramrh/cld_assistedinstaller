# Testing Approach

This document explains our testing strategy based on 2026 Ansible best practices.

## Testing Tools We Use

### pytest (Test Framework)
**Why:** Industry standard, easy to learn, powerful features
**Docs:** https://docs.pytest.org/en/stable/

### pytest-mock (Mocking)
**Why:** Cleaner syntax than unittest.mock, beginner-friendly
**Docs:** https://pytest-mock.readthedocs.io/en/latest/

### ansible-test (Sanity Tests)
**Why:** Ansible's official testing tool for code quality
**Docs:** https://docs.ansible.com/ansible/latest/dev_guide/developing_collections_testing.html

## Test Types

### Unit Tests
**What:** Test individual module functions in isolation
**Location:** `tests/unit/`
**Tools:** pytest + pytest-mock

**Benefits:**
- Fast to run
- No external dependencies
- Easy to debug
- Good for beginners

### Sanity Tests
**What:** Automated code quality checks
**Tools:** ansible-test sanity

**Checks:**
- Python syntax
- Import errors
- Documentation format
- Code style (PEP 8)

## Modern Testing Pattern

### Use This (Modern):
```python
import pytest

def test_list_events(mocker):
    """Test listing all events."""
    mock_get = mocker.patch('requests.get')
    mock_get.return_value.ok = True
    mock_get.return_value.json.return_value = []

    assert mock_get.called
```

### Don't Use (Old):
```python
import unittest
from unittest.mock import patch

class TestEvents(unittest.TestCase):
    @patch('requests.get')
    def test_list_events(self, mock_get):
        # Old style - verbose
        pass
```

## What We Mock

**External Dependencies:**
- API calls (requests.get, requests.post)
- Environment variables
- AnsibleModule

**Don't Mock:**
- Our own module logic (that's what we're testing!)
- Module utilities (unless testing in isolation)

## Test Coverage Goals

**For beginners, focus on:**
- ✅ Happy path (everything works)
- ✅ Common errors (401, 404, 500)
- ✅ Parameter validation
- ✅ Edge cases

**Good coverage: 70-80%**

## Running Tests

```bash
# Run all tests
./tests/run_tests.sh

# Run specific test
pytest tests/unit/test_events.py::test_list_events -v

# With coverage
pytest --cov=plugins/modules --cov-report=html
```

## Benefits

**For Beginners:**
- Modern, widely-used tools
- Clean, readable test code
- Skills transfer to other Python projects

**For Project:**
- Official Ansible recommendations
- Future-proof (current standards)
- Easy to extend

## References

### Official Docs
- [Testing collections](https://docs.ansible.com/ansible/latest/dev_guide/developing_collections_testing.html)
- [Unit testing modules](https://docs.ansible.com/ansible/latest/dev_guide/testing_units_modules.html)
- [pytest](https://docs.pytest.org/en/stable/)
- [pytest-mock](https://pytest-mock.readthedocs.io/en/latest/)

### Tutorials
- [Capital One: Unit Testing Ansible](https://www.capitalone.com/tech/cloud/python-ansible-aws-unit-testing-ansible-modules/)

This ensures you're learning the right way to test Ansible modules!
