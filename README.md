# API Testing Framework

A comprehensive Java-based API testing framework using REST Assured, Selenium, and Cucumber with BDD approach.

## Features

- **REST Assured** for API testing
- **Cucumber** for BDD test scenarios
- **TestNG** for test execution
- **Selenium WebDriver** for browser automation (if needed)
- **Maven** for dependency management
- **Extent Reports** for detailed reporting
- **Jackson** for JSON processing

## Project Structure

```
src/
├── test/
│   ├── java/
│   │   └── com/automation/
│   │       ├── hooks/          # Test hooks (Before/After)
│   │       ├── models/         # Data models and POJOs
│   │       ├── runners/        # Test runners
│   │       ├── steps/          # Step definitions
│   │       └── utils/          # Utility classes
│   └── resources/
│       ├── features/           # Cucumber feature files
│       ├── config.properties   # Configuration properties
│       └── testng.xml         # TestNG configuration
```

## Test Scenarios

### GET Request Test
- **Endpoint**: `https://echo.free.beeceptor.com/sample-request?author=beeceptor`
- **Validations**:
  - Response status code (200)
  - Response contains `path` field
  - Response contains `ip` field
  - Response contains all headers
  - Response time validation

### POST Request Test
- **Endpoint**: `https://echo.free.beeceptor.com/sample-request?author=beeceptor`
- **Payload**: Complete order information with customer, items, payment, and shipping details
- **Validations**:
  - Customer information accuracy
  - Payment details verification
  - Product information validation
  - Order total calculation

## Setup and Installation

1. **Prerequisites**:
   - Java 11 or higher
   - Maven 3.6 or higher

2. **Clone and Setup**:
   ```bash
   git clone <repository-url>
   cd api-testing-framework
   mvn clean install
   ```

3. **Run Tests**:
   ```bash
   # Run all tests
   mvn test

   # Run specific tags
   mvn test -Dcucumber.filter.tags="@get-request"
   mvn test -Dcucumber.filter.tags="@post-request"
   ```

## Configuration

Update `src/test/resources/config.properties` for environment-specific settings:

```properties
api.base.url=https://echo.free.beeceptor.com
api.timeout=30000
test.environment=qa
```

## Reports

After test execution, reports are generated in:
- **Cucumber HTML Report**: `target/cucumber-reports/index.html`
- **JSON Report**: `target/cucumber-reports/Cucumber.json`
- **JUnit XML**: `target/cucumber-reports/Cucumber.xml`

## BDD Feature File

The test scenarios are written in Gherkin syntax in `src/test/resources/features/api_tests.feature`:

```gherkin
Feature: API Testing with Beeceptor
  As a QA Engineer
  I want to test GET and POST API endpoints
  So that I can validate the API responses and data integrity

  @get-request
  Scenario: Validate GET request response
    Given the API base URL is "https://echo.free.beeceptor.com"
    And I have a GET endpoint "/sample-request"
    When I send a GET request
    Then the response status code should be 200
    And the response should contain field "path"
```

## Key Components

### ApiHelper
Utility class for REST Assured operations:
- GET, POST, PUT, DELETE request methods
- Query parameter management
- Request body handling
- Response logging

### TestContext
Singleton pattern for sharing test data across steps:
- Response storage
- Test data management
- Context reset functionality

### OrderPayload
POJO model for order data:
- Customer information
- Product items
- Payment details
- Shipping information

## Best Practices

1. **Page Object Model**: Organized structure for maintainability
2. **Data-Driven Testing**: External test data management
3. **Logging**: Comprehensive logging with SLF4J
4. **Error Handling**: Robust exception handling
5. **Reporting**: Detailed test reports with Cucumber

## Extending the Framework

To add new test scenarios:

1. Add new scenarios in feature files
2. Implement corresponding step definitions
3. Create new model classes if needed
4. Update test runners with appropriate tags

## Dependencies

Key dependencies included:
- REST Assured 5.3.2
- Cucumber 7.14.0
- Selenium 4.15.0
- TestNG 7.8.0
- Jackson 2.15.2
- WebDriverManager 5.5.3