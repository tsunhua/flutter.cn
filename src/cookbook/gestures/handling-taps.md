---
title: Handle taps
title: 捕获和处理点击动作
description: How to handle tapping and dragging.
description: 如何处理点击和拖拽。
tags: cookbook, 实用教程, 手势操作
keywords: 交互,点击,拖动,snackbar
prev:
  title: Add Material touch ripples
  title: 添加点按涟漪效果 (Material Design)
  path: /docs/cookbook/gestures/ripples
next:
  title: Implement swipe to dismiss
  title: 实现「滑动清除」效果
  path: /docs/cookbook/gestures/dismissible
js:
  - defer: true
    url: https://dartpad.cn/inject_embed.dart.js
---

<?code-excerpt path-base="cookbook/gestures/handling_taps/"?>

You not only want to display information to users,
you want users to interact with your app.
Use the [`GestureDetector`][] widget to respond
to fundamental actions, such as tapping and dragging.

我们的 app 不仅要把信息展示给用户，还要和用户进行交互。
怎么响应用户的点击，拖动等操作行为呢？
——使用 [`GestureDetector`][] Widget。

{{site.alert.note}}

  To learn more, watch this short Widget of the Week video on the GestureDetector widget:

  了解更多，请参考下方「每周 Widget」的里关于 GestureDetector 的短视频：

  <iframe class="full-width" src="{{site.youtube-site}}/embed/WhVXkCFPmK4" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

{{site.alert.end}}

This recipe shows how to make a custom button that shows
a snackbar when tapped with the following steps:

你可以通过以下步骤来实现一个按钮，
当用户点击的时候显示 snackbar 消息：

  1. Create the button.

     创建一个按钮。

  2. Wrap it in a `GestureDetector` that an `onTap()` callback.

     用 `GestureDetector` 包裹按钮，并传入 `onTap` 回调函数。

<?code-excerpt "lib/main.dart (GestureDetector)" replace="/return //g;/;$//g"?>
```dart
// The GestureDetector wraps the button.
GestureDetector(
  // When the child is tapped, show a snackbar.
  onTap: () {
    const snackBar = SnackBar(content: Text('Tap'));

    ScaffoldMessenger.of(context).showSnackBar(snackBar);
  },
  // The custom button
  child: Container(
    padding: const EdgeInsets.all(12.0),
    decoration: BoxDecoration(
      color: Colors.lightBlue,
      borderRadius: BorderRadius.circular(8.0),
    ),
    child: const Text('My Button'),
  ),
)
```

## Notes

## 注意

  1. For information on adding the Material ripple effect to your
     button, see the [Add Material touch ripples][] recipe.
      
     如果你想添加点按涟漪效果 (Material Design) 请参考文章 
     [添加点按涟漪效果 (Material Design)][Add Material touch ripples]。

  2. Although this example creates a custom button,
     Flutter includes a handful of button implementations, such as:
     [`ElevatedButton`][], [`TextButton`][], and
     [`CupertinoButton`][].

     这里为了说明原理，我们创建了自定义的按钮，
     其实 Flutter 已经为我们准备了很多现成的按钮供我们使用，比如：
     [`ElevatedButton`][]、[`TextButton`][] 和 [`CupertinoButton`][]。

## Interactive example

## 交互式样例

<?code-excerpt "lib/main.dart"?>
```run-dartpad:theme-light:mode-flutter:run-true:width-100%:height-600px:split-60:ga_id-interactive_example
import 'package:flutter/material.dart';

void main() => runApp(const MyApp());

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    const title = 'Gesture Demo';

    return const MaterialApp(
      title: title,
      home: MyHomePage(title: title),
    );
  }
}

class MyHomePage extends StatelessWidget {
  final String title;

  const MyHomePage({super.key, required this.title});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text(title),
      ),
      body: const Center(
        child: MyButton(),
      ),
    );
  }
}

class MyButton extends StatelessWidget {
  const MyButton({super.key});

  @override
  Widget build(BuildContext context) {
    // The GestureDetector wraps the button.
    return GestureDetector(
      // When the child is tapped, show a snackbar.
      onTap: () {
        const snackBar = SnackBar(content: Text('Tap'));

        ScaffoldMessenger.of(context).showSnackBar(snackBar);
      },
      // The custom button
      child: Container(
        padding: const EdgeInsets.all(12.0),
        decoration: BoxDecoration(
          color: Colors.lightBlue,
          borderRadius: BorderRadius.circular(8.0),
        ),
        child: const Text('My Button'),
      ),
    );
  }
}
```

<noscript>
  <img src="/assets/images/docs/cookbook/handling-taps.gif" alt="Handle taps demo" class="site-mobile-screenshot" />
</noscript>


[Add Material touch ripples]: {{site.url}}/cookbook/gestures/ripples
[`CupertinoButton`]: {{site.api}}/flutter/cupertino/CupertinoButton-class.html
[`TextButton`]: {{site.api}}/flutter/material/TextButton-class.html
[`GestureDetector`]: {{site.api}}/flutter/widgets/GestureDetector-class.html
[`ElevatedButton`]: {{site.api}}/flutter/material/ElevatedButton-class.html
