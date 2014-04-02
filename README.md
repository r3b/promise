promise
=======

A very minimal Promise implementation. Creates a simple deferred object with utility methods for sequential or parallel execution. that's it.

```
var Promise= require('r3b-promise');

function asyncTask(options, callback){
  //do something
  callback();
}

function postProcessingTask(err, result){
  //process
}

function process(options){
  var p = new Promise();
  asyncTask(options, function(err, result){
    p.done(err, result);
  }
  return p;
}

function run(){
  process({}).then(postProcessingTask);
}

function runInParallel(){
  Promise.chain([
    asyncTask({property:'value1'}),
    asyncTask({property:'value2'}),
    asyncTask({property:'value3'}),
  ]).then(function(errors, results){
    errors.forEach(function(err){
      //handle error
    });
    results.forEach(function(result){
      //handle result
    });
  });
}

function step(err, data){
  var p = new Promise();
  passItOn(function(err, result){
    p.done(err, result);
  }
  return p;
}
function runInSequence(){
  Promise.chain([
    step({property:'value1'}),
    step({property:'value1'}),
    step({property:'value1'}),
  ]);
}
```
