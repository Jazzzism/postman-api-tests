# Postman API Test Suite

![api-tests](https://github.com/Jazzzism/postman-api-tests/actions/workflows/api-tests.yml/badge.svg)

Automated REST API tests for the public [JSONPlaceholder](https://jsonplaceholder.typicode.com) service, built in Postman and run from the command line with Newman and in CI with GitHub Actions.

## What is covered
- **Posts:** list, get one, filter by `userId`, create (POST), update (PUT), delete (DELETE)
- **Users:** field validation, email format, nested address data
- **Comments:** query-parameter filtering by `postId`
- **Negative case:** requesting a non-existent post returns 404

Every request checks status code, response time (< 5000 ms) and content type. Response bodies are validated for required fields and values. The first request saves a post id to a collection variable that later requests reuse (request chaining).

## Project structure
```
collections/    Postman collection (v2.1)
environments/   Environment with the baseUrl variable
.github/        CI workflow
package.json    Newman and report dependencies
```

## Run in Postman
1. Import both JSON files from `collections/` and `environments/`.
2. Select the **JSONPlaceholder** environment.
3. Open the collection, click **Run**, and keep the request order.

## Run with Newman
Requires Node.js 18 or newer.
```bash
npm install
npm test
```
The HTML report is written to `reports/report.html`.

## CI
GitHub Actions runs the collection on every push and pull request and uploads the HTML report as a build artifact.

## Notes
JSONPlaceholder is a fake API: writes are simulated and not saved, so POST, PUT and DELETE responses are validated for correct status and echoed data only.
