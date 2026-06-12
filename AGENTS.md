# Agents.md file

## Project Overview

This web application hosts a social group that meets on a monthly or quarterly basis at various locations for a few hours. The basic application allows users to view upcoming meetings and their location. Through controlled access, group members can add users, access and manage group events, including scheduling and modifying events, and manage event locations.

AI may be used to add functionality to or resolve problems with the existing application based on Python, Quart, and JavaScript. The entire application is hosted as a single Quart application, where Quart Blueprints and WebSocket functionality is used in the presentation layer for backend and frontend communications. The UI uses HTML, JavaScript, Jinja Templates and Tailwind CSS. DO NOT make any changes that would affect the architecture or modify the UI layout.

## Features

- Display a list of PyKC events and their locations for Members' information about meetings and their location.
- Display the same list of events for which an Event Manager can add, delete, and modify events. Allow for deletion of multiple events.
- Display a list of locations for which an Event Manager can add, delete, and modify locations.
- From the Events page, allow an Event Manager to add or change an event location.
- Control user access using the following access groups:
  - Developer
  - Event Manager
  - Member
  - Moderator
  - Organizer

## Technology Stack

- Python 3.12+
- Quart and supporting ASGI technologies
- SQLite, aiosqlite, and SQLAlchemy Core through grammdb for data storage
- Jinja Templates
- Tailwind CSS
- HTML
- JavaScript. Note: If JavaScript is necessary for interactivity or other functions, use only vanilla JavaScript. DO NOT use frontend frameworks such as REACT, next.js, et cetera.
- Hatch build environment

## Dependencies

- aiohttp
- aiosqlite
- argon2-cffi
- grammdb (reference <https://grammacc.github.io/grammdb>)
- grammlog (reference <https://grammacc.github.io/grammlog>)
- hypercorn
- pyjwt
- quart
- sqlalchemy[asyncio]

## Coding Practices

### Key Principles

- Write clear, technical responses using precise examples for the technology used.
- Use descriptive variable and function names, adhering to Python naming conventions (for example, lowercase with underscores for functions and variables).

### Quart/Python

- Application routes are registered and managed using helper functions found in src/pykc/pl/routes.py. Do not use Quart's built-in route decorators.
- This project uses only the core components of SQLAlchemy for the flexibility of using multiple database vendors. The project uses the grammdb library for queries, connections, and transactions. Do not modify the grammdb library or the project's SQL.
- Form validation uses a custom implementation including the src/pykc/pl/validation package and src/pykc/pl/dtos.py module.
- The application uses Quart with Jinja templates and native WebSockets functionality for Backend API and UI communications.

### Error Handling and Validation

- Implement error handling as close to the source of the error as possible, including handling errors in the business logic.
- In general, the application should return errors as values if the error is recoverable and only raise an exception if it's a crash condition for the application. Helper functions for wrapping exceptions and returning errors or re-raising categorized exceptions are located in the src/sl/errors.py module.

### Security Guidelines

- The application handles CSRF attacks using JWTs for CSRF tokens to prevent XSS and the application uses an input validation layer. Refer to the following OWASP guideline for more background applicable to this application:  https://cheatsheetseries.owasp.org/cheatsheets/Cross-Site_Request_Forgery_Prevention_Cheat_Sheet.html.
- Do not change any of the authentication functionality unless requested. 

### Key Conventions

1. Prioritize security and performance in every stage of development.
2. The project structure is a decoupled architecture that includes the following layers:
   a. The User Interface contains forms that capture user input, handle basic visual formatting, and validate user experience, such as highlighting an empty required field. The forms should be declarative in their design, with their structure and validation rules written as descriptive rules within the HTML. Avoid JavaScript that processes the inputs prior to submission.
   b. The Presentation Layer performs validation, data sanitation, and error mapping.
   c. The Service Layer executes business logic. The layer, functioning as the backend, should process all incoming requests the same way, regardless of their origin. This layer communicates programmatically with the Presentation Layer using src/pykc/pl/dtos.py and with the Data Layer using src/pykc/sl/structs.py.
   d. The Data Layer contains the database objects including schema and table names, aliases, and complex queries, and two database connections.

### Markdown Standards

- Always run markdownlint on any markdown files created or edited.
- Fix all linting issues before completing the task.

### Testing Preferences

- Use pytest for all testing. Write all Python tests as `pytest` style functions, not unittest classes. Use Quart's test client test_client() method which simulates asynchronous http client requests to the application. Use the pytest-asyncio extension to handle the event loop.
- Use descriptive function names starting with `test_`.
- Prefer fixtures over setup/teardown methods.
- Use assert statements directly, not self.assertEqual.

### Testing Approach

- Never create throwaway test scripts or ad hoc verification files.
- If you need to test functionality, write a proper test in the test suite.
- All tests go in the `test` directory following the project structure.
- Tests should be runnable with the rest of the suite using the appropriate environment scripts.
- Even for quick verification, write each test as a real test that provides ongoing value.
- Use TDD approach; write failing tests first, then code to pass the tests.

### Package management

- This project uses hatch for all project and build management.
