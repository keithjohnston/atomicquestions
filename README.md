## Atomic Game Engine Questions and Answers

### How do I change the size of the app window?


### How do you make the console appear?

Example:

```
require("AtomicGame");

Atomic.game.init(start, update);

function start() {
    Atomic.getUI().showConsole(true);
}

function update(timeStep) {
}
```

### How can I create my own console command from script?

You need to subscribe to the "ConsoleCommand" event. The callback will be passed in the entire command line and you can then react to it from script.

Example:

```
require("AtomicGame");

Atomic.game.init(start, update);

function start() {
  var game = Atomic.game;

  game.createScene2D();

  Atomic.getUI().showConsole(true);
    
  Atomic.getEngine().subscribeToEvent('ConsoleCommand', function(data) {
    var commandLine = data['Command'];
       
    var tokens = commandLine.split(' ');
       
    if (tokens[0] === 'connect') {
      var server = tokens[1];
            
      print('Connecting to ' + server);
    }
  });
}

function update(timeStep) {
}
```
