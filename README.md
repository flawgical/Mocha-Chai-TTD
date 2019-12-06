<img src="https://www.paradigmadigital.com/wp-content/uploads/2017/02/1.png" />

# Introduction to Test Driven Development 
---

| Learning Objectives & Main Takeaways |
|---|
| Understand what Test Driven Development paradigm means |
| Build an environment for Browser Testing |
| Identify common Syntax Patterns |
| How to Run Tests on the browser |
| Write basic tests using the Mocha Suite |
| Navigate through the docs & other testing suites |

## Testing is NOT required as part of your Unit 1 Project but it could be a sweet bonus.

**Do not worry about mastering testing, every company uses a different suite. The purpose of this lesson is to provide you exposure so you are familiar with TDD and are able to talk about it.**

#### IF along the way you get behind, don't worry, this README is like a walk-through tutorial so you can always come back to it. Pay attention! 

## Roadmap
1. TDD & BDD
2. Why we need Tests? 
3. How does TDD save development time? 
4. Let's write our first test!
5. Exercise: You write some tests on your own
6. Essential Questions
7. Lab 

### 1. TDD & BDD

#### Testing... testing... 123 

<img src="https://perspectives.mobilelive.ca/hs-fs/hubfs/TDD%20BDD%20DDD/1-4.jpg?width=1280&name=1-4.jpg">

##### How Testing Works
- 1.  Before you write implementation code, write some code that proves that the implementation works or fails. Watch the test fail before moving on to the next step (this is how we know that the passing test is not a false positive - this is how we test our tests)
- 2.  Write the implementation code and watch the test pass
- 3.  Refactor if needed. You should feel confident refactoring your code now that you have a test to tell you if you’ve broken something.

##### What is BDD (Behavior Driven Development)
<img src="https://blog.testlodge.com/wp-content/uploads/2018/04/tdd_v_bdd_cycle-1024x538.png">

- Behavioral Driven Development (BDD) is a software development approach that has evolved from TDD (Test Driven Development). It differs by being written in a shared language, which improves communication between tech and non-tech teams and stakeholders. In both development approaches, tests are written ahead of the code, but in BDD, tests are more user-focused and based on the system’s behavior.
- BDD is a technique to write tests where we define our spec and then we implement. 
- The spec can be used in three ways: 
	- As **Tests** - they guarantee that the test works
	- As **Docs** - the titles of _describe_ and _it_ tell what the function does. 
	- As **Examples** - the tests are actually working examples showing a function can be used.
	
With the spec, we can safely improve, change, even rewrite the function from scratch and make sure it still works right.

That’s especially important in large projects when a function is used in many places. When we change such a function, there’s just no way to manually check if every place that uses it still works right.


### 2. Why TDD? 
<img src="https://miro.medium.com/max/2048/1*9ZbCv6O3Sr7x6d3lt3uNRA.png">


   " Murphy’s Law of Debugging: The thing you believe so deeply can’t possibly be wrong so you never bother testing it is definitely where you’ll find the bug after you pound your head on your desk and change it only because you’ve tried everything else you can possibly think of."

### 3. How does TDD save development time? 

TDD has a learning curve, and while you’re climbing that learning curve, it can and frequently does add 15% — 35% to implementation times. But somewhere around the 2-years in mark, something magical started to happen: I started coding faster with unit tests than I ever did without them.

`The point is not how long it takes to type this code. The point is how long it would take to debug it if something goes wrong.`


#### TDD helps you write better code - it helps erradicate the fear of change



### 4. Let's Write our first test together

#### We will be using the [Mocha](https://mochajs.org/) Automated Testing Suite 

#### The spec in action (remember FAIL - REFACTOR - PASS - REPEAT) 


**Step 1:** House Keeping
Let's have our classic Unit1 directory structure with an index.html - js/main.js - css/style.css 

Your boilerplate HTML should look like this: 
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Test Driven Development</title>
</head>
<body>
    
</body>
</html>
```
Next, let's make sure our JS and CSS are properly connected to the HTML

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <link rel="stylesheet" href="css/style.css">
</head>
<body>
    
    <script src="js/app.js"></script>
</body>
</html>
```
Next, let's create a new folder at our root level called test ( so you will have you index.html, js, css, and test).
In the tests folder - let's create a file called test.js 

**Step 2:**
Let's set up our environment to install the Mocha Testing Suite into our directory 
```npm init``` 
	- This initializes our directory to use the Node Package Manager - through which we will install 				Mocha and thousands of other packages that will allow us to make applications.
	
You will hit **enter** until it says ```entry point: (index.js)``` and you will add ```app.js``` as the entry point.
As you continue to hit **enter** you will see a prompt for ```test command:``` - here you will write mocha.
	- Upon initializing your directory with node you should see a couple new files added in your directory. 
		- You will see a Node Modules Folder
		- You will see a package.json file 
		- You will also see a package.json.lock file (do not touch that contents on that file)
		
		
**Step 3:**
Since we have initialized our directory to manage node packages - we will install mocha and chai via the following commands: 
```npm i mocha```
```npm i chai```

If you look into the package.json file you will see the following: 
package.json
```{
  "name": "mocha-testing",
  "version": "1.0.0",
  "description": "An example for mocha and chai testing",
  "main": "app.js",
  "directories": {
    "test": "test"
  },
  "scripts": {
    "test": "mocha"
  },
  "author": "",
  "license": "ISC",
  "dependencies": {
    "chai": "^4.2.0",
    "mocha": "^6.2.2"
  }
}
```
NOTE: If you forgot to add mocha to your test command, replace the contents for scripts with "mocha" in your package.json file. 
```
"scripts" : {
	"tests": "mocha"
	}
	
```


**Step 4:**
Let's make sure our index.html is hooked up properly with our new dependencies. 

Paste this in your HTML 

```
<!DOCTYPE html>
<html>
  <head>
    <title>Mocha Tests</title>
    <link rel="stylesheet" href="node_modules/mocha/mocha.css">
  </head>
  <body>


    <div id="mocha"></div>
    <script src="node_modules/mocha/mocha.js"></script>
    <script src="node_modules/chai/chai.js"></script>
    <script>mocha.setup('bdd')</script>

    <!-- load code you want to test here -->
    <script src="js/app.js"></script>

    <!-- load your test files here -->
    <script src="test/test.js"></script>
    

    <script>
      mocha.run();
    </script>
  </body>
</html>
```

**Note**: Mocha comes with browser support - and thus we are linking its inherent styling in our head AND then we are linking its respective script tags for mocha and chai. 
Additioanlly, we are also linking out test.js. 

**Notice the script tag in which mocha.run() is hanging out in - this tells the html to run the tests on the browser. The tests are started by that command. The HTML element id="mocha" will be used by mocha to output results** 


**Step 5:**

Let's move into our test.js file and write a test. 
But first!!!! We need to require the Chai library in our test file so we can use ```assert*``` method. 
At the top of the file let's go ahead and add the following line: 
```const assert = chai.assert```

So to our test now! 

Let's say we want to write a function called yellSomething that converts an input (phrase) into uppercase. 
So if the input is something like ```"hey how are you doing?" ```.
It should convert that phrase into ```"HEY HOW ARE YOU DOING?"```.

So we before we get started, this is how the skeleton syntax for mocha/chai looks like: 

```
describe('function name', function() {
  it('what we think it should do', function() {
    assert.equal(variable name, what we think the value of the variable should be);
  });

  // We can have more its here
});

```

We are using both Mocha and Chai. 
Let's take a moment and look at [Chai]("https://www.chaijs.com/") and see what ```assert``` means. 
In our case, we are only going to use the ```assert.equal()``` but as you can see, there are many methods that we can use depending on our use case. 

A spec has three main building blocks that you can see above:

```describe("title", function() { ... })```

What functionality we’re describing. In our case we’re describing the function pow. Used to group “workers” – the ```it``` blocks.
```it("use case description", function() { ... })```

In the title of it we in a human-readable way describe the particular use case, and the second argument is a function that tests it.
```assert.equal(value1, value2)```

The code inside ```it``` block, if the implementation is correct, should execute without errors.

SO back to our wonderful function ```yellSomething()```

WE want to create a function that takes a string as an input and returns THAT string in all caps. 
The test for ```yellSomething``` looks something like this: 

test.js
```
describe('yellSomething', function() {
  it('should convert a string to all caps', function() {
    const aggressiveGreeting = yellSomething('hey there, friend');
    assert.equal(aggressiveGreeting, 'HEY THERE, FRIEND');
  });
});
```

We could also include the function call in our assert statement like this: 

test.js
```
describe('yellSomething', function() {
  it('should convert a string to all caps', function() {
    assert.equal(yellSomething('hey there, friend'), 'HEY THERE, FRIEND');
  });
});
```
Before we go ahead and write the function in our app.js, let's check our browser (index.html) and make this test fail.

So let's open up our console (or terminal) and type ```open index.html``` 
Here, we should see this test fail. 

***Now*** let's go into our app.js and write the function so we can pass this test. 

app.js 
```
function yellSomething(phrase) {
  return 'HEY THERE, FRIEND'
}
```

Let's refresh the browser - and BAM! our test should be passing.
It sure is nice when a test passes, but it's pretty basic and not very moduler (look this word up in the context of programming) 

Let's now move into the refactor phase of TDD 

We could re-write our function in app.js to look something like this 

```
function yellSomething(phrase) {
  return phrase.toUpperCase();
}
```
NOW let's run the test again and check the browser! It passes! 
I just love seeing that green. 

So far so good.. BUT we haven't thought about other possible ways our function could go wrong. 
This is why testing is challenging and useful - it demands that you think through how any function could go wrong. It helps you consider the possibilities and the unintended consequences. 

At this point I know that my function returns any string input into all caps. Sure! But what if the input is NOT a string, but maybe a number or something else. Have I thought about how I am going to deal with that? Maybe I can say, hey! your input is not a string! How the hell am I supposed to deal with this edge case? 

So we can be smart about this and refactor our test to make sure we accomodate for when the input is not a string - we can do this by adding another ```it``` block. Let's make sure we have type checking! 

Check it out!! 

test.js
```
describe('yellSomething', function() {
  it('should convert a string to all caps', function() {
    const aggressiveGreeting = yellSomething('hey there, friend');
    assert.equal(aggressiveGreeting, 'HEY THERE, FRIEND');
  });
  it('should display a message if given a non-string input', function() {
    const numberInput = yellSomething(5);
    assert.equal(numberInput, 'Please input a string.');
  });
});
```

Now let's run the test by refreshing the browser. AND DAMN! Our awesome function in app.js did NOT account for this edge case. 
You know what we have to do, you do! 
Let's refactor 

app.js 
```
function yellSomething(phrase) {
  if (typeof phrase !== 'string') {
    return 'Please input a string.';
  }
  return phrase.toUpperCase();
}
```

It's time to run the test again. Let's refresh!!
And HELLO! The tests are passing! 


BUT...BUT.. there's more! 
How can take care of a possibility that there is no input - I need to accomodate for when there is no input. 
So here we go again! Let's refactor our test to make sure we say something when there is no input at all. 

Back to the test.js and let's add another ```it``` block. 
```
it('should display a message if no input is given', function() {
  const emptyInput = yellSomething();
  assert.equal(emptyInput, 'Please input a string.');
});
```

We go run the test again, and see that it fails!!

Back to app.js and refactor our function to something like this: 
```
function yellSomething(phrase) {
  if (!phrase || typeof phrase !== 'string') {
    return 'Please input a string.';
  }
  return phrase.toUpperCase();
}
```

Great! Now this version passess our tests! Hooray! Feeling blessed? 

```
console.log(yellSomething("yes") 
// YES
```

JUST ONE MORE THING THOUGH... 

What if I put multiple inputs, but really, I just want 1 input at a time. How can I test for that? 

Back to test.js to refactor by adding this ```it``` block: 
```
it('should display a message if more than one input is given', function() {
  const threeInputs = yellSomething("Wow", "such", "testing");
  assert.equal(threeInputs, 'Please input a string.');
});
```

Ahh! Thank all that there is good in this world... now we need to see the test fail, and then go back to app.js 
to make my function look something like this: 

```
function yellSomething(phrase) {
  if (arguments.length !== 1 || typeof phrase !== 'string') {
    return 'Please input a string.';
  }
  return phrase.toUpperCase();
}
```
Run the test in the browser again! And we have it folks! It all passess. 

This whole process of RED - REFACTOR - GREEN is the essence of how testing works. 



### Review 
***
Note: ```describe()``` is simply a way to group our tests in Mocha. We can nest our tests in groups as deep as we deem necessary. describe() takes two arguments, the first is the name of the test group, and the second is a callback function.


And ```it()``` is used for individual test case. Something like it should... do this or do that. It also takes two arguments.  
***


### 5. Exercise Time!

Let's take a few minutes and write a new test and a new function. 

So in accordance with the BDD technique, 

1. Write a function sayHello that returns "Hello!" 
2. Write a function addOne that adds 1 to any number. 



REMEMBER follow the steps we took - write the test, fail the test, refactor the code, pass the test. 

7 mins. 


### 6. Essential Questions

1. What are at least 2 advantages of following the TDD paradigm? 
2. What are the 2 common testing functions used in Mocha framework?
3. What is another TDD testing suite? (Hint: Look it up!) 


### 7. Lab

1. Write a test for a function addTwoNumbers that adds any 2 numbers. (Easy)

2. Write a mocha/chai test to ***test*** a function
```pow()``` that takes 2 arguments ```(x, n)``` where ```x``` is the number that has the power of ```n```. 
So ```console.log(pow(2, 3))``` should return ```8``` (Medium)

Remember to test for negative numbers. 
Remember to test for data type checking. 

3. Write a test for the following function. (Mildly difficult because of reverse thinking)
This one requires you to study and understand what this function is doing and then write a test for it.
You can use console.log to see what this function is returning.
```
function longestWord (arr) {
  let wrongType = arr.some(element => typeof element !== 'string');
  if (!arr.length || wrongType) {
    return 'Please input an array of strings!';
  }

  if (arr.length === 1) return arr[0];

  let longest = arr.reduce((wordA, wordB) => {
    return wordA.length > wordB.length ? wordA : wordB;
  });
  return longest;
}
```
***Remember to test for both expected cases (actually getting an array of strings as an input) and edge cases (getting something other than an array of strings as an input).***

We can never assume the input will be exactly what the function expects!
