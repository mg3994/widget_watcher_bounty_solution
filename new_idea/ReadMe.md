####  Problem I faced

* As TextFormField is also a tapable , and we can also use that as Input , and the Scrollable Part is also there if we enter long text , So I think , My approch of Dealing is wrong , (I think we  Should get=> Is Tapable is Scrolable or Input From your TestSweets UI)
* As On Scroll Position Offset will changeon Scroll ( change in *Y* if scroll is `VERTICAL` and *X* if `Horizontal`
* Problem With Scrollbar (If there)

### Steps

1. Add this Code in Your code

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

// Tuple4 class to hold Four  values , (Don't go on name Tuple as it is used for 3 , as i modified it for 4)
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

2. In init state of class WidgetWatcher add

```dart
   class WidgetWatcher extends StatefulWidget {
   .........

 @override
  void initState() {
    super.initState();
     WidgetsBinding.instance.addPersistentFrameCallback((timeStamp) {
      List txtfrm = findWidgets<TextFormField>(WidgetType.input); //make sure replace TheTuple Logic with Your WidgetDescription method in production , but for now leave it to tuples4
      //..... If possible change it to your  WidgetDescription ..... but leave it for now ....
      print(txtfrm.toString());
    });
```


# Output
```bash
I/flutter ( 9989): [Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, -654.2),WidgetType: WidgetType.input, Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, -579.2),WidgetType: WidgetType.input, Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, 623.8),WidgetType: WidgetType.input]
I/flutter ( 9989): [Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, -654.4),WidgetType: WidgetType.input, Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, -579.4),WidgetType: WidgetType.input, Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, 623.6),WidgetType: WidgetType.input]
I/flutter ( 9989): [Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, -657.4),WidgetType: WidgetType.input, Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, -582.4),WidgetType: WidgetType.input, Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, 620.6),WidgetType: WidgetType.input]
I/flutter ( 9989): [Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, -693.8),WidgetType: WidgetType.input, Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, -618.8),WidgetType: WidgetType.input, Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, 584.2),WidgetType: WidgetType.input]
I/flutter ( 9989): [Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, -728.7),WidgetType: WidgetType.input, Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, -653.7),WidgetType: WidgetType.input, Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, 549.3),WidgetType: WidgetType.input]
I/flutter ( 9989): [Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, -757.4),WidgetType: WidgetType.input, Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, -682.4),WidgetType: WidgetType.input, Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, 520.6),WidgetType: WidgetType.input]
I/flutter ( 9989): [Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, -783.0),WidgetType: WidgetType.input, Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, -708.0),WidgetType: WidgetType.input, Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, 495.0),WidgetType: WidgetType.input]
I/flutter ( 9989): [Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, -805.5),WidgetType: WidgetType.input, Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, -730.5),WidgetType: WidgetType.input, Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, 472.5),WidgetType: WidgetType.input]
I/flutter ( 9989): [Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, -825.1),WidgetType: WidgetType.input, Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, -750.1),WidgetType: WidgetType.input, Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, 452.9),WidgetType: WidgetType.input]
I/flutter ( 9989): [Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, -841.8),WidgetType: WidgetType.input, Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, -766.8),WidgetType: WidgetType.input, Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, 436.2),WidgetType: WidgetType.input]
I/flutter ( 9989): [Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, -855.9),WidgetType: WidgetType.input, Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, -780.9),WidgetType: WidgetType.input, Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, 422.1),WidgetType: WidgetType.input]
I/flutter ( 9989): [Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, -865.5),WidgetType: WidgetType.input, Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, -790.5),WidgetType: WidgetType.input, Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, 412.5),WidgetType: WidgetType.input]
I/flutter ( 9989): [Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, -893.6),WidgetType: WidgetType.input, Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, -817.2),WidgetType: WidgetType.input, Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, 409.0),WidgetType: WidgetType.input]
I/flutter ( 9989): [Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, -889.1),WidgetType: WidgetType.input, Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, -812.9),WidgetType: WidgetType.input, Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, 409.6),WidgetType: WidgetType.input]
I/flutter ( 9989): [Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, -885.0),WidgetType: WidgetType.input, Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, -809.0),WidgetType: WidgetType.input, Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, 410.1),WidgetType: WidgetType.input]
I/flutter ( 9989): [Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, -881.3),WidgetType: WidgetType.input, Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, -805.5),WidgetType: WidgetType.input, Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, 410.6),WidgetType: WidgetType.input]
I/flutter ( 9989): [Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, -878.0),WidgetType: WidgetType.input, Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, -802.3),WidgetType: WidgetType.input, Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, 411.0),WidgetType: WidgetType.input]
I/flutter ( 9989): [Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, -875.0),WidgetType: WidgetType.input, Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, -799.5),WidgetType: WidgetType.input, Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, 411.3),WidgetType: WidgetType.input]
I/flutter ( 9989): [Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, -872.5),WidgetType: WidgetType.input, Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, -797.1),WidgetType: WidgetType.input, Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, 411.6),WidgetType: WidgetType.input]
I/flutter ( 9989): [Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, -870.3),WidgetType: WidgetType.input, Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, -795.1),WidgetType: WidgetType.input, Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, 411.9),WidgetType: WidgetType.input]
I/flutter ( 9989): [Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, -868.6),WidgetType: WidgetType.input, Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, -793.4),WidgetType: WidgetType.input, Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, 412.1),WidgetType: WidgetType.input]
I/flutter ( 9989): [Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, -867.2),WidgetType: WidgetType.input, Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, -792.1),WidgetType: WidgetType.input, Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, 412.3),WidgetType: WidgetType.input]
I/flutter ( 9989): [Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, -866.3),WidgetType: WidgetType.input, Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, -791.2),WidgetType: WidgetType.input, Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, 412.4),WidgetType: WidgetType.input]
I/flutter ( 9989): [Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, -865.7),WidgetType: WidgetType.input, Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, -790.7),WidgetType: WidgetType.input, Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, 412.5),WidgetType: WidgetType.input]
2
I/flutter ( 9989): [Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, -865.5),WidgetType: WidgetType.input, Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, -790.5),WidgetType: WidgetType.input, Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, 412.5),WidgetType: WidgetType.input]
I/flutter ( 9989): [Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, -866.5),WidgetType: WidgetType.input, Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, -791.5),WidgetType: WidgetType.input, Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, 412.4),WidgetType: WidgetType.input]
I/flutter ( 9989): [Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, -870.7),WidgetType: WidgetType.input, Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, -795.4),WidgetType: WidgetType.input, Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, 411.9),WidgetType: WidgetType.input]
I/flutter ( 9989): [Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, -880.5),WidgetType: WidgetType.input, Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, -804.7),WidgetType: WidgetType.input, Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, 410.7),WidgetType: WidgetType.input]
I/flutter ( 9989): [Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, -888.5),WidgetType: WidgetType.input, Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, -812.3),WidgetType: WidgetType.input, Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, 409.7),WidgetType: WidgetType.input]
I/flutter ( 9989): [Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, -884.8),WidgetType: WidgetType.input, Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, -808.8),WidgetType: WidgetType.input, Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, 410.1),WidgetType: WidgetType.input]
I/flutter ( 9989): [Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, -881.5),WidgetType: WidgetType.input, Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, -805.7),WidgetType: WidgetType.input, Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, 410.5),WidgetType: WidgetType.input]
I/flutter ( 9989): [Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, -878.4),WidgetType: WidgetType.input, Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, -802.7),WidgetType: WidgetType.input, Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, 410.9),WidgetType: WidgetType.input]
I/flutter ( 9989): [Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, -875.7),WidgetType: WidgetType.input, Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, -800.2),WidgetType: WidgetType.input, Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, 411.2),WidgetType: WidgetType.input]
I/flutter ( 9989): [Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, -873.3),WidgetType: WidgetType.input, Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, -797.9),WidgetType: WidgetType.input, Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, 411.5),WidgetType: WidgetType.input]
I/flutter ( 9989): [Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, -871.2),WidgetType: WidgetType.input, Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, -795.9),WidgetType: WidgetType.input, Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, 411.8),WidgetType: WidgetType.input]
I/flutter ( 9989): [Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, -869.4),WidgetType: WidgetType.input, Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, -794.2),WidgetType: WidgetType.input, Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, 412.0),WidgetType: WidgetType.input]
I/flutter ( 9989): [Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, -868.0),WidgetType: WidgetType.input, Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, -792.9),WidgetType: WidgetType.input, Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, 412.2),WidgetType: WidgetType.input]
I/flutter ( 9989): [Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, -866.9),WidgetType: WidgetType.input, Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, -791.8),WidgetType: WidgetType.input, Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, 412.3),WidgetType: WidgetType.input]
I/flutter ( 9989): [Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, -866.1),WidgetType: WidgetType.input, Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, -791.1),WidgetType: WidgetType.input, Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, 412.4),WidgetType: WidgetType.input]
I/flutter ( 9989): [Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, -865.6),WidgetType: WidgetType.input, Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, -790.6),WidgetType: WidgetType.input, Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, 412.5),WidgetType: WidgetType.input]
2
I/flutter ( 9989): [Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, -865.5),WidgetType: WidgetType.input, Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, -790.5),WidgetType: WidgetType.input, Tuple4<Widget>: Widget: TextFormField, Size: Size(258.0, 24.0), Position: Offset(51.0, 412.5),WidgetType: WidgetType.input]








````


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
