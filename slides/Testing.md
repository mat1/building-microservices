# Testing

### Microservice Structure

https://martinfowler.com/articles/microservice-testing/#anatomy-connections

Explain structure and responsibilities.

### Unit Testing

https://martinfowler.com/articles/microservice-testing/#testing-unit-introduction

- Sociable: Treat the class as a black box.
- Solitary: Interactions between objects, use of mocking frameworks.

### Integration Testing

https://martinfowler.com/articles/microservice-testing/#testing-integration-introduction

- Make sure the integration between Services works as expected.
- State management can be difficult for external components. Fixed set of data.
- Separate Integration Tests in the Build

### Component Testing

https://martinfowler.com/articles/microservice-testing/#testing-component-in-process-diagram

- Testing using Spring Container or Java EE Container
- Communication over network or InMemory (Spring Mock MVC)

### Contract Testing (Consumer Driven Contract Testing)

https://martinfowler.com/articles/microservice-testing/#testing-contract-diagram

- Ideally, the contract tests written by each consuming team are runnable in the build for the producing services.

### End-To-End Testing

https://martinfowler.com/articles/microservice-testing/#testing-end-to-end-introduction

1. Write as few end-to-end tests as possible
2. Focus on personas and user journeys
3. Choose your ends wisely (UI, REST)
4. Rely on infrastructure-as-code for repeatability
5. Make tests data-independent

### Exploratory

Example SBB Billettautomat

### Test Pyramid

https://martinfowler.com/articles/microservice-testing/#conclusion-test-pyramid

### Summary

https://martinfowler.com/articles/microservice-testing/#conclusion-summary

- We will write component tests in the next exercise
