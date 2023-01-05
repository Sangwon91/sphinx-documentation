``sphinx.ext.autosummary`` 환경 설정
=============================================

``doc/conf.py`` 를 다음과 같이 수정합니다. ``autodoc`` 환경 설정 방법과
매우 유사합니다.

.. code-block::
    :linenos:

    import os
    import sys

    # Python 라이브러리의 위치를 인식하기 위하여.
    sys.path.insert(0, os.path.abspath('../..'))

    extensions = [
        'sphinx.ext.autodoc',
        'sphinx.ext.napoleon',
        'sphinx.ext.autosummary',
    ]

    # 디폴트도 True라서 안 해도 됨.
    autosummary_generate = True
    # 클레스에서 모듈 경로 삭제.
    add_module_names = False
    # __init__(self) 넣기 위해서.
    autoclass_content = 'both'
    autodoc_inherit_docstrings = False

    templates_path = ['_templates']

그 다음 ``doc/source/_templates`` 폴더에 다음과 같은 두 파일을 추가합니다.
(아래 template는 `이곳 <https://github.com/JamesALeedham/Sphinx-Autosummary-Recursion>`_
에서 참고/수정 하였습니다.)

``base.rst`` :

.. code-block:: rst

    {{ name | escape | underline }}

    .. currentmodule:: {{ module }}

    .. auto{{ objtype }}:: {{ objname }}



``class.rst`` :

.. code-block:: rst

   {{ name | escape | underline }}

   .. currentmodule:: {{ module }}

   .. autoclass:: {{ objname }}
      :members:
      :show-inheritance:
      :special-members: __call__, __add__, __mul__

      {% block methods %}
      {% if methods %}
      .. rubric:: {{ _('Methods') }}

      .. autosummary::
         :nosignatures:
      {% for item in methods %}
      {%- if item not in inherited_members %}
         {%- if not item.startswith('_') %}
         ~{{ name }}.{{ item }}
         {%- endif -%}
      {%- endif -%}
      {%- endfor %}
      {% endif %}
      {% endblock %}

      {% block attributes %}
      {% if attributes %}
      .. rubric:: {{ _('Attributes') }}

      .. autosummary::
      {% for item in attributes %}
      {%- if item not in inherited_members %}
         ~{{ name }}.{{ item }}
      {%- endif -%}
      {%- endfor %}
      {% endif %}
      {% endblock %}


``module.rst`` :

.. code-block:: rst

   {{ name | escape | underline }}

   .. automodule:: {{ fullname }}

      {% block attributes %}
      {% if attributes %}
      .. rubric:: Module attributes

      .. autosummary::
         :toctree:
         :template: base.rst
         :nosignatures:
      {% for item in attributes %}
         {{ item }}
      {%- endfor %}
      {% endif %}
      {% endblock %}

      {% block functions %}
      {% if functions %}
      .. rubric:: {{ _('Functions') }}

      .. autosummary::
         :toctree:
         :template: base.rst
         :nosignatures:
      {% for item in functions %}
         {{ item }}
      {%- endfor %}
      {% endif %}
      {% endblock %}

      {% block classes %}
      {% if classes %}
      .. rubric:: {{ _('Classes') }}

      .. autosummary::
         :toctree:
         :template: class.rst
         :nosignatures:
      {% for item in classes %}
         {{ item }}
      {%- endfor %}
      {% endif %}
      {% endblock %}

      {% block exceptions %}
      {% if exceptions %}
      .. rubric:: {{ _('Exceptions') }}

      .. autosummary::
         :toctree:
         :template: base.rst
         :nosignatures:
      {% for item in exceptions %}
         {{ item }}
      {%- endfor %}
      {% endif %}
      {% endblock %}

   {% block modules %}
   {% if modules %}
   .. autosummary::
      :toctree:
      :template: module.rst
      :recursive:
   {% for item in modules %}
      ~{{ item }}
   {%- endfor %}
   {% endif %}
   {% endblock %}


이 템플레이트에 맞춰 요약 문서가 생성되게 됩니다.

.. note::
   템플레이트에서 사용된 문법은 Jinja입니다. 이 문법은 Flask에서도 사용됩니다.

.. note::
   Directive ``.. rubic:: 내 타이틀`` 의 아웃풋은 다음과 같습니다.

      .. rubric:: 내 타이틀

지금 설정의 경우 부모 클레스의 정보는 포함하지 않도록 했습니다.
템플레이트에 사용할 수 있는 변수명의 경우 `여기 <https://www.sphinx-doc.org/en/master/usage/extensions/autosummary.html>`_
에서 확인할 수 있습니다.
