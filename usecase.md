Use Cases
=========
```python
import DisplayXYZ
```
+ This will set DisplayXYZ, LayerXYZ as the default Display and DrawingLayer classes for all future calls.

```python
img.show()
```
Can be mapped to
```python
img.save(display)
```
If a display doesn't exists, a new one will be created

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
+ A DrawingLayerXYZ is created and inserted into the image's drawing layer stack if one doesnt exist
+ `drawingLayer.drawCircle((10,10),5)` is called
+ A **DisplayXYZ** is created, and the image is shown by calling `display.showImage()`. DisplayXYZ knows how to draw things in a DrawingLayerXYZ


