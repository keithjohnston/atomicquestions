## Atomic Game Engine Questions and Answers

### How do I change the size of the app window?


### How do you make the console appear?

Example:
```
require("AtomicGame");

Atomic.game.init(start);

function start() {
    Atomic.getUI().showConsole(true);
}
```

### How can I create my own console command from script?

You need to subscribe to the "ConsoleCommand" event. The callback will be passed in the entire command line and you can then react to it from script.

Example:
```
require("AtomicGame");

Atomic.game.init(start);

function start() {
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
```

### How do I add a button?

Example:
```
require("AtomicGame");

Atomic.game.init(start);

function start() {
    var view = new Atomic.UIView();
    var layout = new Atomic.UILayout();
    layout.rect = view.rect;
    view.addChild(layout);

    var buttonLayout = new Atomic.UILayout();
    buttonLayout.axis = Atomic.UI_AXIS_X;
    layout.addChild(buttonLayout);
    
    var testButton = new Atomic.UIButton();
    testButton.text = 'Click me!';
    buttonLayout.addChild(testButton);
    testButton.onClick = function () {
        print('Button clicked!');
    };
}
```
