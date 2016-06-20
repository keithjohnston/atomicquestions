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

### How can you create my own console command from script?

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

### How do you add a button?

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

### How can I skin a button with custom graphics?

Create a skin file that refers to the custom graphics. Put the png file into the same directory.

UI/skin.ui

```
elements
	SpecialButton
		bitmap button_normal.png
		min-width 131
		min-height 40
		overrides
			element SpecialButton.pressed
				state pressed
			element SpecialButton.hovered
				state hovered
	SpecialButton.pressed
		bitmap button_click.png
		min-width 131
		min-height 40
	SpecialButton.hovered
		bitmap button_hover.png
		min-width 131
		min-height 40
```

Load the skin and set the skinBg for the UIButton.

```
require("AtomicGame");

Atomic.game.init(start);

function start() {

    Atomic.ui.loadSkin("UI/skin.ui");

    var view = new Atomic.UIView();
    var layout = new Atomic.UILayout();
    layout.rect = view.rect;
    view.addChild(layout);

    var buttonLayout = new Atomic.UILayout();
    buttonLayout.axis = Atomic.UI_AXIS_X;
    layout.addChild(buttonLayout);

    var testButton = new Atomic.UIButton();
    testButton.skinBg = "SpecialButton";
    
    buttonLayout.addChild(testButton);
    testButton.onClick = function () {
        print('Button clicked!');
    };
}
```

### How do you display a sprite in 2D?

Make sure that a file 'star.png' is in the directory 'Sprites'.

```
require("AtomicGame");

Atomic.game.init(start);

function start() {
    var game = Atomic.game;
    game.createScene2D();
    var node = game.scene.createChild("star");
    var starSprite = game.cache.getResource("Sprite2D", "Sprites/star.png");
    var sprite2D = node.createComponent("StaticSprite2D");
    sprite2D.sprite = starSprite;
}
```


