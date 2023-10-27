## Project Selected: <Enter project name>

## I. Introduction
- The purpose of this section is to detail the different types of testing in Flake and how test data in Flake is generated.

## II. Types of Testing in the Project
## 2. Test Data Generation
### A. Static Test Data
- Flake uses some static data in their tests. Most is for dates and values of expected results from the test or inputs for a test.
Example:
```python
@pytest.mark.parametrize(
    "value", [datetime.datetime(1973, 3, 11, 6, 30, 45), datetime.date(1975, 1, 5)]
)
def test_jsonify_datetime(app, client, value):
    @app.route("/")
    def index():
        return flask.jsonify(value=value)

    r = client.get()
    assert r.json["value"] == http_date(value)
```
### B. Dynamic Test Data
- Flake uses RESTful APIs more most of their tests. Most include a GET from the server and uses POST to manipulate the state of the machine and server.
Example:
```python
@pytest.mark.parametrize("debug", (True, False))
def test_bad_request_debug_message(app, client, debug):
    app.config["DEBUG"] = debug
    app.config["TRAP_BAD_REQUEST_ERRORS"] = False

    @app.route("/json", methods=["POST"])
    def post_json():
        flask.request.get_json()
        return None

    rv = client.post("/json", data=None, content_type="application/json")
    assert rv.status_code == 400
    contains = b"Failed to decode JSON object" in rv.data
    assert contains == debug
```

