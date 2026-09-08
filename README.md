# ReqRes API CRUD Testing Suite

<p align="center">
  <strong>End-to-end REST API testing with Postman and Newman</strong>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Postman-API%20Testing-FF6C37?style=flat-square&logo=postman&logoColor=white" alt="Postman" />
  <img src="https://img.shields.io/badge/Newman-CLI%20Runner-FF6C37?style=flat-square&logo=postman&logoColor=white" alt="Newman" />
  <img src="https://img.shields.io/badge/CRUD-Test%20Suite-2EA44F?style=flat-square" alt="CRUD Test Suite" />
</p>

A lightweight API testing project that validates the **Create, Read, Update, and Delete** operations of the public [ReqRes API](https://reqres.in/).

## What This Project Tests

| Test case | Method | Endpoint | Expected status |
|---|---:|---|---:|
| Create a user | `POST` | `/api/users` | `201 Created` |
| Retrieve a user | `GET` | `/api/users/2` | `200 OK` |
| Update a user | `PUT` | `/api/users/2` | `200 OK` |
| Partially update a user | `PATCH` | `/api/users/2` | `200 OK` |
| Delete a user | `DELETE` | `/api/users/2` | `204 No Content` |

## Project Structure

```text
├── collections/
│   ├── ReqRes_CRUD_Collection.postman_collection.json
│   └── ReqRes_Environment.postman_environment.json
├── test-documentation/
│   └── ReqRes_API_Manual_Test_Cases.xlsx
└── README.md
```

## Run with Postman

1. Clone this repository:

   ```bash
   git clone https://github.com/<your-username>/reqres-api-crud-testing.git
   ```

2. Open Postman and import both JSON files from the `collections/` folder.
3. Select the **ReqRes - Practice** environment.
4. Confirm that `{{baseUrl}}` is set to `https://reqres.in`.
5. Run **ReqRes - User Management CRUD** from the Collection Runner.

## Run with Newman

```bash
npm install -g newman

newman run \
  collections/ReqRes_CRUD_Collection.postman_collection.json \
  -e collections/ReqRes_Environment.postman_environment.json
```

## Highlights

- Covers the complete user CRUD lifecycle.
- Uses environment variables instead of hard-coded URLs.
- Includes automated status-code assertions in Postman.
- Includes a manual test case matrix in Excel.
- Supports both Postman and command-line execution.

## Tools

**Postman · Newman · JavaScript · REST API · Excel · Git**

## Disclaimer

ReqRes is a public practice API. Its availability and behavior may change over time.

## License

No license has been specified for this project.

## References

[1]: https://reqres.in/ "ReqRes API"
[2]: https://www.postman.com/ "Postman API Platform"
[3]: https://github.com/postmanlabs/newman "Newman Command-Line Collection Runner"
