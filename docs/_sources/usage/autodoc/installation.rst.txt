``autodoc`` 환경 설정
======================


``doc/conf.py`` 를 다음과 같이 수정합니다. 만약 Sphinx의 ``root`` 경로가 ``doc`` 이 
아니라면 그에 맞게 경로를 수정하면 됩니다.

.. code-block:: 
    :linenos:

    import os
    import sys

    # Python 라이브러리의 위치를 인식하기 위하여.
    sys.path.insert(0, os.path.abspath('../..'))

    # __init__(self) 넣기 위해서.
    autoclass_content = 'both'

    extensions = [ 
        # AutoDoc 기능을 사용하기 위하여.
        'sphinx.ext.autodoc',
        # Numpy style 문서화 스트링을 사용하기 위하여.
        'sphinx.ext.napoleon',
    ]

라인 ``5`` 는 작성한 파이썬 라이브러리의 위치를 인식하기 위함입니다. 파일 시스템이
다음과 같이 구성되었다고 가성하였습니다.

.. │
.. └ 
.. ├
.. ─

::

    project
    ├── doc
    │   └── source
    │       ├── index.rst
    │       └── conf.py
    └── my_package
        └── my_module.py

``conf.py`` 의 위치가 ``doc/source`` 이기 때문에
``../..`` 를 ``path`` 에 추가해야지 ``my_package`` 의 위치를 확인할 수 있습니다.

