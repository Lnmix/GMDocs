.. Blacksmith documentation master file, created by
   sphinx-quickstart on Mon Jan  9 12:06:10 2017.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Blacksmith
======================================

Blacksmith is your source for retreiving Entities and their types


API Keys, Public and Private
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Entity Types can be defined at public or private. Private Entity Types and their respective entities require the client API Key in order to retreive

API Keys can be sent in one of two ways:

A header field called `x-api-key`
In the query string as `apikey`

**https://blacksmith.goodmeasure.io/**

Entity Types (Blueprints) & Entities (Items)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

+-------------------------------------+---------+----------+
| Route                               | Method  | Auth     |
+=====================================+=========+==========+
| /:user/blueprint                    | GET     | Required |
+-------------------------------------+---------+----------+
| /:user/blueprint/:blueprint_name    | GET     | Required |
+-------------------------------------+---------+----------+
| /:user/:blueprint_name              | GET     | Optional |
+-------------------------------------+---------+----------+
| /:user/:blueprint_name/:entity_name | GET     | Optional |
+-------------------------------------+---------+----------+

Block of text about Entity Types and Entities here

Forging
^^^^^^^

Batching
^^^^^^^^

Outcomes & Staging Params
^^^^^^^^^^^^^^^^^^^^^^^^^