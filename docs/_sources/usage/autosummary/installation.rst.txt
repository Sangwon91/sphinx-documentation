``sphinx.ext.autosummary`` 환경 설정
=============================================

``doc/conf.py`` 를 다음과 같이 수정합니다. ``autodoc`` 환경 설정 방법과
매우 유사합니다.

.. code-block:: 
    :linenos:
    :emphasize-lines: 5, 8, 11-13, 16, 17, 19

    import os
    import sys

    # Python 라이브러리의 위치를 인식하기 위하여.
    sys.path.insert(0, os.path.abspath('../..'))

    # __init__(self) 넣기 위해서.
    autoclass_content = 'both'

    extensions = [
        'sphinx.ext.autodoc',
        'sphinx.ext.napoleon',
        'sphinx.ext.autosummary',
    ]

    autosummary_generate = True
    add_module_names = False

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
      :inherited-members:
      :special-members: __call__, __add__, __mul__

      {% block methods %}
      {% if methods %}
      .. rubric:: {{ _('Methods') }}

      .. autosummary::
         :nosignatures:
      {% for item in methods %}
         {%- if not item.startswith('_') %}
         ~{{ name }}.{{ item }}
         {%- endif -%}
      {%- endfor %}
      {% endif %}
      {% endblock %}

      {% block attributes %}
      {% if attributes %}
      .. rubric:: {{ _('Attributes') }}

      .. autosummary::
      {% for item in attributes %}
         ~{{ name }}.{{ item }}
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