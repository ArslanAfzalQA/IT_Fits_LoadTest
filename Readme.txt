
## Test Plan Overview
The test plan includes:
1. A POST request to create a user record, with validation of the response and extraction of the `id`.
2. A GET request to retrieve user record with additional validation of the response.


- Use a user-defined variable to set the base URL.
- Implement a transaction controller to group requests.
- Validate responses using assertions.
- Extract dynamic data using a JSON Extractor.
- Simulate a simple load with 1 user sending 1 request per second.

## Setup Instructions

### User-Defined Variables
1. Add a **User Defined Variables** configuration element.
2. Define the base URL:
   - Name: `BASE_URL1`
   - Value: `reqres.in`

### Thread Group
1. Add a **Thread Group** with the following parameters:
   - Number of Threads (users): `1`
   - Ramp-Up Period (seconds): `1`
   - Loop Count: `1`

### HTTP Requests
#### 1. POST Request: Create User
1. Add an **HTTP Request** sampler.
2. Configure:
   - URL: `${BASE_URL}/api/v1/create`
   - Method: `POST`
   - Body Data:
     ```json
     {
  "name": "Arslan",
  "salary": "123",
  "age": "23"
}
     ```
3. Add a **JSON Extractor** to extract the `id` for the created user:
   - JSON Path Expression: "id":"(\d+)" 
   - Reference Name: `extracted_id`
4. Add a **Response Assertion** to validate the response code:
   - Field to Test: Response Code
   - Pattern: `201`

#### 2. GET Request: Retrieve User
1. Add another **HTTP Request** sampler.
2. Configure:
   - URL: `${BASE_URL}/api/users/2
We can use /${extracted_id} at place of 2 if we want to extract data of user which we created. but this sample api is not supporting this.
   - Method: `GET`
3. Add a **Response Assertion** to validate the presence of an email in the response:
   - Field to Test: Text Response
   - Pattern: `email`

### Transaction Controller
1. Add a **Transaction Controller** to group the POST and GET requests for better result analysis.

## Test Execution
1. Save the Test Plan.
2. Run the test by clicking the green **Start** button.
3. View results using the **View Results Tree** listener.