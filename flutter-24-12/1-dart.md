# dart
- final vs const: const是常量，final是需要初始化的常量

## 奇怪的语法
```dart
class Circle {
  static const pi = 3.14159; // 编译时常量，类级别共享
  final double radius; // 运行时常量，实例级别

  // 构造函数 - 参数直接赋值给radius
  Circle(this.radius);

  // 属性get
  double get area => pi * radius * radius;
}

void main() {
  var circle = Circle(5);
  print(circle.area); // 输出圆的面积
}

```
- const 构造函数
- 相当于优化 - 只要参数相同就用同一个实例
```dart
class Song {
  final Artist artist;
  final String title;
  final Duration length;
  final MyArtistImage image;

  const Song(this.title, this.artist, this.length, this.image);
}

```
##
```dart
void main() {
  // 定义变量
  var name = 'Dart'; // 自动推断类型
  String greeting = 'Hello'; // 显式指定类型
  int age = 30;

  // 定义常量 - final vs const
  final currentYear = 2024; // 运行时常量
  const pi = 3.14159; // 编译时常量
}

```

##  数据类型
- 基础类型：int，double，String，bool
- 集合类型：List，Set，Map
```dart
void main() {
  int a = 10;
  double b = 3.14;
  String s = 'Hello, Dart!';
  bool isDartFun = true;

  List<int> numbers = [1, 2, 3];
  Set<String> fruits = {'apple', 'banana'};
  Map<String, int> scores = {'Alice': 90, 'Bob': 85};
}
```
## 函数
- 类型放在前面
- closure - 匿名函数-箭头函数
```dart
// 普通函数
int add(int a, int b) {
  return a + b;
}

// 可选参数
void greet(String name, [String title = 'Mr./Ms.']) {
  print('Hello, $title $name');
}

// 命名参数
void printInfo({required String name, int age = 18}) {
  print('Name: $name, Age: $age');
}

// 匿名函数和箭头函数
void main() {
  var multiply = (int a, int b) => a * b;
  print(multiply(2, 3)); // 输出 6
}

```
## 类和对象
```dart
class Person {
  String name;
  int age;

  // 构造函数
  Person(this.name, this.age);

  // 方法
  void introduce() {
    print('My name is $name, and I am $age years old.');
  }
}

void main() {
  var person = Person('Alice', 25);
  person.introduce(); // 输出: My name is Alice, and I am 25 years old.
}

```
## 异步
- async + await
- Future<T>

```dart
Future<String> fetchData() async {
  await Future.delayed(Duration(seconds: 2)); // 模拟网络延迟
  return 'Fetched data!';
}

void main() async {
  print('Fetching...');
  String data = await fetchData();
  print(data);
}

```
## optional 
```dart
void main() {
  String? nullableString = null; // 可空变量
  print(nullableString?.length); // 安全调用
  print(nullableString ?? 'Default Value'); // 空值替代
}

```