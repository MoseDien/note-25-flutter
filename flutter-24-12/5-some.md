#  一些特殊的东西
## dart访问控制
- 没有关键字public/open等，使用的是习惯
- 添加下划线表示私有，无法被导出export
- 通过export/import 导出导入
- 一般采用的办法是 - 统一导出，单独的文件写出`export x.dart`
- 通过get/set，来增加一些逻辑

### mixin
- 复用代码
- 如果你的目标是定义行为规范，选择 接口/协议；
- 如果你的目标是共享逻辑或复用代码，选择 mixin。

```dart
class Animal {
  void eat() => print('Eating');
}

mixin CanFly {
  void fly() => print('Flying');
}

class Bird extends Animal with CanFly {}

void main() {
  var bird = Bird();
  bird.eat(); // 输出: Eating
  bird.fly(); // 输出: Flying
}
```
## 继承-实现
- dart 没有protocol，只有class
- implements - 实现接口，可以多个实现
- extends - 继承 - 只能有单继承
- with - 用于mixin

## part + part of
- 主文件中通过 part 明确引入，而分文件中需要通过 part of 声明所属主文件。
- 分文件共享主文件的上下文，不需要额外导入

## 自动生成的代码
```dart
mixin _$PlaybackEvent {
  // 自动生成的代码
}

class PlaybackEvent {
  // 手写的代码
}
```