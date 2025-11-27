#UI #python 

Empty Window
![[Empty Window.png | 300]]

Python Project
```Python
from PySide2.QtWidgets import QApplication, QWidget
import sys

app = QApplication(sys.argv)

window = QWidget()
window.show()

app.exec_()
```

Maya Python Project
```Python
from PySide2.QtWidgets import QApplication, QWidget

window = QWidget()
window.show()
```

```Python
class RocWidget (QWidget):
    def __init__(self):
    super().__init__()
    self.setWindowTitle("RockWidget")
    
    button1 = QPushButton("Button1")
    button2 = QPushButton("Button2")
    
    button_layout = QVBoxLayout()
    button_layout.addWidget(button1)
    button_layout.addWidget(button2)
    
    self.setLayout(button_layout)
    
def button1_clicked():
    print("Button1 Clicked")
```

QMainWindow

```Python
menu_bar = self.menuBar()
menu_bar.addMenu("")
```

```
setCentralWidget()
```

Menu

ToolBar -> Movable

Status bar
```Python
#Menubar and menus
menu_bar = self.menuBar()
file_menu = menu_bar.addMenu ("&File")
quit_action = file_menu.addAction("Quit")
quit_action.triggered.connect(self.quit)

edit_menu = menu_bar.addMenu("&Edit")
edit_menu.addAction("Copy")
edit_menu.addAction("Cut")
edit_menu.addAction("Paste")
edit_menu.addAction("Undo") 
edit_menu.addAction("Redo")

menu_bar.addMenu("&Window")
menu_bar.addMenu("&Setting")
menu_bar.addMenu("&Help")
```

Toolbar
```Python
toolbar = QToolBar("My main toolbar")
toolbar.setIconSize(QSize(16, 16)) 
self.addToolBar(toolbar)

action1 = QAction("Some Action", self)
action1.setStatusTip("Status message for some action")
action1.triggered.connect(self.toolbar_button_click)
toolbar.addAction(action1)

action2 = QAction(QIcon("start.png"), "Some other action", self)
action2.setStatusTip("Status message for some other action")
action2.triggered.connect(self.toolbar_button_click)
action2.setCheckable(True)
toolbar.addAction(action2)

toolbar.addSeparator()
toolbar.addWidget(QPushButton("Click here"))
```

Statusbar
```Python
self.setStatusBar(QStatusBar(self))

button1 = QPushButton("BUTTON1")
button1.clicked.connect(self.button1_clicked)
self.setCentralWidget(button1)
```

The Slots
```Python
def button1_clicked(self):
    print("Clicked on button1")
def toolbar_button_click(self):
    self.statusBar().showMessage("Some message ...",3000)
def quit(self):
    self.app.quit ()
```

![[some-action.png | 300]]

Toolbar.addSeparator()

QMessageBox

The hard way
```Python
def button_clicked_hard(self):
    message = QMessageBox()
    message.setMinimumSize(700,200)
    message.setWindowTitle("Message Title")
    message.set Text("something happened")
    message.setInformativeText("Do you want to do something about it ?")
    message.setIcon (QMessageBox.Critical)
    message.setstandardButtons(QMessageBox.Ok | QMessageBox.Cancel)
    message.setDefaultButton(QMessageBox.Ok)
    ret = message.exec()
    if ret == OMessageBox.Ok:
        print("User chose OK")
    else:
        print ("User chose Cancel"')
```

Simple way → ==QMessageBox.critical==

Static Message-box Methods
Can be : critical - question - information - warning - about

```Python
def button_clicked_critical(self):
    ret = QMessageBox.critical(se1f,"Message Tit1e","Critical Message!", QMessageBox.Ok | QMessageBox.Cancel)
    if ret == QMessageBox.Ok:
        print ("User chose OK")
    else :
        print ("User chose Cancel")
```
