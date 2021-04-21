# hello-world
new repository

#定义 图书 类、教材 类、参考书 类、期刊 类
class Book:
    def __init__(self,num,name,author,publisher,time,prise,nature='图书'):
        self.num = num
        self.name = name
        self.author = author
        self.publisher = publisher
        self.time = time 
        self.prise = prise
        self.nature = nature
    def show(self,n):
        if n==0:
            print('以下为该%s的信息'%self.nature)
            print('编号:',self.num)
            print('书名:',self.name)
            print('作者:',self.author)
            print('出版社:',self.publisher)
            print('出版时间:',self.time)
            print('价格:',self.prise)
        else :
            print(self.num,end='    ')
            print(self.name,end='    ')
            print(self.author,end='    ')
            print(self.publisher,end='    ')
            print(self.time,end='    ')
            print(self.prise,end='    ')
            print(self.nature)
class Classbook(Book):
    def __init__(self,num,name,author,publisher,time,prise):
        super().__init__(num,name,author,publisher,time,prise,nature='教材')
class Referencebook(Book):
    def __init__(self,num,name,author,publisher,time,prise):
        super().__init__(num,name,author,publisher,time,prise,nature='参考书')
class Journal(Book):
    def __init__(self,num,name,author,publisher,time,prise):
        super().__init__(num,name,author,publisher,time,prise,nature='期刊')


#用列表将实例对象储存
total = []

#键盘输入
def keyboard_input():
    
    def imformation_input():
        a = input('请输入该书的编号')
        a = int(a)
        n = 0
        for i in total:
            if i.num == a:
                n = n+1
        if n !=0:
            print('该图书编号已存在')
            return None
        else :
            b = input('请输入该书的名称')
            c = input('请输入该书的作者')
            d = input('请输入该书的出版社')
            e = input('请输入该书的出版时间')
            f = input('请输入该书的价格')
            f = int(f)
            return [a,b,c,d,e,f]
    
    while 1:
        print('''请选择输入图书的种类''')
        b = input('1.普通图书\n2.教材\n3.参考书\n4.期刊\n5.退出输入') 
        b = int(b)
        if b == 1:
            l = imformation_input()
            if l == None:
                pass
            else:
                i = Book(l[0],l[1],l[2],l[3],l[4],l[5])
                total.append(i)
        elif  b ==2:
            l = imformation_input()
            if l == None:
                pass
            else:
                i = Classbook(l[0],l[1],l[2],l[3],l[4],l[5])
                total.append(i)
        elif b==3:
            l = imformation_input()
            if l == None:
                pass
            else:
                i = Referencebook(l[0],l[1],l[2],l[3],l[4],l[5])
                total.append(i)
        elif b==4:
            l = imformation_input()
            if l == None:
                pass
            else:
                i = Journal(l[0],l[1],l[2],l[3],l[4],l[5])
                total.append(i)
        elif b==5:
            print('键盘输入结束')
            break
        else :
            print('输入错误，请重新输入')

#文件输入
def file_input():
    n = 0
    with open('图书信息.dat','r') as fp:
        for line in fp:
            l = line[:len(line)-1].split(',')
            l[0] = int(l[0])
            l[5] = int(l[5])
            for j in range(len(total)):
                if l[0] ==total[j].num:
                    n =n+1
            if n == 0:
                if l[6] == '图书':
                    i = Book(l[0],l[1],l[2],l[3],l[4],l[5])
                elif l[6] == '教材':
                    i = Classbook(l[0],l[1],l[2],l[3],l[4],l[5])
                elif l[6] == '参考书':
                    i = Referencebook(l[0],l[1],l[2],l[3],l[4],l[5])
                elif l[6] == '期刊':
                    i = Journal(l[0],l[1],l[2],l[3],l[4],l[5])
                total.append(i)
        print('文件读取成功')

#显示所有图书
def print_total():
    print('以下为所有图书的信息')
    print("依次为编号,书名,作者,出版社,出版时间,价格,类别")
    for j in range(len(total)):
        total[j].show(n=1)

#按编号查找图书
def num_search():
    a = input('请输入该书的编号')
    a = int(a)
    b = 0
    for j in range(len(total)):
        if total[j].num == a:
            total[j].show(n=0)
            b = b+1
    if b == 0:
        print('未找到该书')

#按书名查找
def name_search():
    a = input('请输入该书的书名')
    b = 0
    for j in range(len(total)):
        if total[j].name == a:
            total[j].show(n=0)
            b = b+1
    if b == 0:
        print('未找到该书')

#按编号删除
def num_delete():
    a = input('请输入所删除图书的编号')
    a = int(a)
    b = 0
    for j in range(len(total)):
        if total[j].num == a:
            total.pop(j)
            b = b+1
    if b ==0:
        print('未找到要删除的图书')

#按书名删除
def name_delete():
    a = input('请输入所删除图书的名称')
    b = 0
    for j in range(len(total)):
        if total[j].name == a:
            total.pop(j)
            b = b+1
    if b ==0:
        print('未找到要删除的图书')


#存入文件
def save_file():
    with open('图书信息.dat','w') as fp:
        for j in range(len(total)):
            fp.write(total[j].num)
            fp.write(',')
            fp.write(total[j].name)
            fp.write(',')
            fp.write(total[j].author)
            fp.write(',')
            fp.write(total[j].publisher)
            fp.write(',')
            fp.write(total[j].time)
            fp.write(',')
            fp.write(total[j].prise)
            fp.write(',')
            fp.write(total[j].nature)
            fp.write('\n')
    print('存入文件成功')                

#按编号升序排序
def num_sort():
    total.sort(key = lambda x:x.num)

#按价格降序排序
def prise_sort():
    total.sort(key= lambda x:x.prise,reverse = True)

#编辑主界面
print('这是图书管理系统')
#根据选择进行相应操作
while 1:
    print('''
1.输入图书信息
2.显示所有图书
3.查找相应图书
4.添加图书
5.删除图书
6.保存所有图书信息到文件中
7.对图书进行排序''')
    a = input('请根据编号选择功能')
    a = int(a)

    if a == 1: 
        b = input('请选择输入方式\n1.键盘输入\n2.文件输入\n')
        b = int(b)
        if b == 1:
            keyboard_input()
        else :
            file_input()

    elif a ==2:
        print_total()

    elif a ==3:
        b = input('请选择查找方式\n1.按编号查找\n2.按书名查找\n')
        b = int(b)
        if b == 1:
            num_search()
        else :
            name_search()

    elif a == 4:
       keyboard_input()

    elif a == 5:
        b = input('请选择删除图书的方式\n1.按编号删除\n2.按书名删除\n')
        b = int(b)
        if b == 1:
            num_delete()
        else :
            name_delete()

    elif a == 6:
        save_file()

    elif a == 7 :
        b = input('请选择排序方式\n1.按编号升序排序\n2.按价格降序排序\n')
        b =int(b)
        if b ==1:
            num_sort()
        else :
            prise_sort()

    else :
        print('输入错误，请重新输入')

