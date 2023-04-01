#python #UI 


```Python
from PySide2.QtWidgets import 
QApplication, # application, no need for maya
QMainWindow, # a window
QWidget, # a child window
QPushButton,
```

<br>

### Layout

-   QVBoxLayout
-   QHBoxLayout

<br>

### Tabs

``` python
tabs = QTabWidget()

tabs.addTab(tab1, "表格节点") → need setLayout
tabs.addTab(tab2, "图片本地化")  → need setLayout

mainLayout.addWidget(tabs)

```

<br>

### Move
``` python
button.move(300,200)
```
  
<br>
### `QLabel`
```python 
QLabel("直径")
```


<br>

### `QPushButton`

```python
button = QPushButton("Click")

button.setText("Press Me") # reset text

QB_png.clicked.connect( function-or-lamda )
button.clicked.connect(lambda *args, **kwargs: print(args, kwargs))

button.clicked.connect(self.button_clicked)
button.pressed.connect(self.button_pressed)
button.released.connect(self.button_released)
```

Widget need have basic layout

``` python 

mainLayout = QVBoxLayout()
self.setLayout(mainLayout)

```

<br>

### `QCheckBox()`

```python
isOverWritten = QCheckBox("是否覆盖源文件")

print( isOverWritten.isChecked() )
```

<br>

### `QLineEdit()`

``` python

_QLineEdit= QLineEdit()

_QLineEdit.setText( ... )

_QLineEdit.textChanged.connect( lambda : _QLineEdit.setText( ... ) )

```

<br>

### `QPlainTextEdit`

``` python
loggingWindow = QPlainTextEdit()
loggingWindow.setReadOnly(True)
```

<br>

### `QFileDialog`

File(s)
```python
# Single File
path = QFileDialog.getOpenFileName()[0]
# Multiple Files
path = QFileDialog.getOpenFileName()[0]

# set path / filter ...
qfd = QFileDialog()
path = ""
filter = "Markdown filse only (*.md)"
_path = QFileDialog.getOpenFileNames(qfd, "title", path, filter)

```

Directory
``` python
path = QFileDialog.getExistingDirectory()
```

<br>

### `QSlider`

```Python
def printValue(data):
    print(data)
    
slider = QSlider(Qt.Horizontal)

slider.setMinimum(1)
slider.setMaximum(100)
slider.setValue(25)
slider.valueChanged.connect(printValue)

slider.show() 
```