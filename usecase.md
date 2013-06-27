Use Cases
=========
```python
import DisplayXYZ
```
> This will set DisplayXYZ, LayerXYZ as the default Display and DrawingLayer classes for all future calls.

```python
img.show()
```
Can be mapped to
```python
img.save(display)
```
If a display doesn't exists, a new one will be created

## 1.Bare Minimum
```python
img = Image('lenna')
img.show()
```
> Image Created
> 

