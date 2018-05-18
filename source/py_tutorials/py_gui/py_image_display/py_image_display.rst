.. _Display_Image:

Getting Started with Images 图像处理入门
*****************************

Goals 目标
======

.. container:: enumeratevisibleitemswithsquare

    * 在此，您将了解如何读取，显示与保存图像
    * 您将学会使用函数 : **cv2.imread()**, **cv2.imshow()** , **cv2.imwrite()**
    * 可选： 学会如何利用Matplotlib显示图像

使用 OpenCV
=============

读取图像
--------------

使用函数 **cv2.imread()** 读取图像。 第一个参数指定图片保存路径(全路径or当前路径)。

第二个参数为读取图像方式的标记位：

* cv2.IMREAD_COLOR : 默认值，带色彩模式加载，透明背景层将被无视。
* cv2.IMREAD_GRAYSCALE : 灰度图模式加载
* cv2.IMREAD_UNCHANGED : Loads image as such including alpha channel

.. note:: 也可以使用1,0,-1来传递该参数。

参见下方代码:
::
    
    import numpy as np
    import cv2
    
    # Load an color image in grayscale
    img = cv2.imread('messi5.jpg',0)
    
.. warning:: 即使图片路径不正确，此步也不会报出任何错误，但是在 ``print img`` 中将会返回 ``None``

显示图像
-----------------

使用函数 **cv2.imshow()** 可以打开一个窗口以显示图像。窗口尺寸依据图片自动调整。

First argument is a window name which is a string. second argument is our image. You can create as many windows as you wish, but with different window names.
::
    
    cv2.imshow('image',img)
    cv2.waitKey(0)
    cv2.destroyAllWindows()

A screenshot of the window will look like this (in Fedora-Gnome machine):

     .. image:: images/opencv_screenshot.jpg
              :alt: Screenshot of Image Window in OpenCV
              :align: center 
   
**cv2.waitKey()** is a keyboard binding function. Its argument is the time in milliseconds. The function waits for specified milliseconds for any keyboard event. If you press any key in that time, the program continues. If **0** is passed, it waits indefinitely for a key stroke. It can also be set to detect specific key strokes like, if key `a` is pressed etc which we will discuss below.

**cv2.destroyAllWindows()** simply destroys all the windows we created. If you want to destroy any specific window, use the function **cv2.destroyWindow()** where you pass the exact window name as the argument.

.. note:: There is a special case where you can already create a window and load image to it later. In that case, you can specify whether window is resizable or not. It is done with the function **cv2.namedWindow()**. By default, the flag is ``cv2.WINDOW_AUTOSIZE``. But if you specify flag to be ``cv2.WINDOW_NORMAL``, you can resize window. It will be helpful when image is too large in dimension and adding track bar to windows.

See the code below:
::
    
    cv2.namedWindow('image', cv2.WINDOW_NORMAL)
    cv2.imshow('image',img)
    cv2.waitKey(0)
    cv2.destroyAllWindows()
    
Write an image
---------------

Use the function **cv2.imwrite()** to save an image.

First argument is the file name, second argument is the image you want to save.
::
    
    cv2.imwrite('messigray.png',img)

This will save the image in PNG format in the working directory. 

Sum it up
---------------

Below program loads an image in grayscale, displays it, save the image if you press 's' and exit, or simply exit without saving if you press `ESC` key.
::
    
    import numpy as np
    import cv2
    
    img = cv2.imread('messi5.jpg',0)
    cv2.imshow('image',img)
    k = cv2.waitKey(0)
    if k == 27:         # wait for ESC key to exit
        cv2.destroyAllWindows()
    elif k == ord('s'): # wait for 's' key to save and exit
        cv2.imwrite('messigray.png',img)
        cv2.destroyAllWindows()
    
.. warning:: If you are using a 64-bit machine, you will have to modify ``k = cv2.waitKey(0)`` line as follows : ``k = cv2.waitKey(0) & 0xFF``

Using Matplotlib
=================

Matplotlib is a plotting library for Python which gives you wide variety of plotting methods. You will see them in coming articles. Here, you will learn how to display image with Matplotlib. You can zoom images, save it etc using Matplotlib.
::
    
    import numpy as np
    import cv2
    from matplotlib import pyplot as plt
    
    img = cv2.imread('messi5.jpg',0)
    plt.imshow(img, cmap = 'gray', interpolation = 'bicubic')
    plt.xticks([]), plt.yticks([])  # to hide tick values on X and Y axis
    plt.show()
    
A screen-shot of the window will look like this :

     .. image:: images/matplotlib_screenshot.jpg
              :alt: Screenshot of Image Window in Matplotlib
              :align: center 
    
.. seealso:: Plenty of plotting options are available in Matplotlib. Please refer to Matplotlib docs for more details. Some, we will see on the way.

.. warning:: Color image loaded by OpenCV is in BGR mode. But Matplotlib displays in RGB mode. So color images will not be displayed correctly in Matplotlib if image is read with OpenCV. Please see the exercises for more details.

Additional Resources
======================

#. `Matplotlib Plotting Styles and Features <http://matplotlib.org/api/pyplot_api.html>`_

Exercises
==========

#. There is some problem when you try to load color image in OpenCV and display it in Matplotlib. Read `this discussion <http://stackoverflow.com/a/15074748/1134940>`_ and understand it.
