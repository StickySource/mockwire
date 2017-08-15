# MockWire

Testing components like they run in production 

## Background 

Using IOC Containers we end up writing components. Components are classes that have their dependencies injected.

The wrangling required to setup IOC contexts can be honerous and complicated.

MockWire takes a very simple approach, the test class is a manifest of the DI context, as a developer this makes it very clear and obvious whats actually being tested.

## Usage

### Junit

To run a test using Mockwire, use @RunWith(MockwireRunner.class)

### Testng

Two base uses for testing. 

## Container Based for Environment Testing 

Uses a container (@MockwireContainement) containing all the components within scope. It is populated by scanning the classpath for components (@StickyComponent); or with additional scanning specified in the @MockwireContainment annotation e.g. @MockwireContainment("main.component1"))

Components for test are then injected (@Inject) and available for use in the test. To inject a component automatically if it is required by configuration use @MockwireConfiguredFieldInjection.

#### Analogy 

If you wish to test a Party Balloon within the context of a Party (@MockwireContainment), the test environment would also include a Cake (@StickyComponent), Candles (@StickyComponent), Guests (@StickyComponent) and Presents (@StickyComponent) even though the balloon may not interact with these. 

If the Balloon's interaction with a Birthday Candle needs to be tested, a Birthday Candle is added (@Inject Candle birthdayCandle) to the test,

## Scenario Based for Isolated Testing

Add test components to the test scope by use of usage based annotations:

### @UnderTest 

The component or components being tested by the test. 

Annotation with @UnderTest will add the component to context and instantiate it for usage.

### @Controlled

A component or components being utilised by the test but which are not being tested by this test. 

Annotation with @Controlled will add the component to context and instantiate it for usage.

### @Uncontrolled

A component or components being used by the test but for which the test is not responsible e.g. a test may require a datascore but it is not responsible for how the datastore responds. 

Annotation with @Uncontrolled will add the component to context but does not instantiate the component, expecting only mocked responses to be returned. 

#### Analogy

If you wish to test your Bath Tub (@UnderTest) will not leak. 

To test your Bath Tub you use a Tap (@Controlled) to add some Water by controlling when the Tap is on/off. 

The Water (@Uncontrolled) itself is also used by the test but you don't control how hot it is.
