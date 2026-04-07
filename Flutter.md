## Dart

## Flutter
**Flutter에서 상태 관리는 어떻게 하는지 말해주세요.**
- Flutter에서 위젯은 state의 변화에 따라 UI를 그리게 됩니다. 이때 state에 따라 위젯을 다시 그리고자 할 때 setState를 통해서 로컬로 상태 관리를 할 수도 있고,
- 여러 위젯에서 State를 공유하는 경우 Provider나 Riverpod, Bloc 등 상태 관리 라이브러리를 통해 state를 관리하게 됩니다.
- 이를 통해 상태를 위젯 트리와 분리하고, 유지보수성을 높일 수 있습니다.

**Riverpod, Bloc, GetX와 같은 상태 관리 도구를 왜 사용할까요?**

- Flutter에서는 상태가 변하면 UI가 다시 그려지는데, 상태가 복잡해지거나 여러 위젯에서 공유되기 시작하면 setState만으로는 관리가 어려워지고 번거로워집니다.
- 그래서 Riverpod, Bloc, GetX 같은 상태 관리 도구를 사용해 상태를 위젯 트리와 분리하고, 유지보수성을 높일 수 있습니다.
