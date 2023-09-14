**Local install works**

```
$ python -m pip install --upgrade .
Processing /home/feickert/Code/debug/sckit-build-core-example/subdir
  Installing build dependencies ... done
  Getting requirements to build wheel ... done
  Installing backend dependencies ... done
  Preparing metadata (pyproject.toml) ... done
Requirement already satisfied: numpy in /home/feickert/.pyenv/versions/talk-odsl-forum-seminar-2023/lib/python3.11/site-packages (from example-pkg==0.1.dev0) (1.25.2)
Building wheels for collected packages: example-pkg
  Building wheel for example-pkg (pyproject.toml) ... done
  Created wheel for example-pkg: filename=example_pkg-0.1.dev0-cp311-cp311-manylinux_2_35_x86_64.whl size=51989 sha256=d9fd4fe4e71e867f75eeb7aae6b9f1816c070e316fde599e79e756a2fac6d3fb
  Stored in directory: /tmp/pip-ephem-wheel-cache-pdx70379/wheels/68/52/95/2ed862a321a9b5f7a76e23e273f0b64a03d5771eae1e8a411f
Successfully built example-pkg
Installing collected packages: example-pkg
Successfully installed example-pkg-0.1.dev0
$ cat src/example_pkg/_version.py
# file generated by setuptools_scm
# don't change, don't track in version control
__version__ = version = '0.1.dev0'
__version_tuple__ = version_tuple = (0, 1, 'dev0')
```

**Wheel build fails**

```
$ rm -rf src/example_pkr/_version.py && rm -rf dist && python -m build .
* Creating venv isolated environment...
* Installing packages in isolated environment... (pybind11, scikit-build-core)
* Getting build dependencies for sdist...
* Installing packages in isolated environment... (pathspec, pyproject_metadata, setuptools-scm)
* Building sdist...
*** scikit-build-core 0.5.0 (sdist)
* Building wheel from sdist
* Creating venv isolated environment...
* Installing packages in isolated environment... (pybind11, scikit-build-core)
* Getting build dependencies for wheel...
* Installing packages in isolated environment... (pathspec, pyproject_metadata, setuptools-scm)
* Building wheel...
Traceback (most recent call last):
  File "/home/feickert/.pyenv/versions/talk-odsl-forum-seminar-2023/lib/python3.11/site-packages/pyproject_hooks/_in_process/_in_process.py", line 353, in <module>
    main()
  File "/home/feickert/.pyenv/versions/talk-odsl-forum-seminar-2023/lib/python3.11/site-packages/pyproject_hooks/_in_process/_in_process.py", line 335, in main
    json_out['return_val'] = hook(**hook_input['kwargs'])
                             ^^^^^^^^^^^^^^^^^^^^^^^^^^^^
  File "/home/feickert/.pyenv/versions/talk-odsl-forum-seminar-2023/lib/python3.11/site-packages/pyproject_hooks/_in_process/_in_process.py", line 251, in build_wheel
    return _build_backend().build_wheel(wheel_directory, config_settings,
           ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
  File "/tmp/build-env-w_pvzrk7/lib/python3.11/site-packages/scikit_build_core/build/__init__.py", line 32, in build_wheel
    return _build_wheel_impl(
           ^^^^^^^^^^^^^^^^^^
  File "/tmp/build-env-w_pvzrk7/lib/python3.11/site-packages/scikit_build_core/build/wheel.py", line 92, in _build_wheel_impl
    metadata = get_standard_metadata(pyproject, settings)
               ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
  File "/tmp/build-env-w_pvzrk7/lib/python3.11/site-packages/scikit_build_core/settings/metadata.py", line 33, in get_standard_metadata
    new_pyproject_dict["project"][field] = provider.dynamic_metadata(field, config)
                                           ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
  File "/tmp/build-env-w_pvzrk7/lib/python3.11/site-packages/scikit_build_core/metadata/setuptools_scm.py", line 28, in dynamic_metadata
    version: str = _get_version(config)
                   ^^^^^^^^^^^^^^^^^^^^
  File "/tmp/build-env-w_pvzrk7/lib/python3.11/site-packages/setuptools_scm/__init__.py", line 162, in _get_version
    dump_version(
  File "/tmp/build-env-w_pvzrk7/lib/python3.11/site-packages/setuptools_scm/__init__.py", line 77, in dump_version
    with open(target, "w") as fp:
         ^^^^^^^^^^^^^^^^^
FileNotFoundError: [Errno 2] No such file or directory: '../subdir/src/example_pkg/_version.py'

ERROR Backend subprocess exited when trying to invoke build_wheel
```
