``autosummary`` 작동 테스트
===================================

본인이 만든 패키지 이름이 ``my_package`` 인 경우
``doc/api.rst`` 에 다음과 같이 작성합니다.

.. code-block:: rst
    :linenos:

    :orphan:

    .. autosummary::
        :toctree: _autosummary
        :template: module.rst
        :recursive:

        my_package


* line ``1`` : ``autosummary`` 를 작동하는 directive 입니다.
* 
    line ``2`` : 작동하여 생성된 모듈 요약 ``rst`` 파일들을 저장하는 경로입니다. 
    ``autodoc`` 을 사용하여 생성된 것과 유사하지만 지정한 ``template`` 의 형태로
    생성됩니다.

*
    line ``3`` : 사용자 지정 template를 지정합니다. 확장자를 같이 사용해야 하며
    절대 경로가 아닌 이유는 ``_templates`` 폴더를 기본으로 설정하여 그 폴더 안에
    있다면 따로 부모경로를 지정하지 않아도 됩니다.

*
    line ``4`` : 주어진 패키지 경로를 재귀적으로 탐색하여 전부 생성합니다. 이 기능
    덕분에 사용자는 모듈을 일일이 작성할 필요 없이 자동으로 생성할 수 있습니다.


컨텐트는 패키지의 경로입니다 (``my_package``). 인식이 잘 되지 않는다면 ``conf.py``
의 옵션의 문제일 가능성이 큽니다.

``api.rst`` 파일은 문서 내부에서 인용되지 않습니다. 단지 ``_autosummary`` 에 
패키지 요약 문서를 생성하기 위하여 작성된 문서입니다. 따라서 ``:orphan:`` 이 문서
맨 위에 사용됩니다.


그 다음 ``_autosummary/my_package`` 를 원하는 방식으로 사용하면 됩니다. 다음은 한
예시입니다.

In ``index.rst`` :

.. code-block:: rst

    ``autosummary`` 를 활용한 문서 작성
    =====================================

    이 문서는 ``my_package`` 패키지의 API reference만을 포함한 문서입니다.

    .. toctree:: 

        API Reference <_autosummary/my_package>