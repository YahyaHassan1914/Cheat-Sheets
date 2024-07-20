## **PySide Cheat Sheet**

### **1. Basics**

- **Hello World**
  ```python
  from PySide2.QtWidgets import QApplication, QLabel

  app = QApplication([])
  label = QLabel("Hello, World!")
  label.show()
  app.exec_()
  ```

- **Basic Widgets**
  ```python
  from PySide2.QtWidgets import QApplication, QPushButton, QVBoxLayout, QWidget

  app = QApplication([])

  window = QWidget()
  layout = QVBoxLayout()

  button1 = QPushButton("Button 1")
  button2 = QPushButton("Button 2")

  layout.addWidget(button1)
  layout.addWidget(button2)

  window.setLayout(layout)
  window.show()

  app.exec_()
  ```

- **Layouts**
  ```python
  from PySide2.QtWidgets import QApplication, QWidget, QVBoxLayout, QPushButton, QHBoxLayout

  app = QApplication([])

  window = QWidget()
  layout = QVBoxLayout()

  hbox = QHBoxLayout()
  button1 = QPushButton("Button 1")
  button2 = QPushButton("Button 2")
  hbox.addWidget(button1)
  hbox.addWidget(button2)

  layout.addLayout(hbox)

  button3 = QPushButton("Button 3")
  layout.addWidget(button3)

  window.setLayout(layout)
  window.show()

  app.exec_()
  ```

### **2. Signals and Slots**

- **Connecting Signals to Slots**
  ```python
  from PySide2.QtWidgets import QApplication, QPushButton, QLabel, QVBoxLayout, QWidget

  def on_button_click():
      label.setText("Button clicked!")

  app = QApplication([])

  window = QWidget()
  layout = QVBoxLayout()

  button = QPushButton("Click Me")
  label = QLabel("")

  button.clicked.connect(on_button_click)

  layout.addWidget(button)
  layout.addWidget(label)

  window.setLayout(layout)
  window.show()

  app.exec_()
  ```

- **Custom Signals**
  ```python
  from PySide2.QtCore import Signal, QObject
  from PySide2.QtWidgets import QApplication, QPushButton, QLabel, QVBoxLayout, QWidget

  class Communicator(QObject):
      custom_signal = Signal()

  def on_custom_signal():
      label.setText("Custom signal emitted!")

  app = QApplication([])

  communicator = Communicator()
  communicator.custom_signal.connect(on_custom_signal)

  window = QWidget()
  layout = QVBoxLayout()

  button = QPushButton("Emit Signal")
  label = QLabel("")

  button.clicked.connect(communicator.custom_signal.emit)

  layout.addWidget(button)
  layout.addWidget(label)

  window.setLayout(layout)
  window.show()

  app.exec_()
  ```

### **3. Widgets and Controls**

- **Line Edit and Text Edit**
  ```python
  from PySide2.QtWidgets import QApplication, QLineEdit, QTextEdit, QVBoxLayout, QWidget

  app = QApplication([])

  window = QWidget()
  layout = QVBoxLayout()

  line_edit = QLineEdit()
  text_edit = QTextEdit()

  layout.addWidget(line_edit)
  layout.addWidget(text_edit)

  window.setLayout(layout)
  window.show()

  app.exec_()
  ```

- **ComboBox and ListView**
  ```python
  from PySide2.QtWidgets import QApplication, QComboBox, QListView, QVBoxLayout, QWidget
  from PySide2.QtCore import QStringListModel

  app = QApplication([])

  window = QWidget()
  layout = QVBoxLayout()

  combo_box = QComboBox()
  combo_box.addItems(["Item 1", "Item 2", "Item 3"])

  list_view = QListView()
  model = QStringListModel(["Item A", "Item B", "Item C"])
  list_view.setModel(model)

  layout.addWidget(combo_box)
  layout.addWidget(list_view)

  window.setLayout(layout)
  window.show()

  app.exec_()
  ```

### **4. Dialogs**

- **Message Box**
  ```python
  from PySide2.QtWidgets import QApplication, QMessageBox, QPushButton, QVBoxLayout, QWidget

  def show_message():
      QMessageBox.information(window, "Title", "Message Content")

  app = QApplication([])

  window = QWidget()
  layout = QVBoxLayout()

  button = QPushButton("Show Message")
  button.clicked.connect(show_message)

  layout.addWidget(button)
  window.setLayout(layout)
  window.show()

  app.exec_()
  ```

- **File Dialog**
  ```python
  from PySide2.QtWidgets import QApplication, QFileDialog, QPushButton, QVBoxLayout, QWidget

  def open_file():
      file_name, _ = QFileDialog.getOpenFileName(window, "Open File")
      if file_name:
          print(f"Selected file: {file_name}")

  app = QApplication([])

  window = QWidget()
  layout = QVBoxLayout()

  button = QPushButton("Open File Dialog")
  button.clicked.connect(open_file)

  layout.addWidget(button)
  window.setLayout(layout)
  window.show()

  app.exec_()
  ```

### **5. Advanced Widgets**

- **Graphics View Framework**
  ```python
  from PySide2.QtWidgets import QApplication, QGraphicsScene, QGraphicsView, QGraphicsEllipseItem, QVBoxLayout, QWidget

  app = QApplication([])

  scene = QGraphicsScene()
  ellipse = QGraphicsEllipseItem(0, 0, 100, 100)
  scene.addItem(ellipse)

  view = QGraphicsView(scene)

  window = QWidget()
  layout = QVBoxLayout()
  layout.addWidget(view)
  window.setLayout(layout)
  window.show()

  app.exec_()
  ```

- **Tree View and Table View**
  ```python
  from PySide2.QtWidgets import QApplication, QTreeView, QStandardItemModel, QStandardItem, QVBoxLayout, QWidget

  app = QApplication([])

  model = QStandardItemModel()
  root_item = model.invisibleRootItem()

  item1 = QStandardItem("Item 1")
  item2 = QStandardItem("Item 2")
  root_item.appendRow(item1)
  root_item.appendRow(item2)

  tree_view = QTreeView()
  tree_view.setModel(model)

  window = QWidget()
  layout = QVBoxLayout()
  layout.addWidget(tree_view)
  window.setLayout(layout)
  window.show()

  app.exec_()
  ```

### **6. Layout Management**

- **Grid Layout**
  ```python
  from PySide2.QtWidgets import QApplication, QWidget, QGridLayout, QPushButton

  app = QApplication([])

  window = QWidget()
  layout = QGridLayout()

  for i in range(3):
      for j in range(3):
          button = QPushButton(f"Button {i},{j}")
          layout.addWidget(button, i, j)

  window.setLayout(layout)
  window.show()

  app.exec_()
  ```

### **7. Custom Widgets**

- **Custom Widget Example**
  ```python
  from PySide2.QtWidgets import QWidget, QLabel, QVBoxLayout
  from PySide2.QtGui import QPainter
  from PySide2.QtCore import Qt

  class CustomWidget(QWidget):
      def __init__(self, parent=None):
          super(CustomWidget, self).__init__(parent)
          self.setFixedSize(200, 100)
      
      def paintEvent(self, event):
          painter = QPainter(self)
          painter.setBrush(Qt.green)
          painter.drawRect(self.rect())
      
  app = QApplication([])

  window = QWidget()
  layout = QVBoxLayout()
  
  custom_widget = CustomWidget()
  layout.addWidget(custom_widget)
  
  window.setLayout(layout)
  window.show()

  app.exec_()
  ```

### **8. Threads and Concurrency**

- **Using QThread**
  ```python
  from PySide2.QtCore import QThread, Signal
  from PySide2.QtWidgets import QApplication, QLabel, QVBoxLayout, QWidget
  import time

  class Worker(QThread):
      update_signal = Signal(str)

      def run(self):
          for i in range(5):
              time.sleep(1)
              self.update_signal.emit(f"Update {i}")

  app = QApplication([])

  window = QWidget()
  layout = QVBoxLayout()

  label = QLabel("Starting...")
  layout.addWidget(label)
  
  worker = Worker()
  worker.update_signal.connect(label.setText)
  worker.start()

  window.setLayout(layout)
  window.show()

  app.exec_()
  ```

### **9. Styles and Themes**

- **Applying Stylesheets**
  ```python
  from PySide2.QtWidgets import QApplication, QPushButton, QWidget, QVBoxLayout

  app = QApplication([])

  window = QWidget()
  layout = QVBoxLayout()

  button = QPushButton("Styled Button")
  button.setStyleSheet("background-color: lightblue; font-size: 20px;")

  layout.addWidget(button)
  window.setLayout(layout)
  window.show()

  app.exec_()
  ```

### **10. Best Practices**

- **Avoid Blocking the GUI**
  - Use QThread or async tasks to perform long-running operations.

- **Signal-Slot Connections**
  - Always disconnect signals to avoid memory leaks if they are no longer needed.

- **Proper Widget Cleanup**
  - Ensure widgets are properly destroyed to avoid resource leaks.

- **Use Layouts**
  - Avoid absolute positioning of widgets. Use

 layouts to ensure proper resizing and positioning.

---

This cheat sheet provides a thorough overview of PySide, from basic usage to more advanced features. It should serve as a handy reference while working with PySide applications.