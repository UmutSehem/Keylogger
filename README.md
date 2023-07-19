# Keylogger
import sys
import os
from PyQt5.QtWidgets import QWidget,QApplication,QTextEdit,QLabel,QPushButton,QHBoxLayout,QVBoxLayout,QFileDialog
from PyQt5.QtWidgets import QAction,qApp,QMainWindow
class Notepad(QWidget):
    def __init__(self):

        super().__init__()

        self.init_ui()
        
    def init_ui(self):
        
        self.yazialani = QTextEdit()
        self.temizle = QPushButton("Temizle")
        self.dosyaac = QPushButton("Dosya Aç")
        self.kaydet = QPushButton("Notumu Kayıt Et")
        v_box = QVBoxLayout()

        v_box.addWidget(self.yazialani)
        v_box.addWidget(self.temizle)
        v_box.addWidget(self.dosyaac)
        v_box.addWidget(self.kaydet)
        


        self.setLayout(v_box)
        self.temizle.clicked.connect(self.temiz)
        self.dosyaac.clicked.connect(self.ac)
        self.kaydet.clicked.connect(self.kayit)


    def temiz(self):
        
        self.yazialani.clear()
    
    def ac(self):
        dosyaismi = QFileDialog.getOpenFileName(self,"Dosya Aç",os.getenv("Desktop"))
        
        with open(dosyaismi[0],"r") as file:
            self.yazialani.setText(file.read())



    def kayit(self):
        dosyaismi = QFileDialog.getSaveFileName(self,"Dosya Kaydet",os.getenv("Desktop"))

        with open(dosyaismi[0],"w") as file:
            file.write(self.yazialani.toPlainText())        

class Menu(QMainWindow):
    def __init__(self):
        
        super().__init__()
        
        self.pencere = Notepad()
        
        self.setCentralWidget(self.pencere)
        
        self.setWindowTitle("Notepadv2")

        self.show()









        


app = QApplication(sys.argv)
menu = Menu()
sys.exit(app.exec_())
