========
Django 2
========

.. contents::
   :backlinks: top
   :depth: 3

-----------------------
How Djano is structured
-----------------------

Model, View, Controller (MVC)
==============================

Django is a Model View Controller (MVC) framework.

    :MVC:   MVC is a software design pattern that aims to separate application into three
            interconnected parts :

            #. **Model** : Provides the interface with the database containing the application data.

            #. **View** : Decides what informations to present to the user and collects information 
               from the user.

            #. **Controler** : Manage the business logic for the application and acts as an
               information broker between the model and the view.

Model, Template, View (MTV)
---------------------------

Django's terminology is slightly different than the MVC's :

    #. **Model** :  Is functionnaly the same. Django's Object Relational Mapping (ORM) provides the 
       interface between the user and your Django application.

    #. **Template** : Provide display logic and is the interface between the user and your
       application. It corresponds to the View in the MVC model

    #. **View** : manage the bulk of the applications data processing, application logic and
       messaging. It corresponds to the Controler in the MVC model

    :/!\\ WARNING /!\\:
    
            There is no direct link between the "Model" and the "Template". Only the "View" can
            interracting with the two other.

Models
======

    :Liens_Web:

            * `Django Project TOPICS Models`_ : The models\' topics from the Django documentation

    :ORM:   
    
            Object Relational Mapping : Provide a simple Mapping between an Object and the
            underlying database. The programmer doesn't to know the database structure, nor does it
            require complex SQL to manipulate and retrieve data.


The model is the object that is mapped to the database. When you create a model, Django create a 
corresponding table in database. Each of your app's models are a class that you create in your app's
*models.py* file.

    * Each model is a Python class that is a subclasses of **django.db.models.Model** 

    * Each attribute of the model represent a database field.

The **models.py** file is automaticaly created inside the app's directory, when you are using the 
*startapp* wizard.

Supported databases
-------------------

    :Liens_Web:
            * `Django Project Settings Databases`_ : The databases\' settings from the official 
              documentation.

Django officially supports four databases :

    * PostgreSQL

    * MySQL

    * SQLite

    * Oracle

By default, Django install SQLite automatically when you are using the *stratproject* wizard.

If you need to connect to an unofficially supported database, there are several third-party
application available.

Template
========

    :DTL:   Django Template Language is a plain text scripting language that uses tags to provide 
            presentation logic for deciding what content to display in the template.

A Django template is a text file designed to separate an application's data from the way it is
presented. It is not limited to HTML.

There are three big principles for the Django templates' :

    #. A template system should separate program logic from design.

    #. Templates should discourage redundancy (DRY : Don't Repeat Yourself)

    #. The template system should be safe and secure. Code execution in the template must be 
       forbiden.

View
====

Django's views are the information brokers of a Django application. A view sources data from your
database and delivers it to a template.

Views are represented by either a function, or a classes methode's. Each view has an associated 
template.

The **views.py** file is automaticaly created inside the app's directory, when you are using the 
*startapp* wizard.

Displaying error pages
----------------------

There are four built-in function-based views for displaying error pages :

    * The 404 (page not found) view

    * The 500 (server error) view

    * The 403 (HTTP forbiden) view

    * The 400 (bad request) view

class-based views for simplifying common display tasks
------------------------------------------------------

There are several class-based views for simplifying common display tasks. They include:

    * ListView : for displaying a list of data objects.

    * DetailView : for displaying a single object

    * RedirectView : for redirecting to another URL

    * FormView : for displaying a form

URL Configuration (URLconf)
===========================

There are several URL Configuration's file (**urls.py**) :

    * One into the Porject's directory. It is created automatically with the "startproject wizard"

    * One per Application's directory. Need to be created manually in every apps' directories.

**URL Configuration** decide which view (from *views.py* or *forms.py* files) will deal with the 
request. When Django finds a URL in *urls.py* that matches the request URL it calls the view 
associated with that URL. The selected view then renders the content to the template.

Admin
=====

    :Liens_Web:

        * `Django Project admin site`_: admin site's page from the Djongo's documentation.

    :Automatic Admin Interface:
        
        It reads metadata from your models to provide a quick, model-centric interface where trusted
        users can manage content on the Django's project. It must be use as an internal management 
        tool. It mustn't be use for building the entire front end.
        
        With Django's admin you can :

            * Authenticate users.

            * Display and handle forms and validate input.

            * Provide a convinient interface to our models for adding content to our app.

    :admin.py:

        The *admin.py* file is created with every apps when your are using the "startapp" wizard. It
        display your models in the Django admin's pannel.

####

--------------
Install Django
--------------

Creating a project directory
============================

The first thing to do is to create a project directory. The directory's name can be modified later,
but it can be easyer if you tag it whith "\ROOT_" followed by the name of the project : ::

    mkdir ROOT_MySuperProject

Installing Django in a Virtual Environement
===========================================

    :Liens_Web:
                    * `Django Project Install`_ : Install from the official documentation.

Assuming "virtualenv" is already installed.

    #. From root of project's directory , create a subdirectory and then create your virtual 
       environement into it. 

       .. code:: shell

            mkdir env_MySuperProject
            cd env_MySuperProject
            python -m virtualenv .
            # /!\ don't forget the dot at the end of the line

    #. Activate the Virtual Environement and install Django :

        .. code:: shell

            env_MySuperProject\Script\activate.bat
            pip install "django>=2.1, <2.2"
            pip install "psycopg2>=2.7,<3.0"

            ## autre solution avec un fichier 'requirements.txt

            # requirements.txt
            Django>=2.0,<3.0
            psycopg2>=2.7,<3.0
            pip install -r requirements.txt

####

-------------------------------
How to start and basic's usages
-------------------------------

Starting a project
==================

    #. From root of project's directory, run the "startproject" wizard :

        .. code:: shell

            django-admin startporject [project_name]

            ex:
            django-admin startporject mySuperProject

            A Directory will be created in the root directory.

    #. Creating a Database :

        .. code:: shell

            cd mySuperProject
            python manage.py migrate

       The *migrate* command creates a new SQLite database and any necessary database tables
       according to the setting file created by the "startporject" command.

Django Shell and Developement Server
====================================

Django Shell
------------

For testing some stuff, you can run a python shell that include the features of Django : 

    .. code:: shell

        python manage.py shell

The developement Server
-----------------------

The developement Server is a lightweight Web server. It is only for the developement environement
and mustn't be use in production environement. 

    .. code:: shell

        # To run the dev server :
        python Manage.py runserver

        # in Dev mode with Debug=False in the settings.py file
        python manage.py run --insecure

        # to use the dev server (in a web browser):
        http://127.0.0.1:8000
    
Django Settings (settings.py)
=============================

    :Liens_Web:     
    
            * `Django Project REF Settings`_ : The  settings\' references from the official
              documentation

            * `Django Project TOPICS Settings`_ : The settings\' topic from the official
              documentation

    :settings.py:
    
            This file contains the configuration information for your Django project.

Django Applications
===================

A Django application (app) is where the work is done. Good design practice says that each Django app
should do one thing (ex: a blog, an article directory, a music collection, etc ...). A Django
project is the collection of apps and configuration settings that make up a Django website.

Creating an App
---------------

    #. Create an app 

        .. code:: shell

            # startapp syntaxe
            python manage.py startapp [app_name]

            # ex: 
            python manage.py startapp pages

    #. Add the new app to the Django project

        All new app must be adding to the **"settings.py"**.

        Inside the **"settings.py"** file, there is a list named **"INSTALLED_APPS"**. This list
        contains all the apps that are installed in the Django project. We just have to add our new
        app to the top of this list.

        Django create **"apps.py"** inside every app. This file contains a configuration class named
        after your app. To register our app with Django, we need to point to this class. the path of
        this class looks like this : 

            .. code:: 

                App's DIR --> apps.py --> [class named after your app]

                # ex for an app called "pages"

                pages.apps.PagesConfig

        The setting list "INSTALLED_APPS" should be : 

            .. code:: python

                INSTALLED_APPS = [
                    'pages.apps.PagesConfig',
                    'django.contrib.admin',
                    # more apps
                ]

    :/!\\ WARNING /!\\: 
            
            Applications must also be entered in the "urls.py" file of the project.

Configuring the URLs (urls.py)
==============================

    :Liens_Web:
            * `Django Project TOPICS URLs`_ : The URLs settings\' Topics from the official
              documentation.

    :path():    The **path()** function is used to configure URLs. In its basic form, it as a very
                simple syntax :

                    .. code:: python

                        path(route, view)

                        # ex:
                        path('mypage/', views.myview)

The application's url
---------------------

We need to create **"urls.py"** in every app's directory and then we need to complete it with a few
set of instruction.

    #. Creating app/urls.py 

        .. code:: shell

            cd [app_name]
            mkdir urls.py

    #. Import "path()" and app.views.py 

        .. code:: python

            from django.urls import path
            from . import views

    #. Set the application's namespace

       To avoid strange behavior if applications use a view with the same name, we need to set 
       "app_name" with the application's name. 

            .. code:: python

                app_name = [Application's name]

                # ex:
                app_name = "pages"

    #. Set the urlpatterns

       .. code:: python

            urlpatterns = [
                # The '' is the default page
                path('', views.index, name='index'),
                ]

The minimum content of the application urls file looks like this :

    .. code:: python

        from django.urls import path
        from . import views

        app_name = "pages"

        urlpatterns = [
            # The '' is the default page
            path('', views.index, name='index'),
            ]

The site's url (the Django's project)
-------------------------------------

    #. Import "include"

    import the "include" function in addition to the "path" function.

        .. code:: python

            from django.urls import path, include

    #. Add the new url dispatcher to the urlpatterns

        .. code:: python

            urlpatterns = [
                path('admin/', admin.site.urls),
                path('', include('pages.urls')),
                ]

    :/!\\ WARNING /!\\:

            * **'admin/'** : must be the first entry in the patterns. 

            * **''** or **'/'** : Must be the last entry in the patterns. 

            .. code:: python

                # exemple of the project's file "urls.py"
                from django.urls import path, include

                urlpatterns = [
                    path('admin/', admin.site.urls),
                    # ...
                    path('', include('pages.urls')),
                ]

apps' model (models.py)
=======================

    :Liens_Web:
            * `Django Project TOPICS Models`_

            * `Django Project Model field reference`_: the Model field reference from the Djanog's
              documentation.

            * `Model Meta options`_: Options for the Meta class

Create the app class
--------------------

    #. Create the app class

        In the **models.py** file of the app's directory, create the app class. It must inherit from 
        Django's Model Class.

        .. code:: python

            # for an app called "page"

            class Page(models.Model):

    #. Define the field for the model

        These fields will have a corresponding field in the table that Django creates for the model
        in the databases.

        .. code:: python

            # exemple of some field you can create
            title = models.CharField(max_length=60)
            permalink = models.CharField(max_length=12, unique=True)
            update_date = models.DateTimeField('Dernière MAJ')
            bodytext = models.TextField('Page Content', blank=True)
            
    #. Adding Metadata information for sorting, select the DB Table, and so on.

        .. code:: python

            # exemple of a Meta class
            class Meta:
                ordering = ['title']

    #. returns a URL for displaying individual model records on the website

        Assume that the "model-detail-view" view is defined in "views.py".

        .. code:: python

            def get_absolute_url(self):
                """Returns the url to access a particular instance of the model."""
                return reverse('model-detail-view', args=[str(self.id)])

    #. Return a human-readable version of the Pages class

        If python ask for a string representation of the Pages object, we need to create a special
        methode that return a human-readable string instead of the default string "Page object".

        .. code:: python

            def __str__(self):
                return self.title

        **N.B:** Adding this method does not imply that you need to migrate the database again.

    #. Check files before migration

        .. code:: shell

            python manage.py check

    #. Prepare for migration and then migrate

        .. code:: shell
        
            # exemple for an app called "pages"
            python manage.py makemigrations pages
            ...
            python manage.py migrate

admin site (and admin.py)
=========================

Create a admin user (superuser)
-------------------------------

Before using the admin site, you need to create a super-User. 

    .. code:: shell

        python manage.py createsuperuser

        >Username: ...
        >Password: ...
        >Password (again): ...

Registering model
-----------------

    :Liens_Web:
            * `The Django admin site`_

For a model to be accessible from the admin, it need to be registered into the **admin.py**.

    .. code:: python

        # admin.py
        from django.contrib import admin
        from .models import Page    # Import the class from the "models.py" file of the app
                                    #
                                    # N.B: If "model.py" includes more than one class you 
                                    # can / should import them all and save it in the same way so
                                    # that it is available on the admin page.

        admin.site.register(Page)

List_display, ordering and searh_fields
---------------------------------------

To change how a model is displayed in the admin interface, we need to define a ModelAdmin class
(which describe the layout) and register it with the model. This class is called after the class'
name of the *"models.py"* file + "Admin" in the **admin.py** file.

    .. code:: Python

        # Model's class name + "Admin"
        # For a class called "Page" in models.py

        class PageAdmin(admin.ModelAdmin):
            # [...]


In the Admin site, we need to sort pages and keep track of changes. We also need to be able to 
search a specific page. Add commands bellow to the admin's model class.

    #. See last update to keep track of change

        .. code:: python

            # in the PageAdmin's class
            # 'title' and 'update_date' are fields displaying in the list of pages
            list_display = ('title', 'update_date')

    #. Sort the display list (ordering by 'title')
        
        .. code:: python

            # in the PageAdmin's class
            # 'title' is the field use to sort the list
            ordering = ('title',)

    #. Search a pages

        .. code:: python

            # in the PageAdmin's class
            # 'title' is the field should be search
            search_fields = ('title',)

    #. Add a filter in the admin page

        .. code:: python

            # Only elements matching to the filter will appear
            list_filter('title',)

    #. Add the class to the 'admin.site.register

        .. code:: python

            admin.site.register(Page, PageAdmin)    # this must no be include into the 
                                                    # MadelAdmin class


        An alternative syntax for registering the MadelAdmin class is to use the register decorator:

        .. code:: python

            @admin.register(Page)
            class PageAdmin(admin.ModelAdmin):
                # do some stuff like ...
                # list_display = ('title', 'update_date')
                # ordering = ('title',)
                # search_fields = ('title',)


Adding content
--------------

    :/!\\ WARNING /!\\:

            When entering the page content (*TextField*), remember that it needs to be HTML to
            display well in your browser.

Django Templates
================

    :Liens_Web:

            * `Django Project TEMPLATES`_: the templates reference from the Djanog's
              documentation.

Template Settings
-----------------

For Django to show your site template, it first must know where to look for template file(s). To
bind a template to the project, you must complete the **TEMPLATES['DIR']** in the **settings.py** file.

Not all template files will be tied to a particuliar app. The **'DIRS'** setting is usefull for
linking to templates that exit elsewere in your project structure.

    #. Add a template's path to **TEMPLATES['DIRS']**

        .. code:: python

            # Exemple for a template in the project's dir, and not bind to a specific app.
            # In the settings.py file
            TEMPLATES = [
                    # ...
                    'DIRS': [os.path.join(BASE_DIR, 'fdw/templates')],
                    'APP_DIRS': True,
                    # ...
                    ]

       **N.B:** 
            * For an app's template, the path must be '[app's_dir]/templates'

            * If 'APP_DIRS' is Ture, Django will look for a folder named *templates* in each of
              your apps. Default is True.

    #. Create the templates' dir into the project's dir 
           ::

                # in the same dir of the *settings.py* file
                mkdir templates

       **N.B:** For an app's template, you must create the template's dir in the same dir of the
       *views.py* file.

base.html file
--------------

The **base.html** file is the 'model' that the other web pages will inherit from, to avoid
to rewrite the same code again and again (DRY). In the child page, only some specific blocks
will be rewritten.

The content of this specific bloks will be replace in the child page only if it is necessary.

    .. code:: html

        <!-- base.html -->
        [...]
        {% block h1_title %}
            <h1>Base h1 title</h1>
        {% enblock h1_title %}
        [...]
        {% block parragraph %}
            <p>
                Lorem ipsum dolor sit amet consectetur, adipisicing elit. Quis, accusantium beatae 
                rem, cum quam, quaerat omnis ad consectetur eligendi placeat minima illo modi culpa
                expedita at reprehenderit corporis suscipit pariatur!
            </p>
        {% enblock parragraph %}


    .. code:: html

        <!-- child.html -->
        {% extends "base.html" %}
        [...]
        {% block h1_title %}
            <h1>Child h1 title</h1>
        {% endblock h1_title %}
        [...]
        {% block parragraph %}
        {% enblock parragraph %}

It is a good practice to create the first "web page" under the project_site's folder :

    .. code:: 

        +---poject_site
        |   [...]
        |   |
        |   \---templates
        |           base.html
        |
        +---App's folder
        |
        [...]

The app's html template
-----------------------

If an app need a html template, we need to create a dir  'templates' in the app's root dir. We also need
to create a new dir nammed as the app inside the templates dir.

    .. code:: 

        +---pages                       <-- app's name
        |   |   [...]
        |   |
        |   +---migrations
        |   |
        |   \---templates
        |       \---pages
        |               contact.html
        |               page.html       <-- inherit from 'base.html'

Static Files
============

    :Liens_Web:

        * `Django Project Static Files`_: the Static Files' reference from the Djanog's
          documentation.

        * `Django Project Deploying static files`_: How to deploying Static files in production
          environement


Static Files are : Images, CSS and JavaScript. Django keep static media in a different directory to
the rest of the application. The directory is defined in the *settings.py* file and is called 
**static** by default. Until the site is in developement, the static dir need to be in the
project_site's dir, at the same level of the templates' dir.

    .. code:: 

        +---project_site
        |   |   [...]
        |   |
        |   +---static
        |   |       logo.jpg
        |   |       main.css
        |   |       top_banner.png
        |   |
        |   \---templates
        |
        +---App's folder
        |
        [...]

    .. code:: python

        STATIC_URL = '/static/'

To find the static files for our site, we need to add a static file's dir :

    .. code:: python

        # Look for static files in the 'static' directory  in our site root
        STAITCFILES_DIR = [
            os.path.join(BASE_DIR, 'fdw/static'),
            ]



To load static file in the template, we need to add it (with the template syntax) at the top of the 
Template. After that, to call / load a specific file from the static's dir, we need to use the 
'static' key word.

    .. code:: python

        # To load static file
        {% load static %}

        # to call / load a specific file from the static's dir
        {% static 'logo.jpg' %}

    **Exemple code :**

    .. code:: html

        {% load static %}
        <!doctype html>
        <html>
            <head>
                <meta http-equiv="Content-Type" content="text/html;charset=UTF-8">
                <title>Untitled Document</title>
                <link rel="stylesheet" href="{% static 'main.css' %}" type="text/css">
            </head>
            <body>
                <div id="wrapper">
                    <header id="header">
                        <div id="logo">
                            <img src="{% static 'logo.jpg' %}" alt=""/>
                        </div>
                    </header>
                </div>
            </body>
        </html>

Django's Error Page
===================

    :Liens_Web:

            * `Howto : Error reporting`_ : The error reporting's page form the Dango's documentation

When you’re running a public site you should always turn off the **DEBUG** setting (in the 
*settings.py's* file). That will make your server run much faster, and will also prevent malicious 
users from seeing details of your application that can be revealed by the error pages.

If **DEBUG** = True, Django will display à **Template-loader postmortem** to show where things
went wrong.

One simple way for testing is to make sure the view is passing the right information back to the
template is to use Django's error page to examine output of the view. For forcing the error page
to appear, add "assert false" just before the return line in the views.py.

    .. code:: python

        def index(request):
            # [...]
            context = {
                # [...]
                }
            assert false    # If this line is not commented, the return will be false
                            # and the function will recive an exit signal
            return render(request, 'base.tml', context)

    **N.B:** Don't forget to comment the 'assert' line for the standard behavior. 

The Django's Error page in Dev mode
-----------------------------------

    * **Exception Type** : first two line of error's page is the Exception Type. It help to
      understand what went wrong.

    * **Traceback** : In the Traceback, the bold line is the were the exption was raise.

Forms
=====

    :Liens_Web:

        * `Working with forms`_
        * `Form fields`_

Django's forms are a easy way to create, in the template, a form from the model.

Django handles three distinct parts of the work involved in forms

    * preparing and restructuring data to make it ready for rendering
    * creating HTML forms for the data
    * receiving and processing submitted forms and data from the client

Email
-----

    :Liens_Web:

        * `Sending email`_ : Django's documentation
        * `settings.py : EMAIL`_ : EMAIL's instructions for the sttings.py's file

Django provide the EmailMessage class for sending and reciving Email. By default **EMAIL_BACKEND**
is set to use the **Console backend** witch is sending email from form to the console. For the list
of available backends see **Sending email** to use it in production.


####

Django's View (views.py)
========================

    :Liens_Web:

        * `Writing views`_ : Dango's documentation for the function-based views

At the fundamental level, a view function is a Python function that take a Web request and returns
a Web response. This response can be the HTML contents of a Web page, or a redirect, or a 404 error,
or an XML document, or an image, or anything.

class-based views
-----------------

    :Liens_Web:

        * `Class-based views`_ : Dango's documentation for the Class-based views

        * `Built-in class-based views API`_ : The list of the Dango's class-based view

Django provide a lot of **class-based views** to simplifying developement.

        .. code:: python

            # exemple for "ListView"

            ## quotes/views.py
            from django.views.generic.list import ListView
            from .models import Quote

####

File Uploads
============

    :Liens_Web:

        * `Upload file in Django`_ : Django's documentation

####

----------
Vocabulary
----------

    :Mixins:

            Mixins are a form of multiple inheritance where behaviors and attributes of mulptiple
            classes can be modified.

            :Liens_Web:

                * `Using mixins`_

    :QuerySet:

            A QuerySet represents a collection of objects from your database. It can have zero,
            one or many filters. Filters narrow down the query results based on the given 
            parameters. In SQL terms, a QuerySet equates to a SELECT statement, and a filter is a
            limiting clause such as WHERE or LIMIT.

            .. code:: python

                # example
                Blog.objects.all()  # returns a QuerySet that contains all Blog objects in the 
                                    # database.

                Entry.objects.filter(pub_date__year=2006)
                                    # returns a QuerySet that contains only blog's entries of 
                                    # the year 2006

            :Liens_Web:

                    * `QuerySet API ref`_
                    * `Making queries`_

            :Scope:

                Apply to the DataBase, but is used in the "Views.py" and "forms.py" files

    :Slug:

            Slug is a newspaper term. A slug is a short label for something, containing only 
            letters, numbers, underscores or hyphens. They’re generally used in URLs. For example,
            in a typical blog entry URL: 

                ::

                    https://www.djangoproject.com/weblog/2008/apr/12/spring/

            the last bit (spring) is the **slug**.

            :Liens_Web:

                    * `SlugField`_ 

            :Scope:

                Apply to the DataBase (models.SlugField) 

####

----------
Webography
----------

.. target-notes::

.. _`Django Project TOPICS Models`: https://docs.djangoproject.com/en/2.1/topics/db/models/
.. _`Django Project Settings Databases`: https://docs.djangoproject.com/en/2.1/ref/settings/#std:setting-DATABASES
.. _`Django Project admin site`: https://docs.djangoproject.com/en/2.1/ref/contrib/admin/
.. _`Django Project Install`: https://docs.djangoproject.com/en/2.1/intro/install
.. _`Django Project REF Settings`: https://docs.djangoproject.com/en/2.1/ref/settings/
.. _`Django Project TOPICS Settings`: https://docs.djangoproject.com/en/2.1/topics/settings/
.. _`Django Project TOPICS URLs`: https://docs.djangoproject.com/en/2.1/topics/http/urls/
.. _`Django Project Model field reference`: https://docs.djangoproject.com/en/2.1/ref/models/fields/
.. _`Model Meta options`: https://docs.djangoproject.com/en/2.1/ref/models/options/
.. _`The Django admin site`: https://docs.djangoproject.com/en/2.1/ref/contrib/admin/
.. _`Django Project TEMPLATES`: https://docs.djangoproject.com/en/2.1/ref/templates/
.. _`Django Project static files`: https://docs.djangoproject.com/en/2.1/howto/static-files/
.. _`Django Project Deploying Static Files`: https://docs.djangoproject.com/en/2.1/howto/static-files/deployment/
.. _`Howto : Error reporting`: https://docs.djangoproject.com/en/2.1/howto/error-reporting/
.. _`Working with forms`: https://docs.djangoproject.com/en/2.1/topics/forms/
.. _`Form fields`: https://docs.djangoproject.com/en/2.1/ref/forms/fields/
.. _`Sending email`: https://docs.djangoproject.com/en/2.1/topics/email/
.. _`settings.py : EMAIL`: https://docs.djangoproject.com/en/2.1/ref/settings/#email-backend
.. _`Writing views`: https://docs.djangoproject.com/en/2.1/topics/http/views/
.. _`Class-based views`: https://docs.djangoproject.com/en/2.1/topics/class-based-views/
.. _`Built-in class-based views API`: https://docs.djangoproject.com/en/2.1/ref/class-based-views/
.. _`Upload file in Django`: https://docs.djangoproject.com/en/2.1/topics/http/file-uploads/

.. _`Using mixins`: https://docs.djangoproject.com/en/2.1/topics/class-based-views/intro/#using-mixins
.. _`QuerySet API ref`: https://docs.djangoproject.com/en/2.1/ref/models/querysets/
.. _`Making queries`: https://docs.djangoproject.com/en/2.1/topics/db/queries/
.. _`SlugField`: https://docs.djangoproject.com/en/2.2/ref/models/fields/#slugfield
