.. Blacksmith documentation master file, created by
   sphinx-quickstart on Mon Jan  9 12:06:10 2017.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Blacksmith
======================================

Blacksmith is your source for retreiving Entities and their types


API Keys, Public and Private
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Entity Types can be defined as public or private. Private Entity Types and their respective entities require the client API Key in order to retreive

API Keys can be sent in one of two ways:

A header field called `x-api-key`

In the query string as `apikey`

**https://blacksmith.goodmeasure.io/**

Entity Types (Blueprints) & Entities (Items)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

+--------------------------------------+---------+----------+
| Route                                | Method  | Auth     |
+======================================+=========+==========+
| /:user/blueprint                     | GET     | Required |
+--------------------------------------+---------+----------+
| /:user/blueprint/:entitytype_name    | GET     | Required |
+--------------------------------------+---------+----------+
| /:user/:entitytype_name              | GET     | Optional |
+--------------------------------------+---------+----------+
| /:user/:entitytype_name/:entity_name | GET     | Optional |
+-------------------------------------+----------+----------+


Forging
^^^^^^^

+--------------------------------------+----------+----------+
| Route                                | Method   | Auth     |
+======================================+==========+==========+
| /:user/forge/:entitytype_name        | GET/POST | Optional |
+--------------------------------------+----------+----------+

Returns you an item based on forge rules set up in the GoodMeasure UI. If no forge rules pass then an empty object is returned.

Batching
^^^^^^^^

+-------------------------------------+----------+----------+
| Route                               | Method   | Auth     |
+=====================================+==========+==========+
| /:user/batch                        | POST     | Optional |
+-------------------------------------+----------+----------+

The batch route allows the sending off multiple of the above requests at once (Max Batch is currently 10).

**When batching requests from the same unique user make sure to supply a source object with a matching requestid.**

Request Body Example::

    [
        {
            type: 'forge',
            blueprint: :entitytype_name,
            source: {
                email: 'axe@yousome.questions',
                requestid: '123abc'
            }
        },
        {
            type: 'entity',
            blueprint: :entitytype_name,
            name: :entity_name,
            source: {
                requestid: '123abc'
            }
        },
        {
            type: 'entitytype',
            blueprint: :entitytype_name,
            tags: [
                'atag'
            ],
            source: {
                requestid: '123abc'
            }
        }
    ]

Response Body Example::

    [
        {
            results: 200,
            item: {} //the decided upon item
        },
        {
            results: 200,
            item: {} //item requested
        },
        {
            results: 200,
            item: [] //array of entities of enitity type with requested tags
        }
    ]

Staging Params
^^^^^^^^^^^^^^^^^^^^^^^^^

+--------------------------------------+----------+----------+
| Route                                | Method   | Auth     |
+======================================+==========+==========+
| /:user/setParams                     | GET/POST | Required |
+--------------------------------------+----------+----------+

The set params route is design for both staging of variables to decision upon later or recording "outcome" variables.

The route will accept and store your query params or request body depending on method and respond with the complete request object for the given requestid.

Outcome Variables
^^^^^^^^^^^^^^^^^

Outcome variables are defined in your GoodMeasure UI and are always proceeded by an o_

Outcome variables are set using the above setParams route but have the additional feature of being able to be incremented by proceeding the value with a + i.e. +1 or +13