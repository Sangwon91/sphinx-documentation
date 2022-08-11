========================
문서 계층 구조 구성하기
========================

Sphinx 문서화가 마크다운 보다 나은 점은 계층적으로 문서를 작성할 수 있다는 것입니다.
:math:`\LaTeX` 를 사용하셨던 분들은 유사한 시스템을 가졌다고 생각하실 수 있습니다.

계층화의 가장 중요한 요소는 ``toctree``
(Table of Contents Tree)입니다. 계층화 구조는 다음과 같이 만들 수 있습니다.

.. code-block:: rst

    .. toctree::
        :maxdepth: 1
        :caption: Contents

        path/to/other_rst_file_stem_1
        path/to/other_rst_file_stem_2

``:maxdepth:`` 는 트리의 깊이를 얼마나 보여줄지를 나타냅니다. 예를 들어 같은 폴더에
``document1.rst`` , ``document2.rst`` 가 존재하며 각 문서의 내용은 다음과 같다고
하겠습니다.

``document1.rst`` ::

    ============
    My Concent 1
    ============

    Section
    -------

``document2.rst`` ::

    ============
    My Concent 2
    ============

이때 다음과 같이 코드를 작성하면

.. code-block:: rst

    .. toctree::
        :maxdepth: 1
        :caption: Contents

        document1
        document2

다음과 같은 페이지가 생성됩니다.

.. image:: _static/hier.png
    :scale: 60 %
    :align: center

|

``toctree`` directive는 파일 시스템 상의 위치를 강제하지는 않지만
더 나은 관리를 위하여  다음과 같이 ``toctree`` 상의 위치와 일치시키는 것이 좋습니다.

::

    source
    ├── index.rst
    └── my_contents
        ├── document1.rst
        └── document2.rst

그리고 코드는 다음과 같이 변경하면 됩니다.

.. code-block:: rst

    .. toctree::
        :maxdepth: 1
        :caption: Contents

        my_contents/document1
        my_contents/document2
