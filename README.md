# Butt-in - A Button Handling Library for Arduino
Butt-in is a button handling library for Arduino, written in a callback driven manner and serviced by interrupts. As most microcontrollers only have a handful of interrupt handlers this should only be used in cases of a few buttons.

## How to use it

#### Step 1 - Set up your config
```c++
// Number of buttons you have
#define BUTTON_COUNT 6

// Pins the buttons are attached to
#define BUTTON_PINS {2, 3, 5, 6, 7, 8}

// Mode you want the buttons to operate in
#define BUTTON_MODES {STANDARD, DISCONNECTED, DISCONNECTED, DISCONNECTED, DISCONNECTED, DISCONNECTED}

ButtonConfig buttonConfig = (ButtonConfig){BUTTON_PINS, BUTTON_MODES};

// Instantiate your handler
ButtonHandler handler(buttonConfig);
```

#### Step 2 - Set up your listener
```c++
// This function is called when a button is pressed or released.
// The event holds information about what action was taken
void onEvent(ButtonEvent event) {
  Serial.println("Button number pressed: " + String(event.number));
}
```

#### Step 3 - Register the listener in your `setup` function, and pipe through a loop iteration
```c++
void setup() {
  Serial.begin(SERIAL_BAUD);
  handler.setListener(onEvent);
}

void loop() {
  // This tells the library you're ready to handle an event
  handler.onLoop();
}
```

And now you're good to go! 

## How to install it
Copy-past the library folder to your Arduino installations library folder.
