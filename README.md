# 🖼️ Easy Editor - PyQt5 Image Editor

A simple desktop image editor built using **PyQt5** and **Pillow** (PIL).  
Supports basic image processing features like rotation, grayscale, filters, and more!

---

## 🚀 Features

- 🖼 Load images from a folder (`.jpg`, `.png`, `.gif`, `.bmp`)
- 🔁 Rotate Left / Right
- 🔄 Mirror (Flip horizontally)
- 🌑 Convert to Black & White (Grayscale)
- 🟤 Sepia filter
- 💧 Blur filter
- 🧱 Emboss filter
- 🌀 Contour filter
- ✨ Sharpness filter
- 💾 Automatically saves edited images in `Modified/` folder

---

## 📦 Requirements

- Python 3.x
- PyQt5
- Pillow (PIL)

You can install dependencies using:

```bash
pip install pyqt5 pillow
```

---

## 🧠 How It Works

- The UI is built using **QHBoxLayout** and **QVBoxLayout** to manage sidebars and toolbars.
- The app allows you to choose a folder, then displays supported image files.
- Selecting an image loads it to preview.
- Clicking a button applies an effect and saves the modified image to `Modified/`.
- The output image is displayed on the right panel.

---

## 🗂️ Project Structure

```
easy_editor.py         # Main app file
Modified/              # Automatically created for edited images
```

---

## 🖥️ Run the App

```bash
python easy_editor.py
```

Make sure your working folder contains some images to edit.

---

## 🎨 Preview

> You can add a screenshot here of your UI layout and image preview

---

## 🧑‍💻 Author

Built with ❤️ by Rucky (RUckyTheGreat)  
Learning PyQt, GUI, and image processing for real-world applications!

---

## 🪪 License

This project is open-source and free to use under the MIT License.
