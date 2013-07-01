Use Cases
=========
```python
import DisplayXYZ
```
+ This will set DisplayXYZ, DrawingLayerXYZ as the default Display and DrawingLayer classes for all future calls.

```python
img.show()
```
Can be mapped to
```python
img.save(display)
```
If a display doesn't exists, a new one will be created. The display always containt a pointer to the current Image being shown

### 1.Bare Minimum
```python
img = Image('lenna')
img.show()
```
+ Image Created
+ A **DisplayXYZ** is created, and the image is shown by calling `display.showImage()`

### 2.Drawing things
```python
img = Image('lenna')
img.drawCircle((10,10),5)
img.show()
```
+ Image Created
+ A **DrawingLayerXYZ** is created and inserted into the image's drawing layer stack if one doesnt exist
+ `drawingLayer.drawCircle((10,10),5)` is called, which also stored a vector representaion of the figure in the Layer
+ A **DisplayXYZ** is created, and the image is shown by calling `display.showImage()`. **DisplayXYZ** knows how to draw things in a DrawingLayerXYZ

### 3.Feature Set
```python
img = Image('lenna')
fs = img.findLines()
img.draw(fs,width=2)
img.show()
```
+ Image Created
+ Feature Set formed
+ **DrawingLayerXYZ** is created is none exists and pushed into stack.
+ `fs` is drawn on by `drawingLayer.draw*`, which also stored a vector representaions of the figure in the Layer
+ A **DisplayXYZ** is created, and the image is shown by calling `display.showImage()`.

### 4.Applying Layers
```python
img = Image('lenna')
img.drawCircle((10,10),5)
drawing = img.applyLayers()
drawing.save('new.jpg')
```
+ Image created 
+ A **DrawingLayerXYZ** is created and inserted into the image's drawing layer stack if one doesnt exist
+ `drawingLayer.drawCircle((10,10),5)` is called, which also stored a vector representaion of the figure in the Layer
+ `applyLayers` iterated through drawing layers forming a bitmap specific to **XYZLib**
+ SimpleCV image object is retuned (most probably by calling `toString()` internally)
+ Image saved

### 5.Events
```python
d = DisplayXYZ((640,480))
#user clicks
d.leftMouse()
```
+ Display Created
+ **LibXYZ** cateches the event and assigns the position `(x,y)` to a local variable
+ `leftMouse()` returns `(x,y)`

Use Cases - Notebook
====================

### 1.Bare Minimum
```python
img = Image('lenna')
img.show()
```
+ Image Created
+ A **DisplayNB** is created, it initializes a web server to serve SimpleCV images seperately, on a different port than the IPy Notebook. Each Image displayed on DIsplayNB has a unique URL(mostly derived from `id()`) off which it serves images.
+ Image Class should have a dirty bit, to know if the user changes data manually
+ When `display.showImage()` is called, it injects Javascript into the Notebook to pop a widnow, and point to the URL
+ The JS to be inserted will be a well defined template which will contain all the code nexessary to catch events and communicate the the Python kernel.

### 2.Drawing things
```python
img = Image('lenna')
img.drawCircle((10,10),5)
img.show()
```
+ Image Created
+ A **DrawingLayerNB** is created and inserted into the image's drawing layer stack if one doesnt exist
+ `drawingLayer.drawCircle((10,10),5)` is called, which also stored a vector representaion of the figure in the Layer.
+ `display.showImage()`t injects Javascript into the Notebook to pop a widnow. 
+ For all the layers present, appropriate processing code is inserted into the window. This way, if the user draws something else, only the drawing code is reloaded (image and js are cached)

### 3.Feature Set
```python
img = Image('lenna')
fs = img.findLines()
img.draw(fs,width=2)
img.show()
```
+ Image Created
+ Feature Set formed
+ **DrawingLayerNB** is created is none exists and pushed into stack.
+ `fs` is drawn on by `drawingLayer.draw*`, which also stored a vector representaions of the figure in the Layer
+ A **DisplayXYZ** is created, and the image is shown by calling `display.showImage()`.
+ Appropriate JS and processing code is inserted as described above.

### 4.Applying Layers
```python
img = Image('lenna')
img.drawCircle((10,10),5)
drawing = img.applyLayers()
drawing.save('new.jpg')
```
+ Image created 
+ A **DrawingLayerNB** is created and inserted into the image's drawing layer stack if one doesnt exist
+ `drawingLayer.drawCircle((10,10),5)` is called, which also stored a vector representaion of the figure in the Layer
+ `applyLayers` iterated through drawing layers forming a bitmap . Drawing will be done by OpenCV methods
+ Image saved


### 5.Events
```python
d = DisplayXYZ((640,480))
#user clicks
d.leftMouse()
```
+ Display Created
+ Client side Javascript catched the event and calls `IPython.notebook.kernel.execute()` to pass the event to the python kernel with (x,y) values
+ `leftMouse()` returns `(x,y)`





