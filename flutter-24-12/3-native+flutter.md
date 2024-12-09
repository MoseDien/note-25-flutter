# iOS native + flutter
可以在一个 iOS 原生应用中嵌入 Flutter 模块。Flutter 提供了一种称为 Add-to-App 的功能，允许你将 Flutter 作为一个模块嵌入到现有的原生应用中，包括 iOS 和 Android。

iOS
- Add-to-App
- cocoapod
- FlutterEngine + FlutterViewController
- 可以多个flutter模块 - 初始化多个 FlutterEngine
- 也可以动态的load某个flutter模块引擎

Android
- FlutterActivity/FlutterFragment

## 以下是实现步骤的概述

### 步骤 1: 创建 Flutter 模块
- 在终端运行以下命令来创建一个 Flutter 模块：
- 进入模块目录，确保它可以正常运行：

```sh
flutter create -t module flutter_module

cd flutter_module
flutter build ios
```
### 步骤 2: 将 Flutter 模块集成到 iOS 原生项目
- 将 Flutter 模块作为 CocoaPods 依赖项引入： 在 iOS 原生项目的 Podfile 中，添加以下内容：
- 通过cocoapod引入

```sh
# Podfile
flutter_module_one_path = '../flutter_module_one'
flutter_module_two_path = '../flutter_module_two'

load File.join(flutter_module_one_path, '.ios', 'Flutter', 'podhelper.rb')
load File.join(flutter_module_two_path, '.ios', 'Flutter', 'podhelper.rb')

target 'YourAppTarget' do
  install_all_flutter_pods(flutter_module_one_path)
  install_all_flutter_pods(flutter_module_two_path)
end

#
pod install

```

### 3 - 代码
```sh
#import <Flutter/Flutter.h>

# swift
import Flutter
```

- 在AppDelegate引入引擎FlutterEngine
- 使用FlutterViewController
```swift
import UIKit
import Flutter

@UIApplicationMain
class AppDelegate: UIResponder, UIApplicationDelegate {
    var window: UIWindow?
    var flutterEngineOne: FlutterEngine?
    var flutterEngineTwo: FlutterEngine?

    func application(
        _ application: UIApplication,
        didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?
    ) -> Bool {
        // 初始化两个 FlutterEngine
        flutterEngineOne = FlutterEngine(name: "flutter_engine_one")
        flutterEngineOne?.run()

        flutterEngineTwo = FlutterEngine(name: "flutter_engine_two")
        flutterEngineTwo?.run()

        return true
    }
}

//
    @objc func showFlutterModuleOne() {
        guard let appDelegate = UIApplication.shared.delegate as? AppDelegate,
              let flutterEngineOne = appDelegate.flutterEngineOne else { return }
        
        let flutterVC = FlutterViewController(engine: flutterEngineOne, nibName: nil, bundle: nil)
        present(flutterVC, animated: true, completion: nil)
    }
```