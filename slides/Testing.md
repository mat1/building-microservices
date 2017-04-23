# Testing

### Microservice Structure

https://martinfowler.com/articles/microservice-testing/#anatomy-connections

Explain structure and responsibilities.

### Unit Testing

- Sociable: Treat the class as a black box.
- Solitary: Interactions between objects, use of mocking frameworks.

### Integration Testing

- Make sure the integration between Services works as expected.
- State management can be difficult for external components. Fixed set of data.
- Separate Integration Tests in the Build

### Component Testing

- Testing using Spring Container or Java EE Container
- Communication over network or InMemory (Spring Mock MVC)

### Contract Testing (Consumer Driven Contract Testing)

- Ideally, the contract tests written by each consuming team are runnable in the build for the producing services.

### End-To-End Testing

1. Write as few end-to-end tests as possible
2. Focus on personas and user journeys
3. Choose your ends wisely (UI, REST)
4. Rely on infrastructure-as-code for repeatability
5. Make tests data-independent

### Exploratory

Example SBB Billettautomat

### Test Pyramid

### Summary

- We will write component tests in the next exercise