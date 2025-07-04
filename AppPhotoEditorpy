

from PyQt5.QtWidgets import *
from PyQt5.QtCore import *
from PyQt5.QtGui import QPixmap
import os
from PIL import Image, ImageFilter
from PIL.ImageFilter import *
from PIL.ImageQt import *
from PIL import ImageOps

app = QApplication([])
main_win = QWidget()
main_win.resize(700,500)
main_win.setWindowTitle('Easy Editor')
label_image = QLabel('Image')
button_dir = QPushButton('Folder')
list_file = QListWidget()

# tombol editnya
button_left = QPushButton('Left')
button_right = QPushButton('Right')
button_mirror = QPushButton('Mirror')
button_sharp = QPushButton('Sharpness')
button_bw = QPushButton('B&W')
button_sepia = QPushButton('Sepia')
button_blur = QPushButton('Blur')
button_emboss = QPushButton('Emboss')
button_contour = QPushButton('Contour')

row = QHBoxLayout() # Main Line
column1 = QVBoxLayout() 
column2 = QVBoxLayout()

column1.addWidget(button_dir)
column1.addWidget(list_file)
column2.addWidget(label_image, 95)

row_tools = QHBoxLayout()
row_tools.addWidget(button_left)
row_tools.addWidget(button_right)
row_tools.addWidget(button_mirror)
row_tools.addWidget(button_sharp)
row_tools.addWidget(button_bw)
row_tools.addWidget(button_sepia)
row_tools.addWidget(button_blur)
row_tools.addWidget(button_emboss)
row_tools.addWidget(button_contour)
column2.addLayout(row_tools)

row.addLayout(column1, 20)
row.addLayout(column2, 80)

main_win.setLayout(row)

main_win.show()

workdir = ''

def filter(files, extentions):
    result = [] # list kosong untuk file
    for filename in files:
        for ext in extentions:
            if filename.endswith(ext):
                result.append(filename)
    return result

def chooseWorkDir():
    global workdir
    workdir = QFileDialog.getExistingDirectory()

def showFilenameList():
    extentions = ['.jpg', '.png', '.gif', '.bmp']
    chooseWorkDir()
    filenames = filter(os.listdir(workdir),extentions)
    list_file.clear()
    for filename in filenames:
        list_file.addItem(filename)

button_dir.clicked.connect(showFilenameList)

# Mulai dari sini Lesson 3:
class ImageProsessor():
    def __init__(self):
        self.image = None
        self.dir = None
        self.filename = None
        self.save_dir = "Modified/"

    def loadImage(self, dir, filename):
        self.dir = dir
        self.filename = filename
        image_path = os.path.join(dir, filename)
        self.image = Image.open(image_path)

    def do_bw(self):
        self.image = self.image.convert('L')
        self.saveimage()
        image_path = os.path.join(self.dir, self.save_dir, self.filename)
        self.showImage(image_path)

    def do_right(self):
        self.image = self.image.transpose(Image.ROTATE_270)
        self.saveimage()
        image_path = os.path.join(self.dir, self.save_dir, self.filename)
        self.showImage(image_path)

    def do_left(self):
        self.image = self.image.transpose(Image.ROTATE_90)
        self.saveimage()
        image_path = os.path.join(self.dir, self.save_dir, self.filename)
        self.showImage(image_path)

    def do_mirror(self):
        self.image = self.image.transpose(Image.FLIP_LEFT_RIGHT)
        self.saveimage()
        image_path = os.path.join(self.dir, self.save_dir, self.filename)
        self.showImage(image_path)

    def do_sharp(self):
        self.image = self.image.filter(SHARPEN)
        self.saveimage()
        image_path = os.path.join(self.dir, self.save_dir, self.filename)
        self.showImage(image_path)

    def do_sepia(self):
        sepia_image = self.image.convert("RGB")
        width, height = sepia_image.size
        pixels = sepia_image.load()

        for py in range(height):
            for px in range(width):
                r, g, b = sepia_image.getpixel((px, py))

                tr = int(0.393 * r + 0.769 * g + 0.189 * b)
                tg = int(0.349 * r + 0.686 * g + 0.168 * b)
                tb = int(0.272 * r + 0.534 * g + 0.131 * b)

                pixels[px, py] = (min(255, tr), min(255, tg), min(255, tb))

        self.image = sepia_image
        self.saveimage()
        image_path = os.path.join(self.dir, self.save_dir, self.filename)
        self.showImage(image_path)

    def do_blur(self):
        self.image = self.image.filter(ImageFilter.BLUR)
        self.saveimage()
        image_path = os.path.join(self.dir, self.save_dir, self.filename)
        self.showImage(image_path)

    def do_emboss(self):
        self.image = self.image.filter(ImageFilter.EMBOSS)
        self.saveimage()
        image_path = os.path.join(self.dir, self.save_dir, self.filename)
        self.showImage(image_path)

    def do_contour(self):
        self.image = self.image.filter(ImageFilter.CONTOUR)
        self.saveimage()
        image_path = os.path.join(self.dir, self.save_dir, self.filename)
        self.showImage(image_path)

    def saveimage(self):
        path = os.path.join(self.dir, self.save_dir)
        if not(os.path.exists(path) or os.path.isdir(path)):
            os.mkdir(path)
        image_path = os.path.join(path, self.filename)
        self.image.save(image_path)

    def showImage(self, path):
        label_image.hide()
        pixmapimage = QPixmap(path)
        w = label_image.width()
        h = label_image.height()
        pixmapimage = pixmapimage.scaled(w, h, Qt.KeepAspectRatio)
        label_image.setPixmap(pixmapimage)
        label_image.show()



workimage = ImageProsessor()

def showChosenImage():
    if list_file.currentRow() >= 0:
        filename = list_file.currentItem().text()
        workimage.loadImage(workdir, filename)
        image_path = os.path.join(workimage.dir,workimage.filename)
        workimage.showImage(image_path)

list_file.currentRowChanged.connect(showChosenImage)
button_sepia.clicked.connect(workimage.do_sepia)
button_blur.clicked.connect(workimage.do_blur)
button_emboss.clicked.connect(workimage.do_emboss)
button_contour.clicked.connect(workimage.do_contour)
button_bw.clicked.connect(workimage.do_bw)
button_left.clicked.connect(workimage.do_left)
button_right.clicked.connect(workimage.do_right)
button_mirror.clicked.connect(workimage.do_mirror)
button_sharp.clicked.connect(workimage.do_sharp)

app.exec()
