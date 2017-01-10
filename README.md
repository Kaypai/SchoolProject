##Unable to load qwidget

class MyWindow(QtGui.QMainWindow):
    def __init__(self):
        super(MyWindow, self).__init__()
        uic.loadUi('untitled.ui', self)
        
        
        self.show()
        
class QTestWidget (QtGui.QWidget):
    def __init__ (self):
        super(QTestWidget, self).__init__()
        allSQLRows= cursor.fetchall()
        self.tableWidget.setRowCount(len(allSQLRows,self))
        self.refreshTable.clicked.connect(self.refreshTable)
        self.tableWidget.setColumnCount(8)
        myQTestWidget.show()

        
if __name__ == '__main__':
    app = QtGui.QApplication(sys.argv)
    window = MyWindow()
    sys.exit(app.exec_())






config = {"host":"localhost",
          "user":"root",
          "passwd":"C0mput!ngict",
          "db":"testK"}
db = mysql.connector.connect(**config)
cur = db.cursor()
       
countT = 1
 
cur.execute("CREATE TABLE IF NOT EXISTS  productsK(Id INT PRIMARY KEY AUTO_INCREMENT, productName VARCHAR(25) , Price real)",)

def cLine():
    
    countL = 1
   
    while countL == 1:
        cmd = input(": ")
        cmdT = cmd.split()
        if cmdT[0] == "add":
            cur.execute("INSERT INTO productsK(productName, Price) VALUES(%s,%s)", (cmdT[1], cmdT[2]) )           
        if cmdT[0] == "remove":
            cur.execute("delete from productsK where productName = '%s' ", cmdT[1])    
        if cmdT[0] == "quit":
            countL = 2
        if cmdT[0] == "print":
            if cmdT[1] == "current":
                cur.execute("SELECT * FROM productsK")
                for x in cur.fetchall():
                    print(x)
        if cmdT[0] == "blank":
            print("Are you sure?")
            opT = input(": ")
            if opT == "yes":
               cur.execute("truncate productsK")
            else:
                print("No clearing")
        if cmdT[0] == "clear":
            for i in range(100):
                print("")
        if cmdT[0] == "commit":
            db.commit()                                 
        
                
                
 
cLine()
db.commit()
db.close()
