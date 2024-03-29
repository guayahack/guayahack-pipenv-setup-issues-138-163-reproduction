
# guayahack-pipenv-setup-issues-138-163-reproduction

This repository enables the reliable reproduction of both Madoshakalaka/pipenv-setup#138 and Madoshakalaka/pipenv-setup#163

## Running


```
$ git clone git@github.com:guayahack/guayahack-pipenv-setup-issues-138-163-reproduction.git

$ cd guayahack-pipenv-setup-issues-138-163-reproduction
```

The structure is as follows:

```
.
├── README.md
├── pipenv_setup_issues_138_reproduction
│   ├── AUTHORS.rst
│   ├── CHANGELOG.rst
│   ├── LICENSE.txt
│   ├── Pipfile
│   ├── Pipfile.lock
│   ├── pyproject.toml
│   ├── requirements.txt
│   ├── setup.cfg
│   ├── setup.py
│   ├── src
│   ├── tests
│   └── tox.ini
│
└── pipenv_setup_issues_163_reproduction
    ├── AUTHORS.rst
    ├── CHANGELOG.rst
    ├── LICENSE.txt
    ├── Pipfile
    ├── Pipfile.lock
    ├── pyproject.toml
    ├── requirements.txt
    ├── setup.cfg
    ├── setup.py
    ├── src
    ├── tests
    ├── tox.ini
    └── trigger.py
```

### Issue 138

Bug 138 can be triggered as follows:

```
$ pipenv run pipenv-setup -h

Traceback (most recent call last):
  File "/Users/User/.local/share/virtualenvs/pipenv_setup_issues_138_reproduction-N1WvMmis/bin/pipenv-setup", line 5, in <module>
    from pipenv_setup.main import cmd
  File "/Users/User/.local/share/virtualenvs/pipenv_setup_issues_138_reproduction-N1WvMmis/lib/python3.11/site-packages/pipenv_setup/main.py", line 19, in <module>
    from vistir.compat import Path
ModuleNotFoundError: No module named 'vistir.compat'
```

Or alternatively, here it is using Tox :

```
cd pipenv_setup_issues_138_reproduction
pipenv install
pipenv run tox -e trigger
```

```
$ tox
.pkg: _optional_hooks> python /Users/User/.asdf/installs/python/3.11.0/lib/python3.11/site-packages/pyproject_api/_backend.py True setuptools.build_meta
.pkg: get_requires_for_build_sdist> python /Users/User/.asdf/installs/python/3.11.0/lib/python3.11/site-packages/pyproject_api/_backend.py True setuptools.build_meta
.pkg: get_requires_for_build_wheel> python /Users/User/.asdf/installs/python/3.11.0/lib/python3.11/site-packages/pyproject_api/_backend.py True setuptools.build_meta
.pkg: prepare_metadata_for_build_wheel> python /Users/User/.asdf/installs/python/3.11.0/lib/python3.11/site-packages/pyproject_api/_backend.py True setuptools.build_meta
.pkg: build_sdist> python /Users/User/.asdf/installs/python/3.11.0/lib/python3.11/site-packages/pyproject_api/_backend.py True setuptools.build_meta

default: install_package> python -I -m pip install --force-reinstall --no-deps /Users/User/ghpr/guayahack-pipenv-setup-issues-138-163-reproduction/pipenv_setup_issues_138_reproduction/.tox/.tmp/package/30/pipenv_setup_issues_138_reproduction-0.0.0.tar.gz
default: commands[0]> pytest
=========================================================================================================== test session starts ============================================================================================================
platform darwin -- Python 3.11.0, pytest-8.0.2, pluggy-1.4.0 -- /Users/User/ghpr/guayahack-pipenv-setup-issues-138-163-reproduction/pipenv_setup_issues_138_reproduction/.tox/default/bin/python
cachedir: .tox/default/.pytest_cache
rootdir: /Users/User/ghpr/guayahack-pipenv-setup-issues-138-163-reproduction/pipenv_setup_issues_138_reproduction
configfile: setup.cfg
testpaths: tests
plugins: cov-4.1.0
collected 0 items / 1 error

================================================================================================================== ERRORS ==================================================================================================================
___________________________________________________________________________________________________ ERROR collecting tests/test_main.py ____________________________________________________________________________________________________
ImportError while importing test module '/Users/User/ghpr/guayahack-pipenv-setup-issues-138-163-reproduction/pipenv_setup_issues_138_reproduction/tests/test_main.py'.
Hint: make sure your test modules/packages have valid Python names.
Traceback:
../../../.asdf/installs/python/3.11.0/lib/python3.11/importlib/__init__.py:126: in import_module
    return _bootstrap._gcd_import(name[level:], package, level)
tests/test_main.py:3: in <module>
    from pipenv_setup_issues_138_reproduction.main import fib, main
.tox/default/lib/python3.11/site-packages/pipenv_setup_issues_138_reproduction/__init__.py:26: in <module>
    from pipenv_setup import pipfile_parser as parser
.tox/default/lib/python3.11/site-packages/pipenv_setup/pipfile_parser.py:4: in <module>
    from requirementslib import Requirement
.tox/default/lib/python3.11/site-packages/requirementslib/__init__.py:9: in <module>
    from .models.lockfile import Lockfile
.tox/default/lib/python3.11/site-packages/requirementslib/models/lockfile.py:14: in <module>
    from ..utils import is_editable, is_vcs, merge_items
.tox/default/lib/python3.11/site-packages/requirementslib/utils.py:14: in <module>
    from vistir.compat import fs_decode
E   ModuleNotFoundError: No module named 'vistir.compat'
============================================================================================================= warnings summary =============================================================================================================
.tox/default/lib/python3.11/site-packages/_distutils_hack/__init__.py:26
  /Users/User/ghpr/guayahack-pipenv-setup-issues-138-163-reproduction/pipenv_setup_issues_138_reproduction/.tox/default/lib/python3.11/site-packages/_distutils_hack/__init__.py:26: UserWarning: Setuptools is replacing distutils.
    warnings.warn("Setuptools is replacing distutils.")

-- Docs: https://docs.pytest.org/en/stable/how-to/capture-warnings.html

---------- coverage: platform darwin, python 3.11.0-final-0 ----------
Name                                                   Stmts   Miss Branch BrPart  Cover   Missing
--------------------------------------------------------------------------------------------------
src/pipenv_setup_issues_138_reproduction/__init__.py       7      0      0      0   100%
--------------------------------------------------------------------------------------------------
TOTAL                                                      7      0      0      0   100%

========================================================================================================= short test summary info ==========================================================================================================
ERROR tests/test_main.py
!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!! Interrupted: 1 error during collection !!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
======================================================================================================= 1 warning, 1 error in 0.43s ========================================================================================================
default: exit 2 (0.68 seconds) /Users/User/ghpr/guayahack-pipenv-setup-issues-138-163-reproduction/pipenv_setup_issues_138_reproduction> pytest pid=87243
.pkg: _exit> python /Users/User/.asdf/installs/python/3.11.0/lib/python3.11/site-packages/pyproject_api/_backend.py True setuptools.build_meta
  default: FAIL code 2 (5.16=setup[4.48]+cmd[0.68] seconds)
  evaluation failed :( (5.23 seconds)
```




### Issue 163

Bug 163 can be triggered as follows:

```
cd pipenv_setup_issues_163_reproduction

$ pipenv run python -c 'from pipenv_setup import pipfile_parser as parser'

/Users/User/.local/share/virtualenvs/pipenv_setup_issues_163_reproduction-W1rmhskS/lib/python3.11/site-packages/_distutils_hack/__init__.py:26: UserWarning: Setuptools is replacing distutils.
  warnings.warn("Setuptools is replacing distutils.")
Traceback (most recent call last):
  File "<string>", line 1, in <module>
  File "/Users/User/.local/share/virtualenvs/pipenv_setup_issues_163_reproduction-W1rmhskS/lib/python3.11/site-packages/pipenv_setup/pipfile_parser.py", line 4, in <module>
    from requirementslib import Requirement
  File "/Users/User/.local/share/virtualenvs/pipenv_setup_issues_163_reproduction-W1rmhskS/lib/python3.11/site-packages/requirementslib/__init__.py", line 10, in <module>
    from .models.pipfile import Pipfile
  File "/Users/User/.local/share/virtualenvs/pipenv_setup_issues_163_reproduction-W1rmhskS/lib/python3.11/site-packages/requirementslib/models/pipfile.py", line 11, in <module>
    import plette.models.base
ModuleNotFoundError: No module named 'plette.models.base'; 'plette.models' is not a package
```


Or alternatively, here it is using Tox :

```
cd pipenv_setup_issues_163_reproduction

pipenv install

pipenv run tox -e trigger
```

```
$ tox
.pkg: _optional_hooks> python /Users/User/.asdf/installs/python/3.11.0/lib/python3.11/site-packages/pyproject_api/_backend.py True setuptools.build_meta
.pkg: get_requires_for_build_sdist> python /Users/User/.asdf/installs/python/3.11.0/lib/python3.11/site-packages/pyproject_api/_backend.py True setuptools.build_meta
.pkg: get_requires_for_build_wheel> python /Users/User/.asdf/installs/python/3.11.0/lib/python3.11/site-packages/pyproject_api/_backend.py True setuptools.build_meta
.pkg: prepare_metadata_for_build_wheel> python /Users/User/.asdf/installs/python/3.11.0/lib/python3.11/site-packages/pyproject_api/_backend.py True setuptools.build_meta
.pkg: build_sdist> python /Users/User/.asdf/installs/python/3.11.0/lib/python3.11/site-packages/pyproject_api/_backend.py True setuptools.build_meta
default: install_package> python -I -m pip install --force-reinstall --no-deps /Users/User/ghpr/guayahack-pipenv-setup-issues-138-163-reproduction/pipenv_setup_issues_163_reproduction/.tox/.tmp/package/30/pipenv_setup_issues_138_reproduction-0.0.0.tar.gz
default: commands[0]> pytest
=========================================================================================================== test session starts ============================================================================================================
platform darwin -- Python 3.11.0, pytest-8.0.2, pluggy-1.4.0 -- /Users/User/ghpr/guayahack-pipenv-setup-issues-138-163-reproduction/pipenv_setup_issues_163_reproduction/.tox/default/bin/python
cachedir: .tox/default/.pytest_cache
rootdir: /Users/User/ghpr/guayahack-pipenv-setup-issues-138-163-reproduction/pipenv_setup_issues_163_reproduction
configfile: setup.cfg
testpaths: tests
plugins: cov-4.1.0
collected 0 items / 1 error

================================================================================================================== ERRORS ==================================================================================================================
___________________________________________________________________________________________________ ERROR collecting tests/test_main.py ____________________________________________________________________________________________________
ImportError while importing test module '/Users/User/ghpr/guayahack-pipenv-setup-issues-138-163-reproduction/pipenv_setup_issues_163_reproduction/tests/test_main.py'.
Hint: make sure your test modules/packages have valid Python names.
Traceback:
../../../.asdf/installs/python/3.11.0/lib/python3.11/importlib/__init__.py:126: in import_module
    return _bootstrap._gcd_import(name[level:], package, level)
tests/test_main.py:3: in <module>
    from pipenv_setup_issues_138_reproduction.main import fib, main
.tox/default/lib/python3.11/site-packages/pipenv_setup_issues_138_reproduction/__init__.py:26: in <module>
    from pipenv_setup import pipfile_parser as parser
.tox/default/lib/python3.11/site-packages/pipenv_setup/pipfile_parser.py:4: in <module>
    from requirementslib import Requirement
.tox/default/lib/python3.11/site-packages/requirementslib/__init__.py:10: in <module>
    from .models.pipfile import Pipfile
.tox/default/lib/python3.11/site-packages/requirementslib/models/pipfile.py:11: in <module>
    import plette.models.base
E   ModuleNotFoundError: No module named 'plette.models.base'; 'plette.models' is not a package
============================================================================================================= warnings summary =============================================================================================================
.tox/default/lib/python3.11/site-packages/vistir/misc.py:828
  /Users/User/ghpr/guayahack-pipenv-setup-issues-138-163-reproduction/pipenv_setup_issues_163_reproduction/.tox/default/lib/python3.11/site-packages/vistir/misc.py:828: DeprecationWarning: Use setlocale(), getencoding() and getlocale() instead
    locale_encoding = locale.getdefaultlocale()[1] or "ascii"

.tox/default/lib/python3.11/site-packages/_distutils_hack/__init__.py:26
  /Users/User/ghpr/guayahack-pipenv-setup-issues-138-163-reproduction/pipenv_setup_issues_163_reproduction/.tox/default/lib/python3.11/site-packages/_distutils_hack/__init__.py:26: UserWarning: Setuptools is replacing distutils.
    warnings.warn("Setuptools is replacing distutils.")

.tox/default/lib/python3.11/site-packages/pyparsing.py:108
  /Users/User/ghpr/guayahack-pipenv-setup-issues-138-163-reproduction/pipenv_setup_issues_163_reproduction/.tox/default/lib/python3.11/site-packages/pyparsing.py:108: DeprecationWarning: module 'sre_constants' is deprecated
    import sre_constants

.tox/default/lib/python3.11/site-packages/requirementslib/models/requirements.py:10
  /Users/User/ghpr/guayahack-pipenv-setup-issues-138-163-reproduction/pipenv_setup_issues_163_reproduction/.tox/default/lib/python3.11/site-packages/requirementslib/models/requirements.py:10: DeprecationWarning: The distutils package is deprecated and slated for removal in Python 3.12. Use setuptools or check PEP 632 for potential alternatives
    from distutils.sysconfig import get_python_lib

.tox/default/lib/python3.11/site-packages/requirementslib/models/requirements.py:10
  /Users/User/ghpr/guayahack-pipenv-setup-issues-138-163-reproduction/pipenv_setup_issues_163_reproduction/.tox/default/lib/python3.11/site-packages/requirementslib/models/requirements.py:10: DeprecationWarning: The distutils.sysconfig module is deprecated, use sysconfig instead
    from distutils.sysconfig import get_python_lib

.tox/default/lib/python3.11/site-packages/requirementslib/models/setup_info.py:45
  /Users/User/ghpr/guayahack-pipenv-setup-issues-138-163-reproduction/pipenv_setup_issues_163_reproduction/.tox/default/lib/python3.11/site-packages/requirementslib/models/setup_info.py:45: DeprecationWarning: pkg_resources is deprecated as an API. See https://setuptools.pypa.io/en/latest/pkg_resources.html
    import pkg_resources.extern.packaging.requirements as pkg_resources_requirements

-- Docs: https://docs.pytest.org/en/stable/how-to/capture-warnings.html

---------- coverage: platform darwin, python 3.11.0-final-0 ----------
Name                                                   Stmts   Miss Branch BrPart  Cover   Missing
--------------------------------------------------------------------------------------------------
src/pipenv_setup_issues_138_reproduction/__init__.py       7      0      0      0   100%
--------------------------------------------------------------------------------------------------
TOTAL                                                      7      0      0      0   100%

========================================================================================================= short test summary info ==========================================================================================================
ERROR tests/test_main.py
!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!! Interrupted: 1 error during collection !!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
======================================================================================================= 6 warnings, 1 error in 0.58s =======================================================================================================
default: exit 2 (0.84 seconds) /Users/User/ghpr/guayahack-pipenv-setup-issues-138-163-reproduction/pipenv_setup_issues_163_reproduction> pytest pid=88573
.pkg: _exit> python /Users/User/.asdf/installs/python/3.11.0/lib/python3.11/site-packages/pyproject_api/_backend.py True setuptools.build_meta
  default: FAIL code 2 (5.11=setup[4.28]+cmd[0.84] seconds)
  evaluation failed :( (5.18 seconds)
```

