Development
===========

Getting started
---------------


``fastapi_aad_auth`` is a volunteer maintained open source project and we welcome contributions of all forms. The sections
below will help you get started with development, testing, and documentation. We’re pleased that you are interested in
working on ``fastapi_aad_auth``. This document is meant to get you setup to work on ``fastapi_aad_auth`` and to act as a guide and reference
to the development setup. If you face any issues during this process, please
`open an issue <https://github.com/nholuongut/fastapi-aad-auth/issues/new?title=Trouble+with+development+environment>`_ about it on
the issue tracker.

Setup
~~~~~

``fastapi_aad_auth`` is an extension component to :pypi:`fastapi` to provide Azure Active Directory authentication,
written in Python. To work on it, you'll need:

- **Source code**: available on `GitHub <https://github.com/nholuongut/fastapi-aad-auth>`_. You can use ``git`` to clone the
    repository:

  .. code-block:: console

      git clone https://github.com/nholuongut/fastapi-aad-auth
      cd fastapi_aad_auth

- **Python interpreter**: We recommend using ``CPython``. You can use
  `this guide <https://realpython.com/installing-python/>`_ to set it up.

- :pypi:`tox`: to automatically get the projects development dependencies and run the test suite.

- **Azure Active Directory App Registration**: We recommend following the configuration section in usage


Running tests
~~~~~~~~~~~~~

``fastapi_aad_auth`` tests are written using the :pypi:`pytest` test framework. :pypi:`tox` is used to automate the setup
and execution of ``fastapi_aad_auth`` tests.

To run tests locally execute:

.. code-block:: console

    tox -e test

This will run the test suite for the same Python version as under which ``tox`` is installed.

.. _testing:

Integration tests
~~~~~~~~~~~~~~~~~

``fastapi_aad_auth`` is very tightly coupled to Azure Active Directory, so most of the full tests follow manual testing
of the testapp. This needs configuring with Azure Active Directory App Registrations (see :ref:`config-aad-appreg`) and
the testapp environment using a ``.env`` file (see :ref:`config-fastapi_aad_auth-env`).

To run the testapp use tox (or directly with ``python tests/testapp/server.py``:

.. code-block:: console

    tox -e testapp

This will run the test app for the same Python version as under which ``tox`` is installed.


Configuring the testapp
#######################

The testapp requires configuring (see :ref:`config-aad-appreg`) for how to configure an appropriate App Registration on Azure.
The app provides a really simple set of tests - the home page has no authentication, but if you have logged in, it will say "hello <email>",
with your logged in email.

The api docs (swagger UI) is authentication limited, as is the simple api endpoint '/hello'.



Running linters
~~~~~~~~~~~~~~~

``fastapi_aad_auth`` uses :pypi:`flake8` and extensions for managing linting of the codebase. ``flake8`` performs various checks on all
files in ``fastapi_aad_auth`` and uses tools that help follow a consistent code style within the codebase. To use linters locally,
run:

.. code-block:: console

    tox -e lint

.. note::

    Avoid using ``# noqa`` comments to suppress linter warnings - wherever possible, warnings should be fixed instead.
    ``# noqa`` comments are reserved for rare cases where the recommended style causes severe readability problems.

Building documentation
~~~~~~~~~~~~~~~~~~~~~~

``fastapi_aad_auth`` documentation is built using :pypi:`Sphinx`. The documentation is written in reStructuredText. To build it
locally, run:

.. code-block:: console

    tox -e docs

The built documentation can be found in the ``docs/html`` folder and may be viewed by opening ``index.html`` within
that folder.

Release
~~~~~~~

We release through GitHub using an automated process to collate and test the releases. 

Developing
------------

Submitting pull requests
~~~~~~~~~~~~~~~~~~~~~~~~

Submit pull requests against the ``master`` branch, providing a good description of what you're doing and why. You must
have legal permission to distribute any code you contribute to ``fastapi_aad_auth`` and it must be available under the MIT
License. Provide tests that cover your changes and run the tests locally first. ``fastapi_aad_auth``
:ref:`supports <compatibility-requirements>` multiple Python versions. Any pull request must
consider and work on all these platforms.

Pull Requests should be small to facilitate review. Keep them self-contained, and limited in scope. `Studies have shown
<https://www.kessler.de/prd/smartbear/BestPracticesForPeerCodeReview.pdf>`_ that review quality falls off as patch size
grows. Sometimes this will result in many small PRs to land a single large feature. In particular, pull requests must
not be treated as "feature branches", with ongoing development work happening within the PR. Instead, the feature should
be broken up into smaller, independent parts which can be reviewed and merged individually.

Additionally, avoid including "cosmetic" changes to code that is unrelated to your change, as these make reviewing the
PR more difficult. Examples include re-flowing text in comments or documentation, or addition or removal of blank lines
or whitespace within lines. Such changes can be made separately, as a "formatting cleanup" PR, if needed.

Automated testing
~~~~~~~~~~~~~~~~~

All pull requests and merges to ``master`` branch are tested using
Github actions (configured by ``.github/workflows/pipeline.yml`` file. You can find the status and results to the CI runs for your
PR on GitHub's Web UI for the pull request. You can also find links to the CI services' pages for the specific builds in
the form of "Details" links, in case the CI run fails and you wish to view the output.

.. _compatibility-requirements:

Compatibility Requirements
~~~~~~~~~~~~~~~~~~~~~~~~~~

We endeavour to support (and test) on multiple python versions, across the following matrix of os and python versions:

.. literalinclude:: ../../.github/workflows/pipeline.yml
    :language: yaml
    :start-after: matrix:
    :end-before: max-parallel
    :dedent: 8