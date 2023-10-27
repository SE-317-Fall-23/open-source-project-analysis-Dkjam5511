# Assignment Submission

## Project Selected: Flask

## I. Introduction
The purpose of this section is to offer a comprehensive description of two specific test cases within Flask. These test cases will be examined to provide a better understanding of how the project's functionality is tested.

## II. Test Case 1: test_bad_request_debug_message
### A. Description
- This test case is designed to validate how the project handles bad requests. It tests the behavior of the application in response to a POST request to the /json endpoint when the request payload is empty, and it's expected to return a 400 Bad Request status.
### B. Gherkin Syntax (if applicable)
- Feature: Handling Bad Requests in Debug Mode

  - Scenario Outline: Verify handling of bad requests with Debug Mode
    Given the Flask application is configured with DEBUG debug
    And TRAP_BAD_REQUEST_ERRORS is set to False
    When a POST request is made to the "/json" endpoint with an empty payload
    Then the response status code should be 400
    And the response should contain "Failed to decode JSON object"

    Examples:
      | debug | contain |
      | ----- | ------- |
      | True  | True    |
      | False | False   |

### C. Test Steps
1. Set the Flask application's DEBUG mode based on the parameterized value (either True or False).
2. Set the Flask application's TRAP_BAD_REQUEST_ERRORS to False.
3. Define a route for the "/json" endpoint that handles POST requests and attempts to parse JSON from the request data but returns None.
4. Make a POST request to the "/json" endpoint with an empty payload (data=None) and specify the content type as "application/json."
5. Verify that the response's status code is 400 (Bad Request).
6. Check whether the response data contains the string "Failed to decode JSON object."
7. Verify that the content check result matches the value of the debug parameter.
### D. Code Segments Under Test
- Identify specific code segments or functions that are being tested in this case.

```Python
 client.post("/json")
```
### E. Initial State
- The Flask application is set up with certain initial configurations, including its DEBUG mode and the TRAP_BAD_REQUEST_ERRORS configuration.
### F. Transition
- Trigger: Sending a POST request to the "/json" endpoint.
- Change in State: This action initiates a POST request to the "/json" endpoint with an empty payload and the specified content type. It triggers the route handling function, which processes the request and generates a response.
### G. Expected State
- The rv.status_code should match the expected 400.
- The boolean variable contains should match the value of debug, ensuring that the response content check behavior corresponds to the DEBUG mode setting.

## III. Test Case 2: test_options_work
### A. Description
- This Python Flask test case is designed to verify and validate the behavior of the application with respect to the HTTP OPTIONS method. 
### B. Gherkin Syntax (if applicable)
- Feature: Verify OPTIONS method behavior for the root URL

    - Scenario: Sending an OPTIONS request to the root URL
    Given the Flask application is running
    And a route is defined for the root URL with methods "GET" and "POST"
    When a client sends an HTTP OPTIONS request to the root URL
    Then the response should include an "Allow" header with the methods "GET", "HEAD", "OPTIONS", and "POST"
    And the response data should be empty
### C. Test Steps
1. Route Definition: Define a route for the root URL ("/") that allows both the "GET" and "POST" HTTP methods. This route is associated with the index function, which returns "Hello World."
2. Request Simulation: Simulate an HTTP OPTIONS request to the root URL ("/") using the Flask test client.
3. Assertions: Check the response from the simulated request for the following:
- Ensure that the "Allow" header in the response includes the methods "GET," "HEAD," "OPTIONS," and "POST."
- Verify that the response data is an empty byte string (b"").
### D. Code Segments Under Test
- Identify specific code segments or functions that are being tested in this case.
```Python
client.open("/", method="OPTIONS")
```
### E. Initial State
The Flask application has a specific route defined for the root URL ("/"). This route is defined with the following characteristics:
- It allows two HTTP methods: "GET" and "POST."
- It is associated with the index function, which returns the string "Hello World" when accessed with the "GET" or "POST" methods.
### F. Transition
- The first significant event is the simulation of an HTTP OPTIONS request to the root URL ("/") of the Flask application. This event involves sending an HTTP OPTIONS request to the specified route using the Flask test client. This request triggers the Flask application to handle the OPTIONS request at the root URL.
### G. Expected State
- The following outcomes are expected as a result of the assertions:
    - The response to the simulated OPTIONS request should include the "Allow" header with the methods "GET," "HEAD," "OPTIONS," and "POST."
    - The response data should be an empty byte string (b"").