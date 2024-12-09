# Express.js Route Handler Missing Error Handling for Invalid User ID

This repository demonstrates a common error in Express.js route handlers: missing error handling for invalid input parameters.  Specifically, the `/users/:id` route fails to handle cases where the `id` parameter is not a valid integer. This leads to unexpected behavior or crashes if the route attempts to perform an operation (like accessing an array using the invalid ID as an index) that's not designed to handle non-numeric inputs.

## Bug Description

The `bug.js` file showcases the problematic code.  The route attempts to find a user using `parseInt(userId)`. If `userId` is not a number, `parseInt()` returns `NaN`, leading to a failed search and potentially other issues down the line, without a clear error message to the client.

## Solution

The `bugSolution.js` file provides a corrected version.  It includes explicit checks to ensure `userId` is a valid number before attempting to use it.  If it's not a number, or if no user is found, it returns an appropriate HTTP error response (400 Bad Request or 404 Not Found).

## How to Reproduce

1. Clone this repository.
2. Run `npm install express`.
3. Run `node bug.js` and send GET requests with invalid `id` parameters (e.g., `/users/abc`, `/users/-1`, `/users/1.5`) to observe the problem.
4. Run `node bugSolution.js` and repeat the GET requests; observe the improved error handling and appropriate responses.