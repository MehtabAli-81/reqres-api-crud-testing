# ReqRes API CRUD Testing Suite

A professional API test automation project for validating the complete **Create, Read, Update, and Delete (CRUD)** lifecycle against the public [ReqRes API](https://reqres.in/).

The repository combines a reusable **Postman collection**, a dedicated **Postman environment**, and a structured **manual test case matrix** to demonstrate practical API testing, environment parameterization, and test documentation.

## Project Overview

This project tests user-management workflows through the following HTTP operations:

- **POST** — Create a user
- **GET** — Retrieve a user
- **PUT** — Replace a user record
- **PATCH** — Partially update a user record
- **DELETE** — Delete a user record

The automated collection includes JavaScript assertions for response status codes and response behavior. The accompanying Excel workbook provides a manual test matrix and execution record for traceability.

## Tools and Technologies

| Tool or Technology | Purpose |
|---|---|
| [Postman](https://www.postman.com/) 10+ | API request authoring and collection execution |
| ReqRes API | Public REST API used as the test target |
| JavaScript | Automated assertions in Postman test scripts |
| Microsoft Excel | Manual test case matrix and execution tracking |
| Git and GitHub | Source control and project collaboration |

## Repository Structure

```text
.
├── collections/
│   ├── ReqRes_CRUD_Collection.postman_collection.json
│   └── ReqRes_Environment.postman_environment.json
├── test-documentation/
│   └── ReqRes_API_Manual_Test_Cases.xlsx
└── README.md
```

## Prerequisites

Before running the suite, install or have access to the following:

- [Postman](https://www.postman.com/downloads/) version 10 or later
- Git, if you plan to clone the repository from the command line
- Internet access to reach the ReqRes API

## Getting Started

### 1. Clone the repository

Replace the placeholder URL with the actual repository URL:

```bash
git clone https://github.com/<your-username>/reqres-api-crud-testing.git
cd reqres-api-crud-testing
```

### 2. Import the Postman assets

1. Open Postman.
2. Select **Import**.
3. Import both files from the `collections/` directory:
   - `ReqRes_CRUD_Collection.postman_collection.json`
   - `ReqRes_Environment.postman_environment.json`

### 3. Select and verify the environment

In Postman’s environment selector, choose **ReqRes - Practice**. Confirm that the `baseUrl` variable is configured as follows:

```text
https://reqres.in
```

The collection uses `{{baseUrl}}` rather than hard-coding the API host in every request. This makes the suite easier to maintain and adapt to other environments.

### 4. Run the collection

1. Locate **ReqRes - User Management CRUD** in the Collections sidebar.
2. Select the collection’s **More actions** menu.
3. Choose **Run collection**.
4. Execute the requests sequentially in the Collection Runner.
5. Review the request results and assertion output after the run completes.

## Test Coverage

| Test ID | Method | Endpoint | Scenario | Expected Result |
|---|---:|---|---|---|
| `TC_REQRES_001` | `POST` | `/api/users` | Create a new user record | `201 Created` |
| `TC_REQRES_002` | `GET` | `/api/users/2` | Retrieve an existing user | `200 OK` |
| `TC_REQRES_003` | `PUT` | `/api/users/2` | Replace the user’s details | `200 OK` |
| `TC_REQRES_004` | `PATCH` | `/api/users/2` | Partially update a user field | `200 OK` |
| `TC_REQRES_005` | `DELETE` | `/api/users/2` | Delete the user record | `204 No Content` |

## Quality and Maintainability Features

### Environment parameterization

The collection references `{{baseUrl}}` for the API host. Centralizing this value prevents repeated edits when the target environment changes.

### Automated assertions

Postman test scripts validate expected HTTP status codes and response behavior directly within the collection. These checks provide immediate feedback during manual runs and can be reused in automated execution workflows.

### Separation of test assets

Automated artifacts and manual documentation are stored in separate directories. This keeps execution assets easy to locate while preserving a clear audit trail for test planning and results.

### Reusable test design

Each request represents a focused business action. The collection structure can therefore be extended with additional positive, negative, validation, and boundary test scenarios without changing the existing organization.

## Running the Suite from the Command Line

For command-line execution, install [Newman](https://github.com/postmanlabs/newman), Postman’s command-line collection runner:

```bash
npm install -g newman
```

Run the collection with the exported environment:

```bash
newman run \
  collections/ReqRes_CRUD_Collection.postman_collection.json \
  -e collections/ReqRes_Environment.postman_environment.json
```

Newman is useful for repeatable local runs and for integrating the collection into a CI/CD pipeline.

## Recommended Extensions

The suite can be expanded with additional scenarios, including:

- Missing or malformed request fields
- Unsupported HTTP methods
- Invalid user identifiers
- Response schema validation
- Header and content-type validation
- Authentication and authorization checks, when supported by the target API
- HTML, JSON, or JUnit test reports for CI pipelines

## Test Documentation

The manual test matrix is available at:

```text
test-documentation/ReqRes_API_Manual_Test_Cases.xlsx
```

It complements the automated collection by documenting test identifiers, scenarios, expected results, and execution outcomes.

## Disclaimer

ReqRes is a public practice API intended for learning, demonstrations, and testing. Its behavior, availability, rate limits, and response data may change over time. Always verify the current API documentation before using this project as part of a production workflow.

## License

No license has been specified for this repository. Add a `LICENSE` file before distributing or reusing the project publicly.

## References

[1]: https://reqres.in/ "ReqRes API"
[2]: https://www.postman.com/ "Postman API Platform"
[3]: https://www.postman.com/downloads/ "Postman Downloads"
[4]: https://github.com/postmanlabs/newman "Newman Command-Line Collection Runner"
[5]: https://git-scm.com/ "Git Version Control System"
[6]: https://github.com/ "GitHub"
