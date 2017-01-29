# sanic_crud

sanic_crud is a REST API framework for creating a CRUD (Create/Retrieve/Update/Delete) API using [Sanic](https://github.com/channelcat/sanic) and [PeeWee](http://docs.peewee-orm.com/en/latest/)
You can use sanic_crud to automatically create an API from your PeeWee models, see how it works in the [Documentation](docs/using_a_sanic_crud_api.md)

Contributions to the repository are welcome!

### Example

  ```python
    from peewee import CharField, DateTimeField, SqliteDatabase, Model
    import datetime
    from sanic import Sanic
    from sanic_crud import generate_crud
    
    db = SqliteDatabase('my_app.db')
    
    class BaseModel(Model):
        class Meta:
            database = db
    
    class Person(BaseModel):
        name = CharField()
        email = CharField()
        create_datetime = DateTimeField(default=datetime.datetime.now, null=True)
    
    db.create_tables([Person])
    
    app = Sanic(__name__)
    generate_crud(app, [Person])
    app.run(host="0.0.0.0", port=8000, debug=True)
  ```

### Installation

-  `python -m pip install sanic_crud`

### Documentation

Documentation can be found in the ``docs`` directory.


### TODO
* Write tests
* Get working with travis-ci
* Add support for custom routes per model
* Make int/string length validation better
* Add documentation for developing