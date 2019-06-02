![1.jpg](https://i.loli.net/2019/06/02/5cf3d5d45cf7347564.jpg)

![2.jpg](https://i.loli.net/2019/06/02/5cf3d5d69177741640.jpg)
![3.jpg](https://i.loli.net/2019/06/02/5cf3d5d6802ff97127.jpg)


用python导入了自己的数据，用支持向量回归跑了一下：
from sklearn.svm  import SVR
from sklearn import svm
import  numpy as np
from sklearn.model_selection import train_test_split
import xlrd
import matplotlib.pyplot as plt


## 构造读取数据类
class excel_read1:
    def __init__(self, excel_path=r'D:\python ex\333.xlsx',encoding='utf-8',index=0):

      self.data=xlrd.open_workbook(excel_path)  ##获取文本对象
      self.table=self.data.sheets()[index]     ###根据index获取某个sheet
      self.rows=self.table.nrows   ##3获取当前sheet页面的总行数,把每一行数据作为list放到 list

    def get_data(self):
        result=[]
        for i in range(self.rows):
            col=self.table.row_values(i)  ##获取每一行数据
            result.append(col)    ##在数组后面加上相应的元素
        return result

##  读取第二个excel
class excel_read2:
    def __init__(self, excel_path=r'D:\python ex\444.xlsx',encoding='utf-8',index=0):

      self.data=xlrd.open_workbook(excel_path)  ##获取文本对象
      self.table=self.data.sheets()[index]     ###根据index获取某个sheet
      self.rows=self.table.nrows   ##3获取当前sheet页面的总行数,把每一行数据作为list放到 list

    def get_data(self):
        result=[]
        for i in range(self.rows):
            col=self.table.row_values(i)  ##获取每一行数据
            result.append(col)    ##在数组后面加上相应的元素
        return col
## 调用读取函数
#if __name__ == '__main__':
#    excel_read().get_data()
X=excel_read1().get_data()
Y=excel_read2().get_data()

#print(X)
#print(Y)

X_train,X_test,Y_train,Y_test=train_test_split(X,Y,test_size=0.3)

#print(Y_train)
#print(Y_test)
#初始化SVR
#

clf = svm.SVR()
clf.fit(X_train, Y_train)
print(clf.predict(X_test))
print(Y_test)

plt.plot(clf.predict(X_test),Y_test)
plt.show()
