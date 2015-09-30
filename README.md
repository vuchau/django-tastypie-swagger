![Concentric Sky](https://concentricsky.com/media/uploads/images/csky_logo.jpg)

## Django Tastypie Swagger

**django-tastypie-swagger** is a small adapter library to construct [Swagger](http://swagger.wordnik.com/) documentation from [Tastypie](https://django-tastypie.readthedocs.org) resources.

This package provides two things:

1. An embedded instance of [Swagger UI](https://github.com/wordnik/swagger-ui) to point a URL to.
2. Automatic [Resource Listing](https://github.com/wordnik/swagger-core/wiki/Resource-Listing) and [API Declaration](https://github.com/wordnik/swagger-core/wiki/API-Declaration) generation that is consumed by #1
3. Markdown parsing of Resource docstrings using misaka


### Table of Contents
- [Version History](#version-history)
- [Documentation](#documentation)
- [Installation](#installation)
- [Getting Started](#getting-started)
- [Contributors](#contributors)
- [License](#license)
- [About Concentric Sky](#about-concentric-sky)


## Version History

- v0.1.3 Various bug fixes and documentation updates
- v0.1.2 Fixes for Django 1.5 compatibility
- v0.1.1 Public codebase was released


## Documentation

Detailed documentation is available on [Read The Docs](http://django-tastypie-swagger.readthedocs.org/en/latest/).

**Additional for custom API**
+ URL convention

    ```
    def prepend_urls(self):
        ...
        url(r'^(?P<resource_name>%s)/login%s$' %
                (self._meta.resource_name, trailing_slash()),
                self.wrap_view('login'), name="api_login"),
        ...
    ```
+ Func convention
    
    ```
    def login(self, request, **kwargs):
        """
        Login into system

        :argument
        { "username" : "test01", "password" : "test01" }

        :return
        {
          "avatar_url": "avatar_url",
          "email": "user02@gmail.com",
          "full_name": "Test 02",
          "id": 115,
          "token": "8937c19ae1a3424f33fb0b7c61578bb954bf6bba",
          "username": "user02"
        }
        """
        ...

    ```
    **To get document of method, you must set name of url = "api_" + wrap_view**

## Installation

Install package::

    pip install django-tastypie-swagger

Add to INSTALLED_APPS::

    INSTALLED_APPS = [
        ...

        'tastypie_swagger',

        ...
    ]


## Getting Started

Enable documentation for an api endpoint by adding a URL to your urlpatterns.

eg::


    urlpatterns = patterns('',
        ...

        url(r'api/myapi/doc/',
          include('tastypie_swagger.urls', namespace='myapi_tastypie_swagger'),
          kwargs={"tastypie_api_module":"myapp.registration.my_api", "namespace":"myapi_tastypie_swagger"}
        ),

        ...
    )


To declare more than one endpoint, repeat the above URL definition and change the namespace.

Swagger documentation will be served up at the URL(s) you configured.

## Contributors

Contributors to this project are listed in the CONTRIBUTORS.md file. If you contribute to this project, please add your name to the file.


## License

This project is licensed under the Apache License, Version 2.0. Details can be found in the LICENSE.md file. License for third-party code is available in 3RDPARTYLICENSES.md.


## About Concentric Sky

_For nearly a decade, Concentric Sky has been building technology solutions that impact people everywhere. We work in the mobile, enterprise and web application spaces. Our team, based in Eugene Oregon, loves to solve complex problems. Concentric Sky believes in contributing back to our community and one of the ways we do that is by open sourcing our code on GitHub. Contact Concentric Sky at hello@concentricsky.com._
