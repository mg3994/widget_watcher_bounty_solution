```dart
List<Type> findWidgetsDerivedFromEditableTextState() {
  // this works perfectly [EditableText, EditableText, EditableText]
  return collectAllElementsFrom(WidgetsBinding.instance.rootElement!,
          skipOffstage: false)
      .map((element) => element.widget)
      .where((widget) => widget is EditableText)
      .map((widget) => widget.runtimeType)
      .toList();
}
```
