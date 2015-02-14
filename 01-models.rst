Escrevendo sua primeira aplicação Django, parte 1
=================================================

Vamos aprender com o exemplo.

Ao longo deste tutorial, vamos levá-lo através da criação de uma aplicação básica de enquetes.

Esta consistirá de duas partes:

* Um site público que permite que as pessoas vejam as enquetes e votem nelas.
* Uma parte administrativa que permita que você adicione, mude ou delete enquetes.

Nós assumiremos que você já tem o `Django <https://docs.djangoproject.com/en/1.7/intro/install/>`_ instalado. Você pode dizer que o Django está instalado e qual versão ao rodar o seguinte comando:

.. code-block:: bash

    $ python -c "import django; print(django.get_version())"

Se o Django estiver instalado, você deverá ver a versão da sua instalação. Se não estiver, você terá uma mensagem de erro dizendo "No module named django".

Este tutorial está escrito para o Django 1.7 e Python 3.2 ou posterior. Se a versão do Django não corresponder, você pode consultar o tutorial para a sua versão do Django, ao usar o trocador de versão no canto inferior direito desta página, ou atualizar o Django para a versão mais nova. Se você ainda estiver usando Python 2.7, você precisará ajustar ligeiramente os exemplos de código, bem como descrito nos comentários.

Veja `como instalar o Django <https://docs.djangoproject.com/en/1.7/topics/install/>`_ para conselhos sobre como remover versões antigas do Django e instalar uma nova.

.. admonition:: **Onde conseguir ajuda**

    Se você está tendo problemas através deste tutorial, por favor poste uma mensagem no `django-users <https://docs.djangoproject.com/en/1.7/internals/mailing-lists/#django-users-mailing-list>`_ ou entre no `#django on irc.freenode.net <irc://irc.freenode.net/django>`_ para falar com outros usuários Django que podem ser capazes de lhe ajudar.

Criando um projeto
------------------
Se esta é sua primeira vez usando Django, você terá que cuidar de algumas configurações iniciais. Ou seja, você vai precisar disso para auto-gerar um código que estabelece um projeto Django - um conjunto de configurações para uma instância do Django, incluindo configuração do banco de dados, opções específicas do Django e configurações específicas da aplicação.

A partir da linha de comando, ``cd`` no diretório onde você gostaria de guardar seu código, e então rode o seguinte comando:

.. code-block:: bash

    $ django-admin.py startproject mysite

Isto criará um diretório chamado *mysite* no seu diretório atual. Se isto não funcionar, veja `Problemas rodando django-admin.py <https://docs.djangoproject.com/en/1.7/faq/troubleshooting/#troubleshooting-django-admin-py>`_.

.. note::
    
    Você precisará evitar dar aos seus projetos nomes de componentes internos do Python e Django. Em particular, iso quer dizer que você deve evitar usar nomes com **django** (que irá conflitar com o Django em si) ou **test** (que conflita com pacotes internos do Python).

.. admonition:: Onde este código deve ficar?

    Se você tem experiência prévia com o velho PHP (sem utilização de frameworks modernos), você provavelmente está acostumado a colocar seu código dentro da pasta raiz do servidor web (como por exemplo, ``/var/www``). Com Django, você não precisa fazer isso. Não é uma boa ideia colocar qualquer código Python dentro da pasta raiz do seu servidor web, porque há o risco da possibilidade que as pessoas possam ver seu código através da web. Isso não é bom para segurança.

    Ponha seu código em algum diretório **fora** da sua pasta raiz, como em ``/home/mycode``.

Vamos olhar para o que o `startproject` criou::
    
    mysite/
        manage.py
        mysite/
            __init__.py
            settings.py
            urls.py
            wsgi.py

.. admonition:: Não bate com o que você está vendo?

    O layout padrão do projeto mudou recentemente. Se você está vendo um layout "flat" (sem um diretório interior *mysite/*), você provavelmente está usando uma versão do Django que não bate com a deste tutorial. Você terá que mudar para o tutorial dessa versão antiga, ou atualizar para a versão mais nova do Django.


Esses arquivos são:

* O diretório exterior raiz *mysite/* é apenas um container para o seu projeto. Seu nome não importa para o Django; você pode renomea-lo para qualquer coisa que você queira.

* **manage.py**: Um utilitário da linha de comando que permite você interagir com este projeto Django em várias maneiras. Você pode ler todos os detalhes sobre o **manage.py** em `django-admin.py e manage.py <https://docs.djangoproject.com/en/1.7/ref/django-admin/>`_.

* O diretório interno *mysyte/* é o atual pacote Python para o seu projeto. Seu nome é o nome do pacote Python que você precisará usar para importar qualquer coisa de dentro dele (por exemplo, **mysite.urls**).

* **mysite/__init__.py**: Um arquivo vazio que fala para o Python que esse diretório deve ser considerado um pacote Python. (Leia `mais sobre pacotes <http://docs.python.org/tutorial/modules.html#packages>`_ no site da documentação oficial do Python, se você for iniciante em Python).

* **mysite/settings.py**: Definições/Configurações para este projeto Django. `Django settings <https://docs.djangoproject.com/en/1.7/topics/settings/>`_ falará para você tudo sobre como o settins funciona.

* **mysite/urls.py**: As declarações das URLs para esse projeto Django; uma "tabela de conteúdos" do seu site feito com Django. Você pode ler mais sobre URLs em `URL dispatcher <https://docs.djangoproject.com/en/1.7/topics/http/urls/>`_

* **mysite/wsgi.py**: Um ponto de entrada para servidores web compatíveis com WSGI. Veja `Como fazer deploy com WSGI <https://docs.djangoproject.com/en/1.7/howto/deployment/wsgi/>`_.