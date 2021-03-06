# API Logic Server

There is widespread agreement that APIs are strategic
to the business, required for mobile apps and internal
/ external systems integration.

The problem is that they are time-consuming and costly to develop.
This reduces strategic business agility.

API Logic Server provides strategic business agility,
by creating executable APIs from a database, instantly:

- **API:** [swagger/OpenAPI](https://swagger.io/)
  and [JSON:API](https://jsonapi.org) compliant.
  Uses [SAFRS](https://github.com/thomaxxl/safrs/wiki), a modern approach that enables client applications to configure their own API to reduce network traffic.


- **Web App:** a multi-page, multi-table web app;
  uses [fab-quickstart](https://pypi.org/project/fab-quick-start).


- **Logic:** spreadsheet-like rules for multi-table derivations and constraint
  that reduce transaction logic by 40X,
  using [Logic Bank](https://pypi.org/project/logicbank).
  
This declarative approach is based on standard Python tooling,
and can be customized with standard approaches as described below.

## Usage

### Install with ```pip```

```
cd ~/Desktop
mkdir server
cd server
virtualenv venv
source venv/bin/activate
# windows venv\Scripts\activate
pip install ApiLogicServer
```

### Quick Start - Create and Execute
This verifies proper install - it will
create and run an [ApiLogicServer Project](../../wiki/Created-Project):

```
ApiLogicServer run --project_name=my_api_logic_server
```

The ``db_url`` parameter defaults to a supplied [sample database](../../wiki/Sample-Database).
Specify a [SQLAlchemy url](https://docs.sqlalchemy.org/en/14/core/engines.html)
to use your own database.


### Create (only)

You can also create the project, without execution.
As above, this verifies proper install:

```
ApiLogicServer create --project_name=my_api_logic_server
cd my_api_logic_server
virtualenv venv
source venv/bin/activate
# windows venv\Scripts\activate
pip install -r requirements.txt
```

You may also wish to include the ``open_with`` parameter,
to open an IDE or Editor on the created project.  For example,
PyCharm (``charm``) will open the project and create / initialize the ``venv``
automatically (some PyCharm configuration may be required):

```
ApiLogicServer create --project_name=my_api_logic_server db_url=sqlite:///nw.sqlite --open_with=charm
```

### Execution
With a proper [environment](../../wiki/Created-Project#environment):

```
python api_logic_server_run.py
python ui/basic_web_app/run.py
```


## Features


### API: SAFRS JSON:API and Swagger

Your API is instantly ready to support ui and integration
development, available in swagger:

<figure><img src="images/swagger.png"></figure>

    Customize your API: https://github.com/thomaxxl/safrs/wiki/Customization

### Logic

Transactional business logic - multi-table derivations and
constraints - are a significant portion of database systems,
often nearly half.  Procedural coding is time-consuming
to develop and maintain, reducing business agility.

ApiLogicServer integrates Logic Bank, spreadsheet-like rules
that reduce transaction logic by 40X.
Logic is declared in Python (example below), and is:

- **Extensible:** logic consists of rules (see below), plus standard Python code

- **Multi-table:** rules like ``sum`` automate multi-table transactions

- **Scalable:** rules are pruned and optimized; for example, sums are processed as *1 row adjustment updates,* rather than expensive SQL aggregate queries

- **Manageable:** develop and debug your rules in IDEs, manage it in SCS systems (such as `git`) using existing procedures

The following 5 rules represent the
[same logic](https://github.com/valhuber/LogicBank/wiki/by-code)
as 200 lines of Python:
<figure><img src="https://github.com/valhuber/LogicBank/raw/main/images/example.png"></figure>

    Declare your logic by editing: logic/rules_bank.py


### Basic Web App - Flask Appbuilder

UI development takes time.  That's a problem since
* Such effort may not be warranted for admin "back office" screens,
and
  
* [Agile approaches](https://agilemanifesto.org) depend on getting _working
software_ soon, to drive _collaboration and iteration_.

ApiLogicServers therefore generate multi-page, multi-table
applications as shown below:

1. **Multi-page:** apps include 1 page per table

2. **Multi-table:** pages include ``related_views`` for each related child table, and join in parent data

3. **Favorite field first:** first-displayed field is "name", or `contains` "name" (configurable)

4. **Predictive joins:** favorite field of each parent is shown (product *name* - not product *id*)

5. **Ids last:** such boring fields are not shown on lists, and at the end on other pages

<figure><img src="https://raw.githubusercontent.com/valhuber/fab-quick-start/master/images/generated-page.png"></figure>

    Customize your app by editing: ui/basic_web_app/app/views.py

## Status
Pre-Alpha / Technology Preview - just entering test.

## Acknowledgements

Many thanks to

- Thomas Pollet, for SAFRS
- Daniel Gaspar, for Flask AppBuilder
- Achim Götz, for design collaboration


## Change Log

1.0.7 - Initial Version

1.0.8 - Fix windows bug, options to specify clone-from and open-with

1.0.9 - ``Run`` command (experimental)