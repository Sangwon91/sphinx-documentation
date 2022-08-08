확장 기능 사용법
==========================

Sphinx는 다양한 확장 기능을 제공합니다. 모든 확장 기능에 대한 문서는 `이곳 <https://www.sphinx-doc.org/en/master/usage/extensions/index.html>`_ 
을 참고하세요.

1. Jupyter Notebook 확장
-----------------------------------

``nbsphinx`` 와 ``ipykernel`` 을 설치합니다.
::

    pip install nbsphinx ipykernel

``conf.py`` 에 ``nbsphinx`` 를 추가합니다.
::

    extensions = [
        'nbsphinx',
    ]

그럼 ``*.ipynb`` 확장자를 ``*.rst`` 파일처럼 문서에 임포트할 수 있습니다.

예시 (``my_notebook_stem.ipynb`` 파일 사용):

.. code-block:: rst

    .. In index.rst

    .. toctree:: 
        my_notebook_stem


.. admonition:: ``ipykernel`` 을 설치하는 이유

    ``nbsphinx`` 자체에는 파이썬 구문의 syntax highlight 기능이 없습니다.
    ``ipykernel`` 이 있어야만 생성된 ``*.ipynb`` 문서의 syntax 
    highlight기능이 활성화 됩니다.


2. Markdown 확장
-----------------------------------

``myst-parser`` 를 설치합니다.
::

    pip install myst-parser

``conf.py`` 에 ``myst-parser`` 를 추가합니다.
::

    extensions = [
        'myst_parser',
    ]

그럼 ``*.md`` 확장자를 ``*.rst`` 파일처럼 문서에 임포트할 수 있습니다.

예시 (``my_markdown_stem.md`` 파일 사용):

.. code-block:: rst

    .. In index.rst

    .. toctree:: 
        my_markdown_stem