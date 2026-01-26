# REST API Design Standards

This document defines organization-wide standards for designing and maintaining REST APIs. Its purpose is to ensure consistency, reliability, and long-term maintainability of REST APIs, while reducing ambiguity for both API consumers and engineers.


---

## Table of Contents

- [0. Purpose and Scope](#0-purpose-and-scope)
  - [Goals of this standard](#goals-of-this-standard)
  - [Who this document applies to](#who-this-document-applies-to)
  - [What is intentionally out of scope](#what-is-intentionally-out-of-scope)

- [1. API Design Principles](#1-api-design-principles)
  - [Core design principles](#core-design-principles)
    - [1.1 Consistency over perfection](#11-consistency-over-perfection)
    - [1.2 APIs are contracts](#12-apis-are-contracts)
    - [1.3 Explicit over implicit](#13-explicit-over-implicit)
    - [1.4 Fail fast and fail clearly](#14-fail-fast-and-fail-clearly)
    - [1.5 Design for evolution](#15-design-for-evolution)
  - [Trade-offs and priorities](#trade-offs-and-priorities)
  - [Consistency and backward compatibility](#consistency-and-backward-compatibility)

- [2. Resource Modeling](#2-resource-modeling)
  - [Resource naming conventions](#resource-naming-conventions)
  - [Singular vs plural resources](#singular-vs-plural-resources)
  - [Nested resources and relationships](#nested-resources-and-relationships)
  - [URL structure guidelines](#url-structure-guidelines)
  - [Response structure depth](#response-structure-depth)

- [3. HTTP Methods Usage](#3-http-methods-usage)
  - [GET](#get)
  - [POST](#post)
  - [PUT](#put)
  - [PATCH](#patch)
  - [DELETE](#delete)
  - [Idempotency expectations](#idempotency-expectations)

- [4. HTTP Status Codes Policy](#4-http-status-codes-policy)
  - [Success responses](#success-responses)
  - [Client error responses](#client-error-responses)
  - [Authorization and authentication errors](#authorization-and-authentication-errors)
  - [Conflict and validation errors](#conflict-and-validation-errors)
  - [Server errors](#server-errors)

- [5. Error Response Format](#5-error-response-format)
  - [Standard error structure](#standard-error-structure)
  - [Error codes](#error-codes)
  - [Human-readable messages](#human-readable-messages)
  - [Trace and correlation identifiers](#trace-and-correlation-identifiers)

- [6. Validation and Input Handling](#6-validation-and-input-handling)
  - [Request validation rules](#request-validation-rules)
  - [Validation vs business logic](#validation-vs-business-logic)
  - [Partial updates](#partial-updates)
  - [Consistent validation error responses](#consistent-validation-error-responses)

- [7. Pagination, Filtering, and Sorting](#7-pagination-filtering-and-sorting)
  - [Pagination strategy](#pagination-strategy)
  - [Pagination approaches](#pagination-approaches)
  - [Pagination metadata](#pagination-metadata)
  - [Default limits and boundaries](#default-limits-and-boundaries)
  - [Filtering conventions](#filtering-conventions)
  - [Sorting conventions](#sorting-conventions)

- [8. Versioning Strategy](#8-versioning-strategy)
  - [When versioning is required](#when-versioning-is-required)
  - [Versioning approaches](#versioning-approaches)
  - [Backward compatibility rules](#backward-compatibility-rules)
  - [Deprecation process](#deprecation-process)

- [9. Idempotency and Retries](#9-idempotency-and-retries)
  - [Idempotent operations](#idempotent-operations)
  - [Idempotency keys](#idempotency-keys)
  - [Retry behavior](#retry-behavior)
  - [Client responsibilities](#client-responsibilities)

- [10. Authentication and Authorization (High-Level)](#10-authentication-and-authorization-high-level)
  - [Authentication enforcement points](#authentication-enforcement-points)
  - [Authorization checks](#authorization-checks)
  - [Error handling for access control](#error-handling-for-access-control)

- [11. Observability and Debugging](#11-observability-and-debugging)
  - [Request identifiers](#request-identifiers)
  - [Correlation across services](#correlation-across-services)
  - [Logging expectations](#logging-expectations)
  - [Error transparency](#error-transparency)

- [12. Backward Compatibility and Deprecation](#12-backward-compatibility-and-deprecation)
  - [Breaking vs non-breaking changes](#breaking-vs-non-breaking-changes)
  - [Communication of changes](#communication-of-changes)
  - [Deprecation timelines](#deprecation-timelines)

- [13. API Documentation](#13-api-documentation)

- [14. Common Anti-Patterns](#14-common-anti-patterns)
  - [Inconsistent status codes](#inconsistent-status-codes)
  - [Leaking internal errors](#leaking-internal-errors)
  - [Ambiguous resource design](#ambiguous-resource-design)
  - [Silent breaking changes](#silent-breaking-changes)
  - [Overloaded endpoints](#overloaded-endpoints)

- [15. Exceptions and Governance](#15-exceptions-and-governance)
  - [When exceptions are allowed](#when-exceptions-are-allowed)
  - [How exceptions are documented](#how-exceptions-are-documented)
  - [Decision ownership](#decision-ownership)

---

## 0. Purpose and Scope

### Goals of this standard

The primary goals of these REST API design standards are to:

- Ensure consistent REST API behavior across all services and teams
- Reduce ambiguity for API consumers (frontend, mobile, internal services, partners)
- Improve long-term maintainability and evolvability of REST APIs
- Minimize breaking changes and unexpected API behavior
- Simplify onboarding of new engineers working with REST APIs
- Enable reliable monitoring, debugging, and incident response

### Who this document applies to

These standards apply to:

- All backend services exposing REST APIs
- Internal REST APIs used between services
- Public and partner-facing REST APIs
- Engineers designing or modifying REST API contracts
- Tech Leads and Engineering Managers responsible for API quality and consistency

Following these standards is expected by default.

### What is intentionally out of scope

This document does not cover:

- Business-specific API logic and workflows
- Framework or language-specific implementation details
- Database schema design
- API styles other than REST (e.g. GraphQL, gRPC, event-driven APIs)
- Authentication and authorization implementation details (only high-level behavioral rules are included)

---

## 1. API Design Principles

### Core design principles

All REST APIs should follow these core principles:

#### 1.1 Consistency over perfection

- Similar resources should behave in similar ways
- Naming, error formats, pagination, and status codes must be consistent across services
- A slightly imperfect but consistent API is preferable to a perfectly designed but inconsistent one

#### 1.2 APIs are contracts

- API behavior is a contract with its consumers
- Changes must be made with backward compatibility in mind
- Breaking changes should be avoided whenever possible and explicitly managed when required

#### 1.3 Explicit over implicit

- API behavior should be clear and predictable
- Avoid hidden logic or side effects
- Validation rules, errors, and state transitions should be transparent

#### 1.4 Fail fast and fail clearly

- Invalid requests should be rejected as early as possible
- Error responses must clearly explain what went wrong
- Do not hide errors behind generic success responses

#### 1.5 Design for evolution

- APIs should be designed to evolve without breaking existing clients
- Prefer additive changes over modifying existing behavior
- Plan for versioning and deprecation from the beginning

---

### Trade-offs and priorities

When designing REST APIs, the following priorities should guide decisions:

1. Consumer experience over internal convenience  
2. Long-term maintainability over short-term speed  
3. Consistency across services over local optimization  
4. Backward compatibility over perfect design  

In case of conflict between priorities, decisions should favor:

- Stability for existing consumers
- Clear and predictable behavior
- Simpler mental models

---

### Consistency and backward compatibility

Consistency and backward compatibility are mandatory design goals:

- Once an API contract is published, it should not be broken without a formal deprecation process
- Existing fields and behaviors must continue to work as originally defined
- New functionality should be added in a backward-compatible manner

Examples of backward-compatible changes:

- Adding new optional fields
- Adding new endpoints
- Extending enum values (when safely handled)

Examples of breaking changes:

- Removing fields or endpoints
- Changing field types or meanings
- Changing validation rules that reject previously valid requests
- Modifying error formats or status codes

Breaking changes require:

- Explicit versioning
- Clear communication
- Migration support when possible

---

## 2. Resource Modeling

### Resource naming conventions

Resources must be represented as nouns describing domain entities.

Guidelines:

- Use plural nouns for resource collections  
- Use lowercase letters with hyphens for multi-word names  
- Avoid verbs in resource names  
- Keep names simple and domain-oriented  

Examples:

**Correct:**

```text
/users
/orders
/payment-methods
/subscriptions
```

**Incorrect:**

```text
/getUser
/create-order
/userList
/processPayment
```

### Singular vs plural resources

- Use plural form for collections:

```text
/users
/orders
```

- Use identifiers to access a single resource:

```text
/users/{userId}
/orders/{orderId}
```

- Avoid singular resource names unless representing a unique singleton resource.  Acceptable singleton examples:

```text
/health
/status
/configuration
```

### Nested resources and relationships

Nested resources should reflect clear ownership or strong relationships.

Use nesting when:
- A resource cannot exist without its parent
- The relationship is conceptually hierarchical

Examples:

```text
/users/{userId}/orders
/orders/{orderId}/items
```

Avoid deep nesting (more than two levels), as it increases complexity and reduces readability.

Avoid:

```text
/users/{userId}/orders/{orderId}/items/{itemId}
```

Prefer flatter structures with references when relationships are complex.

### URL structure guidelines

- URLs should represent resources, not actions
- Structure should be predictable and readable
- Avoid query parameters for resource identification

Guidelines:

- Use path parameters for resource identity
- Use query parameters for filtering and pagination
- Do not expose internal implementation details in URLs

Examples:

**Good:**

```text
/orders/{orderId}
/orders?status=completed&limit=20
```

**Bad:**

```text
/getOrderById?id=123
/orderService/findOrder
```

### Response structure depth

API responses should avoid excessive nesting.

Guidelines:

- Prefer flat structures where possible
- Avoid more than two levels of nesting unless strongly justified
- Do not embed dynamic collections inside resource objects

Example to avoid:

```text
A wallet object containing a full list of transactions.
```

Instead:

```text
Expose related collections via dedicated endpoints:
GET /wallets/{id}/transactions
```


---

## 3. HTTP Methods Usage

Each HTTP method must be used according to its semantic meaning. Incorrect usage of methods leads to unclear API semantics and unpredictable behavior.

### GET

Use `GET` to retrieve resources without causing side effects.

Rules:

- Must not modify server state
- Must be safe and idempotent
- Should return appropriate status codes when resources are missing

Examples:

```text
GET /users
GET /users/{userId}
GET /orders?status=completed
```

Avoid:

- Using GET for actions or state changes
- Passing sensitive data in query parameters

### POST

Use `POST` to create new resources or trigger non-idempotent operations.

Rules:

- Typically used to create a new resource in a collection
- May be used for complex operations that do not fit CRUD semantics
- Is not idempotent by default

Examples:

```text
POST /users
POST /orders
```

Avoid:

- Using POST for simple updates
- Overloading POST for every operation

### PUT

Use `PUT` to fully replace an existing resource.

Rules:

- Must be idempotent
- The full resource representation should be provided
- Missing fields may be overwritten or reset

Examples:

```text
PUT /users/{userId}
PUT /orders/{orderId}
```

Avoid:

- Partial updates with PUT (use PATCH instead)
- Using PUT for resource creation unless explicitly intended

### PATCH

Use `PATCH` to partially update a resource.

Rules:

- Used for modifying one or more fields
- Should be idempotent when possible
- Only changed fields should be sent

Examples:

```text
PATCH /users/{userId}
PATCH /orders/{orderId}
```

Avoid:

- Sending full resource payloads unnecessarily
- Mixing PATCH semantics with PUT behavior

### DELETE

Use `DELETE` to remove a resource.

Rules:

- Must be idempotent
- Should return appropriate status codes when resource does not exist
- Deletions should be explicit and predictable

Examples:

```text
DELETE /users/{userId}
DELETE /orders/{orderId}
```

Avoid:

- Using DELETE for soft actions without clear semantics
- Hiding delete operations behind POST requests

### Idempotency expectations

Method idempotency expectations:

- GET — idempotent
- PUT — idempotent
- PATCH — ideally idempotent
- DELETE — idempotent
- POST — not idempotent by default

Guidelines:

- Retried requests should not cause unintended side effects
- For non-idempotent operations that may be retried, consider using idempotency keys
- Document idempotent behavior clearly in API contracts

---

## 4. HTTP Status Codes Policy

HTTP status codes must accurately reflect the outcome of each request.
They represent the technical result of the operation and must not be used to encode business logic.

Avoid returning `200 OK` for error scenarios, even if an error code or error details are included in the response body.

### Success responses

Use the following status codes for successful operations:

- `200 OK` — Successful retrieval or update of a resource  
- `201 Created` — Resource successfully created  
- `204 No Content` — Successful operation with no response body (e.g. delete)  

Examples:

```text
GET /users/{userId} -> 200 OK
POST /users -> 201 Created
DELETE /users/{userId} -> 204 No Content
```

### Client error responses

Use client error codes when the request is invalid or cannot be processed as sent.

Common cases:

- `400 Bad Request` — Malformed request or invalid parameters
- `404 Not Found` — Requested resource does not exist
- `405 Method Not Allowed` — Unsupported HTTP method for the endpoint

Examples:

```text
GET /users/invalid-id -> 400 Bad Request
GET /users/99999 -> 404 Not Found
POST /users/{userId} -> 405 Method Not Allowed
```

### Authorization and authentication errors

Use dedicated status codes for access control issues:

- `401 Unauthorized` — Authentication is missing or invalid
- `403 Forbidden` — Authenticated but not allowed to access the resource

Guidelines:

- Do not expose sensitive authorization logic
- Use `403` when user is authenticated but lacks permission
- Use `401` when authentication is required or failed

Examples:

```text
GET /orders -> 401 Unauthorized
GET /admin/users -> 403 Forbidden
```

### Conflict and validation errors

Use specific codes to represent business and state conflicts:

- `409 Conflict` — Resource state conflicts with the request
- `422 Unprocessable Entity` — Validation errors (optional, if adopted consistently)

Typical cases:

- Duplicate resource creation
- State transition conflicts
- Business rule violations

Examples:

```text
POST /users with existing email -> 409 Conflict
PATCH /orders/{id} with invalid status -> 422 Unprocessable Entity
```

### Server errors

Use server error codes for unexpected failures:

- `500 Internal Server Error` — Generic server failure
- `502 Bad Gateway` — Upstream dependency failure
- `503 Service Unavailable` — Temporary unavailability

Guidelines:

- Do not expose internal error details in responses
- Always log full error context internally
- Return standardized error response format (see section 5)

Examples:
```text
GET /users -> 500 Internal Server Error
POST /orders -> 503 Service Unavailable
```

---

## 5. Error Response Format

All REST APIs must return errors using a standardized response structure. The error format must be consistent across all services to ensure predictable client behavior, simplified debugging, and reliable monitoring.

### Standard error structure

Each error response must follow this structure:

```json
{
  "error": {
    "code": "RESOURCE_NOT_FOUND",
    "message": "The requested user does not exist.",
    "details": [],
    "traceId": "abc123xyz"
  }
}
```

Fields description:

- `code` — machine-readable error identifier
- `message` — human-readable description of the error
- `details` — optional array with additional error information (e.g. validation issues)
- `traceId` — unique identifier for request tracing and debugging


### Error codes

Error codes must:

- Be uppercase with underscores
- Be stable and not change over time
- Represent error categories clearly
- Be independent of HTTP status codes

Examples:

```text
INVALID_REQUEST
RESOURCE_NOT_FOUND
UNAUTHORIZED_ACCESS
VALIDATION_FAILED
RESOURCE_CONFLICT
INTERNAL_ERROR
```

Guidelines:

- Do not expose internal system details in error codes
- Group similar errors under consistent naming patterns
- Document error codes when APIs are public or shared


### Human-readable messages

Error messages must:

- Clearly describe what went wrong
- Be understandable without technical knowledge
- Avoid exposing sensitive system information
- Not depend on internal implementation details

Examples:

**Good:**

```text
"User with the provided email already exists."
"Order cannot be cancelled in its current state."
```

**Bad:**

```text
"NullPointerException occurred"
"Database constraint violation"
```

### Trace and correlation identifiers

Each error response must include a trace or correlation identifier:

- Used to track requests across services
- Enables faster debugging and incident investigation
- Must be logged internally with full context

Guidelines:

- Use a single `traceId` field consistently
- Generate a new identifier if none is provided by upstream systems
- Propagate trace identifiers across service boundaries

---

## 6. Validation and Input Handling

All incoming requests must be validated consistently before business logic execution.

Validation ensures data correctness, protects services from invalid input,
and provides clear feedback to API consumers.

### Request validation rules

Validation must be applied to:

- Required fields presence
- Data types and formats
- Value ranges and constraints
- Enum and allowed value sets
- Request structure and nesting

Guidelines:

- Reject invalid requests as early as possible
- Do not rely on downstream systems for validation
- Keep validation logic explicit and maintainable

Examples of typical validations:

- Required parameters missing  
- Invalid email or date format  
- Negative values where not allowed  
- Exceeding maximum length  

### Validation vs business logic

Validation errors and business rule violations must be clearly separated.

Validation covers:

- Data format and structure correctness
- Required fields
- Type and constraint checks

Business logic covers:

- State transitions
- Domain-specific rules
- Cross-entity constraints

Guidelines:

- Use validation errors for malformed or invalid input  
- Use business errors for domain rule violations  
- Map validation errors to appropriate client error status codes  

### Partial updates

For partial updates (using `PATCH`):

- Only provided fields should be validated and updated  
- Unspecified fields must remain unchanged  
- Validation rules must still apply to modified fields  

Guidelines:

- Do not require full resource payload for partial updates  
- Validate only the fields included in the request  
- Ensure consistent behavior across all PATCH endpoints  

### Consistent validation error responses

Validation errors must follow the standardized error response format (see section 5).

When multiple validation errors occur:

- Return all relevant validation issues in a single response
- Include field-level details when applicable

Example structure:

```json
{
  "error": {
    "code": "VALIDATION_FAILED",
    "message": "One or more fields are invalid.",
    "details": [
      {
        "field": "email",
        "issue": "Invalid format"
      },
      {
        "field": "age",
        "issue": "Must be greater than 0"
      }
    ],
    "traceId": "abc123xyz"
  }
}
```

---

## 7. Pagination, Filtering, and Sorting

All collection endpoints must support pagination and follow consistent
filtering and sorting conventions to ensure predictable behavior and performance.

### Pagination strategy

Pagination must be applied to all endpoints returning collections.

Recommended approach:

- Offset-based pagination using `limit` and `offset`

Parameters:

- `limit` — number of items to return  
- `offset` — starting position in the collection  

Example:

```text
GET /orders?limit=20&offset=40
```

Guidelines:

- Always enforce a maximum limit to prevent large responses
- Provide reasonable default values when not specified
- Return pagination metadata when applicable

Optional metadata example:

```json
{
  "data": [],
  "pagination": {
    "limit": 20,
    "offset": 40,
    "total": 235
  }
}
```

### Pagination approaches

Two pagination approaches may be supported:

- Offset-based pagination (`limit`, `offset`)
- Page-based pagination (`page`, `size`)

Guidelines:

- APIs must never return full collections by default
- Reasonable defaults must always be enforced
- Large unbounded responses are not allowed

Example (page-based):
```text
GET /wallets?page=0&size=25
```

### Pagination metadata

Pagination metadata may be provided either in the response body or via HTTP headers. When using headers, custom fields should be prefixed with `X-`.

Examples:

```text
X-Total-Count: 235  
X-Total-Pages: 27  
```

Guidelines:

- Metadata must be consistent across services
- Do not mix multiple metadata formats within the same API

### Default limits and boundaries

Default pagination values should be defined globally.

Recommended defaults:

- Default `limit`: 20
- Maximum `limit`: 100

Guidelines:

- Reject requests exceeding maximum limits or cap them automatically
- Document default and maximum values clearly
- Ensure consistent behavior across all endpoints

### Filtering conventions

Filtering must be implemented using query parameters.

Guidelines:

- Use clear and domain-oriented field names
- Support multiple filters where appropriate
- Avoid complex filtering syntax when possible

Examples:

```text
GET /orders?status=completed
GET /users?role=admin&active=true
```

Avoid:

- Embedding filters in path segments
- Using cryptic or abbreviated parameter names

### Sorting conventions

Sorting must be implemented using a `sort` query parameter.

Recommended format:

- `sort=field` for ascending order
- `sort=-field` for descending order

Examples:

```text
GET /orders?sort=createdAt
GET /orders?sort=-createdAt
```

Guidelines:

- Allow sorting only on indexed or safe fields
- Document supported sorting fields
- Apply default sorting when none is specified

---

## 8. Versioning Strategy

REST APIs must be designed to evolve over time while minimizing breaking changes.
Versioning should be used only when backward compatibility cannot be preserved.

### When versioning is required

Versioning is required when changes are breaking for existing API consumers.

Examples of breaking changes:

- Removing or renaming endpoints
- Removing or renaming fields
- Changing field data types
- Changing required fields
- Modifying validation rules that reject previously valid requests
- Changing response structures or error formats

Examples of non-breaking changes:

- Adding new optional fields
- Adding new endpoints
- Extending enum values (when safely handled)

Guideline:

- Prefer backward-compatible changes whenever possible
- Introduce a new API version only as a last resort

### Versioning approaches

The preferred versioning approach is URL-based versioning.

Example:

```text
/v1/users
/v2/users
```

Alternative approaches (if explicitly approved):

- Header-based versioning
- Media type versioning

Guidelines:

- Use simple numeric versions (v1, v2, v3)
- Avoid embedding version in query parameters
- Apply versioning consistently across all endpoints

### Backward compatibility rules

Backward compatibility must be preserved within the same API version.

Rules:

- Existing endpoints must continue to work as documented
- Existing fields must retain their original meaning and type
- Newly added fields must be optional by default
- Deprecated fields must continue to function until officially removed

Breaking changes within the same version are not allowed.

### Deprecation process

When an API version or feature must be retired:

1. Mark the feature or version as deprecated in documentation
2. Communicate deprecation to all consumers
3. Provide a migration path when possible
4. Maintain deprecated functionality for an agreed period
5. Remove deprecated functionality after sunset date

Guidelines:

- Deprecation timelines should be clearly defined
- Critical APIs should allow longer migration windows
- Track deprecated usage where possible

---

## 9. Idempotency and Retries

REST APIs must be designed to safely handle repeated requests without causing unintended side effects.
Idempotency ensures reliability in the presence of network failures, timeouts, and retries.

### Idempotent operations

The following HTTP methods must be idempotent by design:

- GET  
- PUT  
- DELETE  

PATCH should be idempotent whenever possible.

Rules:

- Repeating the same request must result in the same final state  
- Duplicate requests must not create duplicate resources  
- Side effects must be predictable  

Examples:

- Repeating `PUT /users/{id}` should always result in the same user state  
- Repeating `DELETE /orders/{id}` should not cause errors after the first successful deletion  

### Idempotency keys

For non-idempotent operations (primarily `POST`), idempotency keys should be supported when retries are possible.

Guidelines:

- Clients may send an `Idempotency-Key` header with a unique value  
- The server must store and reuse the result for repeated requests with the same key  
- The key should have a reasonable expiration period  

Example:

```text
POST /orders
Idempotency-Key: 123e4567-e89b-12d3-a456-426614174000
```

### Retry behavior

APIs should be designed to handle retries safely.

Guidelines:

- Clients may retry requests on network failures or server errors (5xx)
- Retries must not cause duplicate side effects
- Idempotent operations should be safe to retry by default

Avoid:

- Retrying non-idempotent requests without idempotency keys
- Retrying indefinitely without backoff

### Client responsibilities

API consumers are responsible for:

- Implementing retry logic with exponential backoff when appropriate
- Using idempotency keys for non-idempotent operations
- Handling duplicate responses gracefully

Servers should clearly document retry-safe behavior for each endpoint.

---

## 10. Authentication and Authorization (High-Level)

All REST APIs must enforce authentication and authorization consistently
to protect resources and ensure proper access control.
This section defines behavioral expectations rather than implementation details.


### Authentication enforcement points

Authentication must be enforced:

- At the API gateway or service entry point where applicable  
- Before any business logic is executed  
- For all endpoints unless explicitly marked as public  

Guidelines:

- Public endpoints must be clearly documented  
- Authentication checks must be centralized when possible  
- Requests without valid authentication must be rejected immediately  

Typical behavior:

- Missing or invalid credentials → `401 Unauthorized`  

### Authorization checks

Authorization determines whether an authenticated client is allowed to perform an action.

Rules:

- Authorization must be checked for every protected resource  
- Access should be evaluated based on roles, permissions, or ownership  
- Do not rely on client-side enforcement  

Guidelines:

- Apply least-privilege principle  
- Avoid hardcoding permissions in business logic  
- Centralize authorization rules where possible  

Typical behavior:

- Authenticated but not allowed → `403 Forbidden`  

### Error handling for access control

Access control errors must follow standardized behavior:

- Use `401 Unauthorized` for authentication failures  
- Use `403 Forbidden` for authorization failures  
- Do not expose sensitive access control details in error messages  

Examples:

```text
GET /orders without token -> 401 Unauthorized
DELETE /orders/{id} without permission -> 403 Forbidden
```

---

## 11. Observability and Debugging

REST APIs must provide sufficient observability to support monitoring,
debugging, and incident investigation across services.
Consistent tracing and logging are required to ensure system reliability.

### Request identifiers

Each incoming request must be associated with a unique request or trace identifier.

Guidelines:

- Accept request identifiers from upstream systems when provided  
- Generate a new identifier when none is present  
- Include the identifier in all responses (especially error responses)  

Example header:

```text
X-Request-Id: abc123xyz
```

### Correlation across services

Request identifiers must be propagated across all internal service calls.

Guidelines:

- Use the same trace or correlation ID throughout the request lifecycle
- Pass identifiers through HTTP headers or metadata
- Ensure all services log the same identifier

This enables:

- End-to-end request tracing
- Faster root cause analysis
- Cross-service debugging

### Logging expectations

Each API request should generate structured logs containing:

- Request identifier
- Endpoint and HTTP method
- Response status code
- Execution time
- Error details when applicable

Guidelines:

- Use structured (machine-readable) logs
- Avoid logging sensitive data
- Log at appropriate levels (info, warning, error)

### Error transparency

Error responses should provide enough information to help clients understand failures without exposing internal system details.

Guidelines:

- Provide clear, standardized error codes and messages
- Avoid leaking stack traces or internal implementation details
- Log full technical error context internally

Client-facing errors must remain stable and predictable.

---

## 12. Backward Compatibility and Deprecation

REST APIs must prioritize stability for existing consumers while allowing controlled evolution. Backward compatibility is the default expectation. Breaking changes should be rare and explicitly managed.

### Breaking vs non-breaking changes

Non-breaking changes (preferred):

- Adding new optional fields  
- Adding new endpoints  
- Extending enum values when safely handled  
- Adding new query parameters with defaults  

Breaking changes (require versioning or deprecation):

- Removing or renaming fields  
- Removing or renaming endpoints  
- Changing field data types or semantics  
- Making optional fields required  
- Modifying validation rules that reject previously valid requests  
- Changing response or error formats  

Guideline:

- Always favor non-breaking changes whenever possible  

### Communication of changes

All API changes must be communicated clearly to consumers.

Guidelines:

- Document changes in API documentation or changelog  
- Highlight breaking changes explicitly  
- Provide migration guidance when applicable  
- Notify consumers ahead of major changes  

Recommended channels:

- Release notes  
- Developer documentation  
- Direct notifications for critical APIs  

### Deprecation timelines

When deprecating APIs or features:

- Define a clear deprecation start date  
- Provide a sunset date for removal  
- Allow sufficient time for migration  

Recommended minimum timelines:

- Minor features: 1–3 months  
- Major endpoints or versions: 3–12 months  

Guidelines:

- Critical APIs should allow longer migration periods  
- Track usage of deprecated functionality when possible  
- Avoid abrupt removals without notice  

---

## 13. API Documentation

All REST APIs must be documented using a standardized API documentation tool (e.g. OpenAPI / Swagger).

Guidelines:

- API contracts must be documented and kept up to date
- Documentation should be generated automatically when possible
- Public APIs may expose documentation publicly
- Internal APIs should restrict documentation access in production environments

---

## 14. Common Anti-Patterns

The following anti-patterns commonly lead to unstable APIs, poor developer experience, and increased maintenance costs. They must be avoided.

### Inconsistent status codes

Using different status codes for the same type of outcome across endpoints or services.

Examples:

- Returning `200 OK` for errors in some APIs and `4xx/5xx` in others  
- Using `400` for missing resources instead of `404`  

Impact:

- Confuses API consumers  
- Complicates client-side error handling  
- Makes monitoring unreliable  

### Leaking internal errors

Exposing internal system details in API responses.

Examples:

- Stack traces in response body  
- Database or framework error messages  
- Internal service names  

Impact:

- Security risks  
- Poor user experience  
- Tight coupling to internal implementation  

---

### Ambiguous resource design

Designing endpoints that mix multiple responsibilities or unclear resource meaning.

Examples:

```text
/processOrder
/userActions
/handlePayment
```

Impact:

- Difficult to understand API behavior
- Hard to evolve without breaking changes
- Encourages misuse of HTTP methods

### Silent breaking changes

Introducing breaking changes without proper versioning or communication.

Examples:

- Removing fields without notice
- Changing response structure silently
- Tightening validation unexpectedly

Impact:

- Client applications break unexpectedly
- Loss of trust in API reliability
- Increased support overhead

### Overloaded endpoints

Using a single endpoint to perform multiple unrelated operations.

Examples:

```text
POST /actions
POST /execute
```

Impact:

- Hard to document and maintain
- Unclear behavior
- Difficult to secure and monitor

---

## 15. Exceptions and Governance

While these REST API standards are expected to be followed by default, there are cases where deviations may be necessary. This section defines how exceptions are handled to maintain consistency without blocking innovation or practical constraints.

### When exceptions are allowed

Exceptions may be allowed in the following cases:

- Legacy systems that cannot be immediately refactored  
- External dependencies imposing incompatible constraints  
- Performance or scalability requirements requiring alternative approaches  
- Transitional phases during migrations or major refactors  

Guidelines:

- Exceptions should be rare and well-justified  
- Standards remain the default expectation  
- Exceptions must not become permanent without review  


### How exceptions are documented

All exceptions must be explicitly documented.

Documentation should include:

- The specific standard being violated  
- Reason for the exception  
- Scope of impact (which endpoints or services)  
- Mitigation measures  
- Planned resolution or review date  

Recommended format:

```text
Standard section: 
Exception description:
Reason:
Affected services/endpoints:
Mitigation:
Review date:
```

### Decision ownership

Exception approval must have clear ownership.

Guidelines:

- Technical exceptions should be approved by Tech Leads or Architecture owners
- Organization-wide exceptions should be approved by Engineering Leadership
- Decisions should be recorded and traceable

The goal is to balance consistency with practical engineering needs.