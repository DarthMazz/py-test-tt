# py-test-tt

 py-test のチュートリアル

## テスト実行指定

### テストメソッドを１つだけ
```bash
pytest tests/test_module.py::TestClass::test_method
```

### クラス内の全てのメソッド
```bash
pytest tests/test_module.py::TestClass
```

### テスト関数を１つだけ
```bash
pytest tests/test_module.py::test_function
```

### モジュール内の全てのテスト
```bash
pytest tests/test_module.py
```

### ディレクトリ内の全てのテスト
```bash
pytest tests
```

### パターンとマッチする名前のテスト
```bash
$ pytest -v -k raises
======================= test session starts ========================
platform linux -- Python 3.12.5, pytest-8.3.3, pluggy-1.5.0 -- /home/ma2moto/_garage/py-test-tt/.venv/bin/python3
cachedir: .pytest_cache
rootdir: /home/ma2moto/_garage/py-test-tt
configfile: pyproject.toml
collected 14 items / 11 deselected / 3 selected

tests/test_2nd_4_exceptions.py::test_no_path_raises PASSED   [ 33%]
tests/test_2nd_4_exceptions.py::test_raises_with_info PASSED [ 66%]
tests/test_2nd_4_exceptions.py::test_raises_with_info_alt PASSED [100%]

================= 3 passed, 11 deselected in 0.04s =================
```
```bash
$ pytest -v --tb=no -k "(dict or ids) and not raises"
======================= test session starts ========================
platform linux -- Python 3.12.5, pytest-8.3.3, pluggy-1.5.0 -- /home/ma2moto/_garage/py-test-tt/.venv/bin/python3
cachedir: .pytest_cache
rootdir: /home/ma2moto/_garage/py-test-tt
configfile: pyproject.toml
collected 14 items / 11 deselected / 3 selected

tests/test_2nd_1_card.py::test_equality_with_diff_ids PASSED [ 33%]
tests/test_2nd_1_card.py::test_from_dict PASSED              [ 66%]
tests/test_2nd_1_card.py::test_to_dict PASSED                [100%]

================= 3 passed, 11 deselected in 0.07s =================
```


## テストオプション

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
### 成功-詳細出力
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
$ pytest -v ./tests/test_1st_2_failing.py
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

### 失敗-さらに詳細表示
```bash
$ pytest -vv tests/test_2nd_2_fail.py
======================= test session starts ========================
platform linux -- Python 3.12.5, pytest-8.3.3, pluggy-1.5.0 -- /home/ma2moto/_garage/py-test-tt/.venv/bin/python3
cachedir: .pytest_cache
rootdir: /home/ma2moto/_garage/py-test-tt
configfile: pyproject.toml
collected 1 item

tests/test_2nd_2_fail.py::test_equality_fail FAILED          [100%]

============================= FAILURES =============================
________________________ test_equality_fail ________________________

    def test_equality_fail():
        c1 = Card("sit there", "brian")
        c2 = Card("do something", "okken")
>       assert c1 == c2
E       AssertionError: assert Card(summary='sit there', owner='brian', state='todo', id=None) == Card(summary='do something', owner='okken', state='todo', id=None)
E
E         Matching attributes:
E         ['state']
E         Differing attributes:
E         ['summary', 'owner']
E
E         Drill down into differing attribute summary:
E           summary: 'sit there' != 'do something'
E           - do something
E           + sit there
E
E         Drill down into differing attribute owner:
E           owner: 'brian' != 'okken'
E           - okken
E           + brian

tests/test_2nd_2_fail.py:7: AssertionError
===================== short test summary info ======================
FAILED tests/test_2nd_2_fail.py::test_equality_fail - AssertionError: assert Card(summary='sit there', owner='brian', state='todo', id=None) == Card(summary='do something', owner='okken', state='todo', id=None)

  Matching attributes:
  ['state']
  Differing attributes:
  ['summary', 'owner']

  Drill down into differing attribute summary:
    summary: 'sit there' != 'do something'
    - do something
    + sit there

  Drill down into differing attribute owner:
    owner: 'brian' != 'okken'
    - okken
    + brian
======================== 1 failed in 0.07s =========================
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

### トレースバックショート
```bash
$ pytest --tb=short tests/test_2nd_3_experiment.py
======================= test session starts ========================
platform linux -- Python 3.12.5, pytest-8.3.3, pluggy-1.5.0
rootdir: /home/ma2moto/_garage/py-test-tt
configfile: pyproject.toml
collected 1 item

tests/test_2nd_3_experiment.py F                             [100%]

============================= FAILURES =============================
________________________ test_no_path_fail _________________________
tests/test_2nd_3_experiment.py:5: in test_no_path_fail
    cards.CardsDB()
E   TypeError: CardsDB.__init__() missing 1 required positional argument: 'db_path'
===================== short test summary info ======================
FAILED tests/test_2nd_3_experiment.py::test_no_path_fail - TypeError: CardsDB.__init__() missing 1 required positional arg...
======================== 1 failed in 0.11s =========================
```

