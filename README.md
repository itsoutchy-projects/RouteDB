![PyPI - Version](https://img.shields.io/pypi/v/RouteDB)

# RouteDB
RouteDB is a package built for managing databases locally. Its path hierarchy is simple and easy to use

To install run:
```
pip install RouteDB
```

## How to use
If you're not sure, check out this neat demonstration to learn the basics.

### Creating a Database
To create a Database, you'll need to provide 2 parameters: `path` and `types` to the `Database()` constructor.

Types is necessary to manage the data that flows into a route and makes sure that the type stays consistent.

Make it into a dictionary which looks something like this:
```python
types = {
    "string": str
}
```
Put the key as the name you want to use to refer to the type, and then as the value put the type, so something like `str`, or `float`. Do not try to convert it to anything, just put it into the dictionary.

### Adding a route
Adding a route is simple, you pass the name and the type (the name of a type that you put earlier) to the `addRoute()` method. Don't worry about whether the route's path exists or not, as we make it for you.  
Example:
```python
db.addRoute("my awesome route", "string")
```

### Writting data to a route
Finally, we'll write some data to the route, it's simple as long as you make the type of the data match the type of the route. Pass the data, the route, and the name of the data  
Example:
```python
db.write(f"hello world! from {datetime.datetime.now().strftime("%d/%m/%Y, %H:%M:%S")} :D", "my awesome route", f"user1")
```

## Demos
Here we have a simple demo which demonstrates how you can add a route (which makes a new folder if it exists), and how you can write data to one:
```python
import RouteDB
import datetime
import os

types = {
    "string": str
}
db = RouteDB.Database("db", types)
route = "my amazing route aaaaaaaaaaaaaa"

print(db.addRoute(route, "string"))
thisIdx = len(os.listdir(db.routeDir(route))) + 1
db.write(f"hello world! from {datetime.datetime.now().strftime("%d/%m/%Y, %H:%M:%S")} :D", route, f"user{thisIdx}")
print(db.getData(route, f"user{thisIdx}"))
```