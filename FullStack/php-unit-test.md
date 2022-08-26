# PHP Unit

- In general, your test file should `extend TestCase`
- There are pleny of asserts statements such as `assertEquals`, `assertInstanceOf`, etc.
- To test exceptions, start off with `expectException` before calling the method that will throw
- Bootstrap.php is a file that executes code that will run before anything else
- Configuration `phpunit.xml` is another setup file for handling configuration
