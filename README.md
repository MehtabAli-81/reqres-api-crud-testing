# ReqRes API CRUD Testing Suite

<p align="center">
  <strong>Reliable REST API validation with Postman, Newman, and structured test documentation</strong>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Postman-API%20Testing-FF6C37?style=for-the-badge&logo=postman&logoColor=white" alt="Postman API Testing" />
  <img src="https://img.shields.io/badge/Newman-CLI%20Runner-FF6C37?style=for-the-badge&logo=postman&logoColor=white" alt="Newman CLI Runner" />
  <img src="https://img.shields.io/badge/API-REST-0A66C2?style=for-the-badge" alt="REST API" />
  <img src="https://img.shields.io/badge/Test%20Coverage-CRUD-2EA44F?style=for-the-badge" alt="CRUD Test Coverage" />
</p>

<p align="center">
  An end-to-end API testing project that validates the user-management lifecycle against the public <a href="https://reqres.in/">ReqRes API</a>.
</p>

---

## Table of Contents

- [About the Project](#about-the-project)
- [Why This Project Matters](#why-this-project-matters)
- [Test Strategy](#test-strategy)
- [Coverage at a Glance](#coverage-at-a-glance)
- [Repository Layout](#repository-layout)
- [Prerequisites](#prerequisites)
- [Quick Start](#quick-start)
- [Run the Tests in Postman](#run-the-tests-in-postman)
- [Run the Tests with Newman](#run-the-tests-with-newman)
- [Assertions and Validation](#assertions-and-validation)
- [Test Data and Environment Configuration](#test-data-and-environment-configuration)
- [Results and Reporting](#results-and-reporting)
- [Troubleshooting](#troubleshooting)
- [Roadmap](#roadmap)
- [Contributing](#contributing)
- [Disclaimer](#disclaimer)
- [License](#license)

## About the Project

This repository demonstrates a maintainable approach to REST API testing using Postman. It validates the complete **CRUD lifecycle** for user resources and combines automated request assertions with a manually maintained test matrix.

The suite is designed for learning, portfolio demonstration, and repeatable local execution. It keeps collection assets, environment settings, and test documentation separate so that each artifact has a clear purpose and can evolve independently.

### What is included

| Asset | Description |
|---|---|
| Postman collection | Ordered user-management requests with automated test scripts |
| Postman environment | Configurable variables, including the shared API base URL |
| Manual test matrix | Test IDs, scenarios, expected outcomes, and execution tracking |
| Project README | Setup, execution, coverage, and maintenance documentation |

## Why This Project Matters

A good API test suite does more than send requests. It makes expected behavior explicit, produces repeatable results, and gives future contributors a clear path to extend coverage.

This project demonstrates the following practical testing capabilities:

- Designing tests around business actions rather than isolated URLs.
- Verifying both successful request execution and expected HTTP semantics.
- Reusing environment variables instead of duplicating configuration.
- Combining automated checks with traceable manual documentation.
- Supporting both GUI-based Postman execution and command-line Newman execution.
- Organizing the repository so that test artifacts remain discoverable and maintainable.

## Test Strategy

The collection follows a focused request flow for user management:

```text
Create user  →  Read user  →  Replace user  →  Partially update user  →  Delete user
   POST            GET              PUT                    PATCH                 DELETE
```

The current suite focuses on the core happy path. Each request is mapped to a documented test case and an expected HTTP status code. The structure is intentionally extensible so negative, boundary, schema, and contract checks can be added without reorganizing the project.

## Coverage at a Glance

| ID | Operation | Method | Endpoint | Expected response |
|---|---|---|---|---|
| `TC_REQRES_001` | Create a user | `POST` | `/api/users` | `201 Created` |
| `TC_REQRES_002` | Retrieve a user | `GET` | `/api/users/2` | `200 OK` |
| `TC_REQRES_003` | Replace user details | `PUT` | `/api/users/2` | `200 OK` |
| `TC_REQRES_004` | Partially update a user | `PATCH` | `/api/users/2` | `200 OK` |
| `TC_REQRES_005` | Delete a user | `DELETE` | `/api/users/2` | `204 No Content` |

### Coverage categories

| Category | Current status | Notes |
|---|---:|---|
| CRUD operations | Complete | Create, read, full update, partial update, and delete are represented |
| Status-code assertions | Included | Requests validate the expected HTTP response status |
| Environment parameterization | Included | Requests use the `{{baseUrl}}` variable |
| Manual test documentation | Included | Available in the Excel test matrix |
| Negative testing | Planned | Invalid payloads and unsupported inputs can be added next |
| Response schema validation | Planned | JSON structure checks can be expanded in the collection |
| CI reporting | Ready to configure | Newman supports command-line and pipeline execution |

## Repository Layout

```text
reqres-api-crud-testing/
├── collections/
│   ├── ReqRes_CRUD_Collection.postman_collection.json
│   └── ReqRes_Environment.postman_environment.json
├── test-documentation/
│   └── ReqRes_API_Manual_Test_Cases.xlsx
└── README.md
```

## Prerequisites

Install or have access to the following before running the suite:

- [Postman](https://www.postman.com/downloads/) 10 or later for interactive execution.
- [Node.js](https://nodejs.org/) and npm if Newman will be used.
- Internet access to reach the ReqRes API.
- Git if the repository will be cloned from a remote source.

## Quick Start

### 1. Clone the repository

```bash
git clone https://github.com/<your-username>/reqres-api-crud-testing.git
cd reqres-api-crud-testing
```

### 2. Confirm the test assets

```bash
ls collections/
ls test-documentation/
```

You should see the Postman collection, the Postman environment, and the Excel test matrix.

## Run the Tests in Postman

1. Open Postman.
2. Select **Import**.
3. Import both JSON files from `collections/`:
   - `ReqRes_CRUD_Collection.postman_collection.json`
   - `ReqRes_Environment.postman_environment.json`
4. Select **ReqRes - Practice** from the environment selector.
5. Confirm that `baseUrl` resolves to:

   ```text
   https://reqres.in
   ```

6. Open **ReqRes - User Management CRUD**.
7. Select **Run collection**.
8. Run the requests sequentially and review the assertion results in the Collection Runner.

> **Important:** Keep the environment selected while running the collection. If `{{baseUrl}}` is unresolved, the requests will not target the expected host.

## Run the Tests with Newman

Newman is Postman’s command-line collection runner. It is useful for repeatable local execution and CI/CD integration.

### Install Newman

```bash
npm install --global newman
```

### Execute the collection

```bash
newman run \
  collections/ReqRes_CRUD_Collection.postman_collection.json \
  --environment collections/ReqRes_Environment.postman_environment.json
```

### Execute with a local HTML report

Install the HTML reporter once:

```bash
npm install --global newman-reporter-htmlextra
```

Then run:

```bash
newman run \
  collections/ReqRes_CRUD_Collection.postman_collection.json \
  --environment collections/ReqRes_Environment.postman_environment.json \
  --reporters cli,htmlextra \
  --reporter-htmlextra-export reports/reqres-api-report.html
```

Create the output directory first if it does not already exist:

```bash
mkdir --parents reports
```

Generated reports should normally be excluded from version control unless the project intentionally stores historical test evidence.

## Assertions and Validation

The collection’s Postman scripts are intended to validate the response produced by each request. At minimum, the suite verifies the expected HTTP status for every CRUD operation.

A mature extension of the current checks would validate the following response characteristics:

| Validation layer | Example check |
|---|---|
| Transport | Expected HTTP status code |
| Headers | Expected content type and required headers |
| Response body | Required fields are present and have the expected types |
| Business behavior | Updated values are returned after `PUT` or `PATCH` |
| Timing | Response completes within an agreed threshold |
| Contract | Response structure matches the documented API contract |

## Test Data and Environment Configuration

The collection uses the environment variable `{{baseUrl}}` rather than embedding the host in every request.

| Variable | Value | Purpose |
|---|---|---|
| `baseUrl` | `https://reqres.in` | Shared host for all API requests |

If the API host changes, update the environment variable once instead of editing every request URL.

Do not commit secrets, access tokens, private URLs, or production credentials to a Postman environment file. Use Postman’s local or secret variable types for sensitive values when they become necessary.

## Results and Reporting

A successful run should show all five documented requests completing with their expected response statuses. For auditability, record execution outcomes in `test-documentation/ReqRes_API_Manual_Test_Cases.xlsx` and attach Newman reports to CI job artifacts when the suite is integrated into a pipeline.

Recommended evidence for each execution includes:

- Collection run timestamp.
- Tool and runtime version.
- Environment name.
- Passed and failed test counts.
- Failure details, including request and response context.
- Generated HTML or JUnit report when applicable.

## Troubleshooting

| Problem | Likely cause | Resolution |
|---|---|---|
| `{{baseUrl}}` is unresolved | The environment is not selected | Select **ReqRes - Practice** before running |
| Requests fail to connect | Network access is unavailable | Verify internet connectivity and retry |
| Expected status does not match | API behavior or test data changed | Inspect the response and confirm the current ReqRes behavior |
| Newman command is not found | Newman is not installed globally or is not on `PATH` | Reinstall Newman or run it through the project’s npm environment |
| Report cannot be written | The `reports/` directory does not exist | Run `mkdir --parents reports` before execution |

## Roadmap

The following improvements would strengthen the suite for a production-style test strategy:

- Add negative tests for missing, empty, and invalid request fields.
- Add response schema validation for every endpoint.
- Add reusable pre-request scripts for generated test data.
- Add environment-specific configuration for local, staging, and production-like targets.
- Add JUnit output for CI test-result publishing.
- Add a GitHub Actions workflow for automated Newman execution.
- Add request/response logging for failed tests only.
- Add collection-level documentation for test data assumptions and execution order.

## Contributing

Contributions are welcome when they improve coverage, reliability, or documentation.

1. Create a feature branch.
2. Add or update the relevant Postman request and test documentation.
3. Verify the collection locally in Postman or Newman.
4. Update this README when execution steps or repository structure change.
5. Open a pull request with a concise summary of the change and test evidence.

Use descriptive commit messages such as:

```text
test: add negative validation for user creation

docs: clarify Newman reporting workflow
```

## Disclaimer

ReqRes is a public practice API intended for learning, demonstrations, and testing. Availability, response data, rate limits, and behavior may change. Confirm the current [ReqRes documentation](https://reqres.in/) before relying on this project for any production decision.

## License

No license has been specified for this repository. Add a `LICENSE` file before distributing or reusing the project publicly.

## References

[1]: https://reqres.in/ "ReqRes API"
[2]: https://www.postman.com/ "Postman API Platform"
[3]: https://www.postman.com/downloads/ "Postman Downloads"
[4]: https://github.com/postmanlabs/newman "Newman Command-Line Collection Runner"
[5]: https://nodejs.org/ "Node.js JavaScript Runtime"
[6]: https://github.com/ "GitHub"
