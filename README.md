# py-test-tt

 py-test のチュートリアル

## 1st

### 成功-オプションなし
```bash
$ pytest ./tests/test_1st_1_passing.py
======================== test session starts =========================
platform linux -- Python 3.12.5, pytest-8.3.3, pluggy-1.5.0
rootdir: /home/ma2moto/_garage/py-test-tt
configfile: pyproject.toml
collected 1 item

tests/test_1st_1_passing.py .                                  [100%]

========================= 1 passed in 0.01s ==========================
```
### 成功-詳細出力-モジュール指定
```bash
$ pytest -v ./tests/test_1st_1_passing.py
======================== test session starts =========================
platform linux -- Python 3.12.5, pytest-8.3.3, pluggy-1.5.0 -- /home/ma2moto/_garage/py-test-tt/.venv/bin/python3
cachedir: .pytest_cache
rootdir: /home/ma2moto/_garage/py-test-tt
configfile: pyproject.toml
collected 1 item

tests/test_1st_1_passing.py::test_passing PASSED               [100%]

========================= 1 passed in 0.00s ==========================
```

### 失敗-オプションなし
```bash
$ pytest ./tests/test_1st_2_failing.py
======================== test session starts =========================
platform linux -- Python 3.12.5, pytest-8.3.3, pluggy-1.5.0
rootdir: /home/ma2moto/_garage/py-test-tt
configfile: pyproject.toml
collected 1 item

tests/test_1st_2_failing.py F                                  [100%]

============================== FAILURES ==============================
____________________________ test_failing ____________________________

    def test_failing():
>       assert (1, 2, 3) == (3, 2, 1)
E       assert (1, 2, 3) == (3, 2, 1)
E
E         At index 0 diff: 1 != 3
E         Use -v to get more diff

tests/test_1st_2_failing.py:2: AssertionError
====================== short test summary info =======================
FAILED tests/test_1st_2_failing.py::test_failing - assert (1, 2, 3) == (3, 2, 1)
========================= 1 failed in 0.02s ==========================
```

### 失敗-詳細表示
```bash
$ pytest -v .
/tests/test_1st_2_failing.py
======================== test session starts =========================
platform linux -- Python 3.12.5, pytest-8.3.3, pluggy-1.5.0 -- /home/ma2moto/_garage/py-test-tt/.venv/bin/python3
cachedir: .pytest_cache
rootdir: /home/ma2moto/_garage/py-test-tt
configfile: pyproject.toml
collected 1 item

tests/test_1st_2_failing.py::test_failing FAILED               [100%]

============================== FAILURES ==============================
____________________________ test_failing ____________________________

    def test_failing():
>       assert (1, 2, 3) == (3, 2, 1)
E       AssertionError: assert (1, 2, 3) == (3, 2, 1)
E
E         At index 0 diff: 1 != 3
E
E         Full diff:
E           (
E         +     1,
E         +     2,...
E
E         ...Full output truncated (4 lines hidden), use '-vv' to show

tests/test_1st_2_failing.py:2: AssertionError
====================== short test summary info =======================
FAILED tests/test_1st_2_failing.py::test_failing - AssertionError: assert (1, 2, 3) == (3, 2, 1)
========================= 1 failed in 0.02s ==========================
```

### 全テスト実行-トレースバックなし
```bash
pytest --tb=no
======================== test session starts =========================
platform linux -- Python 3.12.5, pytest-8.3.3, pluggy-1.5.0
rootdir: /home/ma2moto/_garage/py-test-tt
configfile: pyproject.toml
collected 2 items

tests/test_1st_1_passing.py .                                  [ 50%]
tests/test_1st_2_failing.py F                                  [100%]

====================== short test summary info =======================
FAILED tests/test_1st_2_failing.py::test_failing - assert (1, 2, 3) == (3, 2, 1)
==================== 1 failed, 1 passed in 0.01s =====================
```

### テストメソッド指定-詳細表示
```bash
$ pytest -v ./tests/test_1st_1_passing.py::test_passing
======================== test session starts =========================
platform linux -- Python 3.12.5, pytest-8.3.3, pluggy-1.5.0 -- /home/ma2moto/_garage/py-test-tt/.venv/bin/python3
cachedir: .pytest_cache
rootdir: /home/ma2moto/_garage/py-test-tt
configfile: pyproject.toml
collected 1 item

tests/test_1st_1_passing.py::test_passing PASSED               [100%]

========================= 1 passed in 0.01s ==========================
```