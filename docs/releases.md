# 0.5.0

* Added save status -> you can check if model is saved with `ModelInstance.saved` property
    *  Model is saved after `save/update/load/upsert` method on model
    *  Model is saved after `create/get/first/all/get_or_create/update_or_create` method
    *  Model is saved when passed to `bulk_update` and `bulk_create`
    *  Model is saved after adding/removing `ManyToMany` related objects (through model instance auto saved/deleted)
    *  Model is **not** saved after change of any own field (including pk as `Model.pk` alias)
    *  Model is **not** saved after adding/removing `ForeignKey` related object (fk column not saved)
    *  Model is **not** saved after instantation with `__init__` (w/o `QuerySet.create` or before calling `save`)
*  Added `Model.upsert(**kwargs)` that performs `save()` if pk not set otherwise `update(**kwargs)`
*  Added `Model.save_related(follow=False)` that iterates all related objects in all relations and checks if they are saved. If not it calls `upsert()` on each of them.
*  **Breaking:** added raising exceptions if `add`-ing/`remove`-ing not saved (pk is None) models to `ManyToMany` relation
*  Allow passing dictionaries and sets to fields and exclude_fields
*  Auto translate str and lists to dicts for fields and exclude_fields
*  **Breaking:** passing nested models to fields and exclude_fields is now by related ForeignKey name and not by target model name 
*  Performance optimizations - in modelproxy, newbasemodel - > less queries, some properties are cached on models
*  Cleanup of unused relations code
*  Optional performance dependency orjson added (**strongly recommended**)
*  Updated docs

# 0.4.4

*  add exclude_fields() method to exclude fields from sql
*  refactor column names setting (aliases)
*  fix ordering by for column with aliases
*  additional tests for fields and exclude_fields
*  update docs

# 0.4.3

*  include properties in models.dict() and model.json()

# 0.4.2

*  modify creation of pydantic models to allow returning related models with only pk populated

# 0.4.1

*  add order_by method to queryset to allow sorting
*  update docs

# 0.4.0

*  Changed notation in Model definition -> now use name = ormar.Field() not name: ormar.Field()
    * Note that old notation is still supported but deprecated and will not play nice with static checkers like mypy and pydantic pycharm plugin
*  Type hint docs and test
*  Use mypy for tests also not, only ormar package
*  Fix scale and precision translation with max_digits and decimal_places pydantic Decimal field
*  Update docs - add best practices for dependencies
*  Refactor metaclass and model_fields to play nice with type hints
*  Add mypy and pydantic plugin to docs 
*  Expand the docs on ManyToMany relation

# 0.3.11

* Fix setting server_default as default field value in python

# 0.3.10

* Fix postgresql check to avoid exceptions with drivers not installed if using different backend

# 0.3.9

*  Fix json schema generation as of [#19][#19]
*  Fix for not initialized ManyToMany relations in fastapi copies of ormar.Models
*  Update docs in regard of fastapi use
*  Add tests to verify fastapi/docs proper generation

# 0.3.8

*  Added possibility to provide alternative database column names with name parameter to all fields.
*  Fix bug with selecting related ManyToMany fields with `fields()` if they are empty.
*  Updated documentation

# 0.3.7

*  Publish documentation and update readme

# 0.3.6

*  Add fields() method to limit the selected columns from database - only nullable columns can be excluded.
*  Added UniqueColumns and constraints list in model Meta to build unique constraints on list of columns.
*  Added UUID field type based on Char(32) column type.

# 0.3.5

*  Added bulk_create and bulk_update for operations on multiple objects.

# 0.3.4

Add queryset level methods
*  delete
*  update
*  get_or_create
*  update_or_create

# 0.3.3

*  Add additional filters - startswith and endswith

# 0.3.2

*  Add choices parameter to all fields - limiting the accepted values to ones provided

# 0.3.1

*  Added exclude to filter where not conditions.
*  Added tests for mysql and postgres with fixes for postgres.
*  Rafactors and cleanup.

# 0.3.0

* Added ManyToMany field and support for many to many relations


[#19]: https://github.com/collerek/ormar/issues/19