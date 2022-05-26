===========
Sphinx 설치
===========

Sphinx를 윈도우에서 원활하게 사용하기 위해서는 시스템의 파이썬을 
사용하는 것을 가정합니다.
따라서 `파이썬을 다운로드 <https://www.python.org/downloads/>`_ 합니다. 

.. warning::
  
    파이썬이 설치된 뒤 파이썬과 **파이썬 스크립트 폴더** 경로가 환경변수 ``PATH`` 에 등록되었는지 확인해야 합니다.
    파이썬 스크립트 폴더는 라이브러리 설치시 제공되는 스크립트들이 저장되는 폴더입니다.
    Sphinx는 ``sphinx-quickstart`` 등의 스크립트를 사용하기 때문에 환경변수에 등록되어야 합니다.
    



.. code-block::

    pip install sphinx sphinx_rtd_theme 
    pip ipython nbsphinx