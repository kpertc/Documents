#python #UI 

PyQt - PySide

[[PyQT-PySide Window]]
[[PyQT-PySide Components]]

<br>

### [Official Documentation](https://doc.qt.io/qtforpython/)

**Tutorial:**

  **[Tech with Tim](https://www.youtube.com/watch?v=Vde5SH8e1OQ&list=PLzMcBGfZo4-lB8MZfHPLTEHO9zJDDLpYj)**

  **[白月黑羽](http://www.byhy.net/tut/py/gui/qt_01/)**

  https://youtu.be/Z1N9JzNax2k

<br>

# QT vs Others

### **QT - Different Licenses and company**

PyQt|Riverbank Computing, early
---|---
PySide|QT


<br>

# Start to use Qt for Python

### [Starter Template](https://doc.qt.io/qtforpython/quickstart.html)

-   QT Widgets (desktop & mature)
-   QML (new support mobile embedded)

  

QT is more than just GUI
-   Network
-   Treading
-   Databases
-   ... other utility

<br>

### Three ways to create UI：

-   Using Python
    

Using a .ui with QT Designer https://doc.qt.io/qtforpython/tutorials/basictutorial/uifiles.html

QT Designer is within PyQt#-tools, or included within PySide

PySide6 `site-packages` -> `PySide6` -> `Designer.app`

-   convert to py
    
      `pyuic# -x mainwindow.ui -o ui_mainwindow.py`
    
      `pyside6-uic mainwindow.ui > ui_mainwindow.py`
    
-   direct load
    

  

Change `QObject` -> `objectName`

Preview Shortcut: Command + R