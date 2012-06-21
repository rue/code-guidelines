# Test-Driven Development

* [Philosophy](#philosophy)
* [Available TDD documentations](#doc)
* [Theory](#theory)
  * [Test-First](#test-first)
  * [Top-down design](#top-down)
  * [Arrange Act Assert](#aaa)
  * [BDD](#bdd)
  * [Writing testable code](#testable-code)
  * [Unit vs integration](#unit-vs-integration)
* [Practice](#practice)
  * [Working your way through an untested code base](#untested)
  * [Define a testing strategy](#test-strategy)
* [Conclusion](#conclusion)

## <a id="philosophy"></a>Philosophy
 Test-driven development (TDD) is a software development process that relies on the repetition of a very short development cycle: first the developer writes a failing automated test case that defines a desired improvement or new function, then produces code to pass that test and finally refactors the new code to acceptable standards. Kent Beck, who is credited with having developed or 'rediscovered' the technique, stated in 2003 that TDD encourages simple designs and inspires confidence.
##<a id="doc"></a>Available TDD documentations
##<a id="theory"></a>Theory
### <a id="test-first"></a>Test-First
 You first start by writing a test that best describe the use case of your business.
 This step is really important because it forces you to change your default mindset ).
 You to focus on real business use cases and object interfaces and api instead of mere implementations.
 
 - Your write a failing test (really important, it helps you to avoir false positives)
 - You write as least code as possible to make the test pass
 - You refactor your code.
 - Repeat until the end of time.
 
### <a id="top-down"></a>Top-down design
 When you build a new feature, starting by the database then implementing your way up the UI usually introduce a lot of cruft. 
 By the time you feature is done, you realize that some of the lower layers doesn't fit with the UI or worse you have implemented the world in those layers for future needs.
 
 The proposed method instead, is to start to write an test as close as possible to the UI (controllers?), mock the datasources if needed and then test your way to the bottom until the feature is complete.
### <a id="aaa"></a>Arrange Act Assert
 This pattern is juste a simple way to organize a single test.
 The comments are not necessary, but the way the test is split is really important.
```c#
[Test]
public void When_the_irritable_mailman_does_not_get_an_answer_he_get_angry()
{
 //Arrange
 var mailman = new IrritableMailman();
 var house = new EmptyHouse();

 //Act
 mailman.KnocksTheDoorOf(house);
 
 //Assert
 Assert.That(mailman.Mood, Is.EqualTo(Mood.Angry)
}
```
It is very easy to understand what is tested, how to set it up and what is the behavior.
### <a id="bdd"></a>BDD
 Behavior-driven development is nothing else than TDD v2. 
 There were many complaints when TDD started that a lot of people were doing it wrong.
 They were testing for the sake of doing tests instead of trying to test the behaviors.
 It is really important to understand that what we want to test is the application behavior and not just validation or if the value of a variable is correctly set.
 Your tests should become executable specs of your business.
###<a id="testable-code"></a> Writing testable code
 Because of the design choice of C#, it is easy to write code that is untestable by default.
 A good advice would be to follow SOLID principles.
 Secondly, because of the static nature of c# you need to interface the wazoo out of your app so that you can replace the implementations easily.
 
 If you have problem testing your app because your setup is really big or anything else.
 It is usually a sign that you have a poor oo design and that you need a refactor.
 
### <a id="unit-vs-integration"></a>Unit vs Integration tests

Unit tests are very useful for the domain because you can test your behaviors seperately are those test are very fast.
On the other hand, integration tests usually integrate multiple systems together to ensure that your app is really working as a whole.

Both are useful, the rule of thumb would be that when a unit test is not useful for your particular case do an integration test.


##<a id="practice"></a>Practice
##<a id="conclusion"></a> Conclustion