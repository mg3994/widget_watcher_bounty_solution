```dart
import 'package:flutter/material.dart';

import 'package:flutter_test/flutter_test.dart';

import '../../../enum/widget_type.dart';

// Modified findWidgets function
List<Tuple4<Widget, Size, Offset, WidgetType>> findWidgets<T extends Widget>(
    WidgetType widgetType) {
  return collectAllElementsFrom(WidgetsBinding.instance.rootElement!,
          skipOffstage: false)
      .map((e) => Tuple4<Widget, Size, Offset, WidgetType>(
            e.widget,
            _getSize(e),
            _getPosition(e),
            widgetType,
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

// Tuple3 class to hold Four  values , (Don't go on name Tuple as it is used for 3 , as i modified it for 4)
class Tuple4<A, B, C, D> {
  final A item1;
  final B item2;
  final C item3;
  final D item4;

  Tuple4(this.item1, this.item2, this.item3, this.item4);
  @override
  String toString() {
    return 'Tuple4<${A.toString()}>: '
        'Widget: $item1, '
        'Size: $item2, '
        'Position: $item3,'
        'WidgetType: $item4';
  }
}
```


# How to use 
* in init state just add this
  ```dart
   WidgetsBinding.instance.addPersistentFrameCallback((timeStamp) {
      List txtfrm = findWidgets<TextFormField>(WidgetType.input);
      print(txtfrm.length.toString());
    });
  ```

  # as I think we should not use Set as On scroll the position Changes , So The Above code gives Extra Flexibility
# How to use
```dart
   List txtfrm = findWidgets<TextFormField>(WidgetType.input);
```
