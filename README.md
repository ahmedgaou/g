from cProfile import label
from cgitb import text
from code import interact
from email.headerregistry import Address
from os import remove
from pickle import FRAME
import string
from  tkinter import * 
from  tkinter import ttk
from tkinter import messagebox
from turtle import width
from unicodedata import name
from click import style
from colorama import Style
from mysqlx import Row
from numpy import imag, place
from db import Database
db=Database("employess.db")

#==========bisec heder===========
root=Tk()
root.title("MyFill")
root.geometry('1210x615+0+0')
root.resizable(False,False)
root.configure(bg="#3d6466")
#======================db=====
names = StringVar()
job = StringVar()
gender = StringVar()
age = StringVar()
mobile = StringVar()
   
#========imge===========
logo = PhotoImage(file='woww.png')
libel_img= Label(root,imag=logo,bg="#3d6466")
libel_img.place(x=5,y=410)
#===============senerf============
snterf_frem= Frame(root,bg="#0000CD")
snterf_frem.place(x=1,y=1,width=400,height=510)
title_a=Label (snterf_frem,text="Members File",font= ("Calibri",18,"bold"),bg="#0000CD",fg="white")
title_a.place(x=10,y=1)
libelnam= Label(snterf_frem,text="Name",font= ("Calibri",15,"bold"),bg="#0000CD",fg="white")
libelnam.place(x=10,y=50)
interynam= Entry(snterf_frem,textvariable=names,width=20,font= ("Calibri",15,"bold"),bg="white")
interynam.place(x=110,y=50)
libeljop= Label(snterf_frem,text="Job",font= ("Calibri",15,"bold"),bg="#0000CD",fg="white")
libeljop.place(x=10,y=90)
interjop= Entry(snterf_frem,textvariable=job,width=20,font= ("Calibri",15,"bold"),bg="white")
interjop.place(x=110,y=90)
libelgender= Label(snterf_frem,text="Gender",font= ("Calibri",15,"bold"),bg="#0000CD",fg="white")
libelgender.place(x=10,y=130)
intergender= Entry(snterf_frem,width=20,font= ("Calibri",15,"bold"),bg="white")
compogender= ttk.Combobox(snterf_frem,textvariable=gender,width=18,state="readonly",font= ("Calibri",15,"bold"))
compogender["value"]=("Male","Fmale")
compogender.place(x=110,y=130)
libelage= Label(snterf_frem,text="Age",font= ("Calibri",15,"bold"),bg="#0000CD",fg="white")
libelage.place(x=10,y=170)
interage= Entry(snterf_frem,textvariable=age,width=20,font= ("Calibri",15,"bold"),bg="white")
interage.place(x=110,y=170)
libelconuct= Label(snterf_frem,text="Mobile",font= ("Calibri",15,"bold"),bg="#0000CD",fg="white")
libelconuct.place(x=10,y=210)
libelconuct= Entry(snterf_frem,textvariable=mobile,width=20,font= ("Calibri",15,"bold"),bg="white")
libelconuct.place(x=110,y=210)
libeladress= Label(snterf_frem,text="Adress : ",font= ("Calibri",15,"bold"),bg="#0000CD",fg="white")
libeladress.place(x=10,y=250)
textadress = Text(snterf_frem,width=31,height=2,font= ("Calibri",15,"bold"))
textadress.place(x=2,y=280)
#============ Difine ============
def hide():
    root.geometry("340x515")
def show():
   root.geometry('1210x615+0+0')

betnhide=Button(snterf_frem,text="HIDE",cursor='hand2',bg='white',bd=1,relief=SOLID,command=hide)
betnhide.place(x=240,y=10)
betnshow=Button(snterf_frem,text="SHOW",bg='white',bd=1,relief=SOLID, cursor='hand2',command=show)
betnshow.place(x=290,y=10)
def getaData(event):
 selected_row=tv.focus()
 data=tv.item(selected_row)
 global row 
 row= data["values"]
 names.set(row[1])
 job.set(row[2])
 gender.set(row[3])
 age.set(row[4])
 mobile.set(row[5])
 textadress.delete(1.0,END)
 textadress.insert(END,row[6])
def displayALL():
    tv.delete(*tv.get_children())
    for row in db.fetch():
     tv.insert("",END,values=row)
def Clear():
    names.set("")
    job.set("")
    gender.set("")
    age.set("")
    mobile.set("")
    textadress.delete(1.0,END)
def delete():
    db.remove(row[0])
    Clear()
    displayALL()
def add_employee(): 
     if interynam.get()=="" or interjop.get()=="" or compogender.get()=="" or interage.get()=="" or libelconuct.get() =="" or textadress.get(1.0,END) =="" :
        messagebox.showerror("errer","please fill all the items")
        return
     db.insert(
        interynam.get(),
        interjop.get(),
        compogender.get(),
        interage.get(),
        libelconuct.get(),
        textadress.get(1.0,END)
       )
     messagebox.showinfo("Success","Add new Employee")
     displayALL()
     Clear()
def Update():
     if interynam.get()=="" or interjop.get()=="" or compogender.get()=="" or interage.get()=="" or libelconuct.get() =="" or textadress.get(1.0,END) =="" :
        messagebox.showerror("errer","please fill all the items")
        return
     db.update(row[0],

        interynam.get(),
        interjop.get(),
        compogender.get(),
        interage.get(),
        libelconuct.get(),
        textadress.get(1.0,END)
     )
     messagebox.showinfo("Success","the employee data is update")
     displayALL()
     Clear()
#============= Buttons frame============
bet_frame=Frame(snterf_frem,bg="#0000CD",bd=1,relief=SOLID)
bet_frame.place(x=1,y=340,width=320,height=100)
btnadd=Button(bet_frame,
 text="ADD NEW",
 width=14,
 height=1,
 font= ("Calibri",15,"bold"),
 fg="white",
 bg="green",
 bd=0, 
 command=add_employee
)
btnadd.place(x=4,y=5)
btndelet=Button(bet_frame,
 text="DELETE",
 width=14,
 height=1,
 font= ("Calibri",15,"bold"),
 fg="white",
 bg="red",
 bd=0,
 command= delete
)
btndelet.place(x=4,y=50)
btndelit=Button(bet_frame,
 text="UPDATE",
 width=14,
 height=1,
 font= ("Calibri",15,"bold"),
 fg="white",
 bg="#8A360F",
 bd=0,
 command= Update
)
btndelit.place(x=170,y=5)
btnClear=Button(bet_frame,
 text="CLEARS",
 width=14,
 height=1,
 font= ("Calibri",15,"bold"),
 fg="white",
 bg="#FF6103",
 bd=0,
 command = Clear
)
btnClear.place(x=170,y=50)
#============ tables frame ======
tree_Frame=Frame(root,bg="white")
tree_Frame.place(x=340,y=1,width=860,height=610)
style=ttk.Style()
style.configure("mystyle.Treeview",font= ("Calibri",13,"bold"),rowheight=50)
style.configure("mystyle.Treeview.Heading",font= ("Calibri",13,"bold"))
tv= ttk.Treeview(tree_Frame,columns=(1,2,3,4,5,6,7),style="mystyle.Treeview")
tv.heading("1",text="ID")
tv.column("1",width="40")
tv.heading("2",text="Name")
tv.column("2",width="140")
tv.heading("3",text="Job")
tv.column("3",width="50")
tv.heading("4",text="Gender")
tv.column("4",width="120")
tv.heading("5",text="Age")
tv.column("5",width="110")
tv.heading("6",text="Mobile")
tv.column("6",width="120")
tv.heading("7",text="Adress")
tv.column("7",width="190")
tv["show"]='headings'
tv.bind("<ButtonRelease-1>",getaData)
tv.place(x=1,y=1,height=610,width=900)
displayALL()
root.mainloop()




mysql 
import sqlite3
class Database:
    def __init__(self,db):
      self.con=sqlite3.connect(db)
      self.cur=self.con.cursor()

      sql = """
      CREATE TABLE IF NOT EXISTS employees(
        id Integer Primary Key,
        name text,
        job text,
        gender text,
        age text,
        mobile text,
        adress text
      )
      """
      self.cur.execute(sql)
      self.con.commit()
    def insert(self,name,job,gender,age,mobile,adress):
        self.cur.execute("insert into employees values (NULL,?,?,?,?,?,?)",
           (name,job,gender,age,mobile,adress) )
        self.con.commit()
    def fetch(self):
        self.cur.execute("SELECT * FROM employees ")
        rows = self.cur.fetchall()
        return rows
    def remove(self,id):
        self.cur.execute("delete from employees where id=?",(id,))
        self.con.commit()
    def update(self,id,name,job,gender,age,mobile,adress):
        self.cur.execute("update employees set name=?,job=?,gender=?,age=?,mobile=?,adress=? where id=?",
                        (name,job,gender,age,mobile,adress,id))
        self.con.commit()


