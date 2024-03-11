```dart
import 'package:flutter/material.dart'; //or use widget
import 'package:flutter_test/flutter_test.dart';

List<T> findWidgets<T extends Widget>() =>
    collectAllElementsFrom(WidgetsBinding.instance.rootElement!,
            skipOffstage: false)
        .map((e) => e.widget)
        .whereType<T>()
        .toList();
```
#### TASK: Listen to widgets here (or anywhere besides the UI files) and pass it to the widget monitor service
    
     ###### NON-NEGOTIABLE IMPLEMENTATION RULES:
     1. Widgets should be added as they appear in the widget tree (tap "get started button to add and remove widgets")
     2. No code to be added in any of the UI files (this code will eventually be used in a package)
     3. The same widget should not be added twice
     4. We want to get the position, size and type of widget
     5. We should detect all tappable widgets, all input/text fields, all scrollable widgets

# Here the Point :-    5). We should detect all tappable widgets, all input/text fields, all scrollable widgets
> it is not possible as Each widget is derived from different widget and Some of Single (Example Given ) widget have All kind of Behaviour like Tap action , input or scroll :- TextInput ,

### Uses 
```dart
     List<TextFormField> txtfrm = findWidgets();
```
#### output be
```bash
[TextFormField, TextFormField]
```

# Key Idea we can get the <T> Widget Type , How much They are 

### Ultimate Code 
```dart
import 'package:flutter/material.dart';
import 'package:flutter/rendering.dart'; // Import rendering library for RenderObject
import 'package:flutter_test/flutter_test.dart';

// Modified findWidgets function
List<Tuple3<Widget, Size, Offset>> findWidgets<T extends Widget>() {
  return collectAllElementsFrom(WidgetsBinding.instance.rootElement!,
          skipOffstage: false)
      .map((e) => Tuple3<Widget, Size, Offset>(
            e.widget,
            _getSize(e),
            _getPosition(e),
          ))
      .where((tuple) => tuple.item1.runtimeType == T)
      .toList();
}

// Helper function to get size of widget
Size _getSize(Element element) {
  final renderObject = element.renderObject;
  if (renderObject is RenderBox) {
    return renderObject.size;
  }
  return Size.zero;
}

// Helper function to get position of widget
Offset _getPosition(Element element) {
  final renderObject = element.renderObject;
  if (renderObject is RenderBox) {
    return renderObject.localToGlobal(Offset.zero);
  }
  return Offset.zero;
}

// Tuple3 class to hold three values
class Tuple3<A, B, C> {
  final A item1;
  final B item2;
  final C item3;

  Tuple3(this.item1, this.item2, this.item3);
  @override
  String toString() {
    return 'WidgetInfo<${A.toString()}>: '
        'Widget: $item1, '
        'Size: $item2, '
        'Position: $item3';
  }
}
```

