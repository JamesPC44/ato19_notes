# Automated Testing Javascript

@venkat_s

* Verification - Testing that code written yesterday still works; should be automated
* Selenium - Pathway to Hell Automation
* Test pyramid
* 'This code is hard to test' => The design of this code sucks
* Integration testing is like salt in a meal; it adds to the meal but you can't live oon salt

Tools here not recommendations, just examples

`npm install mocha chai istanbul karma karm-chai karma-chrome-launcher karma-cli karma-clear-screen-repeater karma-coverage`

* start with canary test, assert true==true
 * test that system is working so you know if an upgrade has broken your testing
* edit karma.conf.js, add `'chai','sinon'` to frameworks array
 * in files add 'test/**/*.js', src/**/*.js'
 * preprocessors: `'src/**/*.js: 'coverage'`
* in package.json under scripts, test: `karma start --reprorts clear-screen,dots,coverage`
* create test dir
* sample.test.js
````
describe('sample test, function() {
  it('canary shoudl sing', ()=> {
    expect(true).to.be.true;
  });
})
````
* Now setup CI (Jenkins, etc.)
* 4 types of test I like to write:
 * positive test - happy path - working as intended
 * negative test - handling exception (make sure can't put $$ in a closed account, etc)
 * exception test - is it throwing the right exceptions at the right time
````
describe('exception test, funcation() {
  it ('divide by zero', ()=> {
    expect({} => divide(8,0)).to.throw(Error)
  });
});
````
 * performance test - is it performing at speed expected

3 choices for unit testing
1. do it
1. Ask for help
1. be yelled at

Testing with Dependencides
* mocking and stubbing - sinon js package
````
  let sandbox;
  beforeEach(function() {
    sandbox = sinon.createSandbox();
  });
  afterEach(function() {
    sandbox.restore();
  }
