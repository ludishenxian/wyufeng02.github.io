---
layout: post
title:  导航过渡动画
tag: [code4flutter,flutterAwesome , Navigation, Material Design]
date: 2019-06-10
---

 


## [立即下载 ️⬇️ ](https://codeload.github.com/Salby/morpheus/zip/master) 


 
![](https://flutterawesome.com/content/images/2019/05/morpheus.gif)
 
>
> 用于轻松实现Material 设计导航过渡。
>

 
# Morpheus

![Pub](https://img.shields.io/pub/v/morpheus.svg)
[![Build Status](https://travis-ci.org/Salby/morpheus.svg?branch=master)](https://travis-ci.org/Salby/morpheus)

A Flutter package for easily implementing Material Design navigation transitions.

## Examples

### Parent-child transition

You can use `MorpheusPageRoute` to create a [parent-child transition](https://material.io/design/navigation/navigation-transitions.html#hierarchical-transitions) between two screens.

<img src="https://github.com/Salby/morpheus/blob/master/assets/parentchild-demo.gif" align = "right" width="30%" alt="Parent-child gif"/>

```dart
import 'package:morpheus/morpheus.dart';

class MyList extends StatelessWidget {

  @override
  Widget build(BuildContext context) {
    return ListView.builder(
      itemCount: 10,
      itemBuilder: (context, index) {
        final _parentKey = GlobalKey();
        return ListTile(
          key: _parentKey,
          leading: CircleAvatar(child: Text((index + 1).toString())),
          title: Text('Item ${index + 1}'),
          onTap: () => _handleTap(context, _parentKey),
        );
      }
    );
  }

  void _handleTap(BuildContext context, GlobalKey parentKey) {
    Navigator.of(context).push(MorpheusPageRoute(
      builder: (context) => Scaffold(),
      parentKey: parentKey,
    ));
  }

}
```

### Top-level transition

You can use the `MorpheusTabView` widget to create a [top-level transition](https://material.io/design/navigation/navigation-transitions.html#peer-transitions) when the child widget changes.

<img src="https://github.com/Salby/morpheus/blob/master/assets/toplevel-demo.gif" align = "right" width="30%" alt="Top-level gif"/>

```dart
import 'package:morpheus/morpheus.dart';

class MyTabScreen extends StatefulWidget {

  @override
  _MyTabScreenState createState() => _MyTabScreenState();

}

class _MyTabScreenState extends State<MyTabScreen> {

  final List<Widget> _screens = [
    Scaffold(backgroundColor: Colors.green),
    Scaffold(backgroundColor: Colors.red),
    Scaffold(backgroundColor: Colors.blue),
  ];
  int _currentIndex = 0;

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: MorpheusTabView(
        child: _screens[_currentIndex]
      ),
      bottomNavigationBar: BottomNavigationBar(
        currentIndex: _currentIndex,
        items: [
          BottomNavigationBarItem(
            icon: Icon(Icons.trending_up),
            title: Text('Trending'),
          ),
          BottomNavigationBarItem(
            icon: Icon(Icons.star),
            title: Text('Saved'),
          ),
        ],
        onTap: (index) {
          if (index != _currentIndex) {
            setState(() => _currentIndex = index);
          }
        },
      ),
    );
  }

}
```

## Github主页 👉[Salby/morpheus](http://github.com/Salby/morpheus)