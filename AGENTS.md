# Agents.md file

## Project Overview

Develop or add features to an existing web application using Python, Quart, JavaScript, and other technologies listed below. The application hosts a social group that meets on a monthly or quarterly basis at various locations for a few hours. The basic application allows users to view upcoming meetings and their location. Additional functionality may be added as requirements and resources are available.

 The application enables a group of people to add users with controlled access, access and manage group events, including scheduling and modifying events, and add and relate event locations to the events. The application uses Python and Quart for the backend. The UI uses HTML, JavaScript, Jinja Templates and Tailwind CSS. The Quart backend communicates with the UI using web sockets.

### Home Page Layout

The home or index page has the following menu layout across the top of the page:

- Home
- About PyKC
- Events
- Venues
- Members

## Features

- Display a list of events and their locations for normal users.
  - Allow users to optionally add and update their attendance for an event.
- Display the same list of events for which an Event Manager can add, delete, and modify events. Allow for deletion of multiple events.
- Display a list of locations for users.
- Display the same list of locations for which an Event Manager can add, delete, and modify locations.
- From the Events page, allow an Event Manager to relate a location to an event or change an event location.
- Control user access using the following access groups:
  - Developer
  - Event Manager
  - Moderator
  - Organizer

## Technology Stack

- Python 3.12+
- Quart and supporting ASGI technologies
- SQLite and aiosqlite for data storage
- Jinja Templates
- Tailwind CSS
- HTML
- JavaScript. Note: If JavaScript is necessary for interactivity or other functions, use only vanilla JavaScript. DO NOT use frontend frameworks such as REACT, next.js, et cetera.
- Hatch build environment

## Dependencies

- aiohttp
- aiosqlite
- argon2-cffi
- grammdb
- grammlog
- hypercorn
- pyjwt
- quart
- sqlalchemy[asyncio]

## Coding Practices

### Key Principles

- Write clear, technical responses with precise Quart examples.
- Use Quart's built-in features and tools wherever possible to leverage its full capabilities.
- Prioritize readability and maintainability.
- Use descriptive variable and function names; adhere to naming conventions (for example, lowercase with underscores for functions and variables).
- Structure the project in a modular way using Quart apps to promote reusability and separation of concerns.

### Quart/Python

- Use Quart's route decorators for routing; leverage blueprints for organizing related endpoints.
- Leverage the asynchronous version of SQLAlchemy's ORM for database interactions; avoid raw SQL queries unless necessary for performance.
- Implement custom authentication using JWT via Quart-Session or similar; avoid Django's built-in user model.
- Use Quart's request validation with libraries such as marshmallow for form handling and validation.
- Follow the MVC pattern (Model-View-Controller) for clear separation of concerns.
- Use Quart with Jinja templates and native web sockets functionality for controller and UI communications.

### Error Handling and Validation

- Implement error handling at the view level using Quart's error handlers.
- Use Quart's request validation with libraries such as marshmallow to validate form and model data.
- Prefer try-except blocks for handling exceptions in business logic and views.
- Customize error pages (for example, 404, 500) to improve user experience and provide helpful information.
- Use Quart signals to decouple error handling and logging from core business logic for HTTP request lifecycle events as applicable.

### Security Guidelines

- Apply Quart security best practices for CSRF protection, SQL injection prevention, and XSS prevention.
- Use Quart's built-in tools for testing to ensure code quality and reliability.
- Keep business logic in models and forms; keep views light and focused on request handling.

### Performance Optimization

- Optimize static file handling with Quart's static file management.

### Key Conventions

1. Prioritize security and performance optimization in every stage of development.
2. Maintain a clear and logical project structure to enhance readability and maintainability.

### Markdown Standards

- Always run markdownlint on any markdown files created or edited.
- Install using: `npx markdownlint-cli`
- Fix all linting issues before completing the task

### Testing Preferences

- Write all Python tests as `pytest` style functions, not unittest classes.
- Use descriptive function names starting with `test_`.
- Prefer fixtures over setup/teardown methods
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
