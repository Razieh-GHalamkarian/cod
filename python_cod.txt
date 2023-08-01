from tkinter import *
from tkinter import filedialog
import pandas
root = Tk()
#Menu
my_menu=Menu(root)
root.config(menu=my_menu)

def New_fram():
    scrollable_frame_m= ctk.CTkScrollableFrame(root, width=400, height=200)
    r=scrollable_frame_m.pack(pady=40)
    return r

def colour():
    rang=root.configure(bg='red')
    return rang

file_menu=Menu(my_menu)
my_menu.add_cascade(label='edit',menu=file_menu)
file_menu.add_command(label='New',command=New_fram)
file_menu.add_command(label='colour',command=colour)
#******************************************************************************
#open file
def openf():
    global data
    file = filedialog.askopenfilename(initialdir='/', title="select file", filetypes=(("Csv Files",".csv"), ("All Files","*.*")))
    data = pandas.read_csv(file)
    o=teditor.insert(END, data)
    return  data

#frame
#teditor = Text(root, width=4, height=2)
#teditor.pack(pady=10)

file_open = Button(root, text="Open file", command= openf)
file_open.pack()

root.geometry("350x200")
root.title("PythonLobby.com")


#%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
#graph
import customtkinter as ctk
import pandas
import matplotlib.pyplot as plt
import seaborn as sns
from tkinter import *
from tkinter import ttk



def Histogram():

    data_c=combox.get()
    x=data[data_c]
    plt.hist(x,bins=15,ec='blue')
    plt.ylabel('days')
    plt.xlabel('New_deaths')
    p=plt.show()
    return p


def Bar():


    data_c1 =combox.get()
    data_c2 =combo2.get()
    bar_chart = sns.barplot(x=data[data_c1], y=data[data_c2], data=data, order=None, linewidth=0.1, color='black',palette='Blues', saturation=0)
    bar_chart.set_xlabel('Date_reported')
    bar_chart.set_ylabel('New_deaths')
    bar_chart.set_title('crona')
    o = plt.show()
    return o

title_lable=ctk.CTkLabel(root,text='data analysis',font=ctk.CTkFont(size=20,weight='bold'))
title_lable.pack(padx=100,pady=(10,20))


scrollable_frame=ctk.CTkScrollableFrame(root,width=200,height=2)
scrollable_frame.pack()

graph_lable=ctk.CTkLabel(scrollable_frame,text='graph',font=ctk.CTkFont(size=20,weight='bold'))
graph_lable.pack()



combox=ttk.Combobox(scrollable_frame, values=('Date_reported','New_deaths'))
combox.pack()


combo2= ttk.Combobox(scrollable_frame, values=('Date_reported', 'New_deaths'))
combo2.pack()


#entry_c1=ctk.CTkEntry(scrollable_frame,placeholder_text=('enter your column'))
#entry_c1.pack(fill='x')


#entry_c2=ctk.CTkEntry(scrollable_frame,placeholder_text=('enter your column'))
#entry_c2.pack(fill='x')

H_button=ctk.CTkButton(scrollable_frame,text='Histogram',width=500,command=Histogram)
H_button.pack(pady=10)

Bar_button=ctk.CTkButton(scrollable_frame,text='Bar Chart',width=500,command=Bar)
Bar_button.pack(pady=10)

########################################################################################
#central tendency
def mean():

    data_c3 = combo_death.get()
    myangin = data[data_c3].mean()
    title_lable = ctk.CTkLabel(scrollable_frame2, text=myangin, font=ctk.CTkFont(size=20, weight='bold'))
    y = title_lable.pack(padx=10, pady=(20, 20))
    return y


def median():

    data_c3=combo_death.get()
    myane=data[data_c3].median()
    title_lable = ctk.CTkLabel(scrollable_frame2, text=myane, font=ctk.CTkFont(size=20, weight='bold'))
    b= title_lable.pack(padx=10, pady=(20, 20))
    return b

scrollable_frame2=ctk.CTkScrollableFrame(root,width=200,height=2)
scrollable_frame2.pack(pady=4)

cetral_lable=ctk.CTkLabel(scrollable_frame2,text='Central Tendency',font=ctk.CTkFont(size=20,weight='bold'))
cetral_lable.pack()

#entry_c3 = ctk.CTkEntry(scrollable_frame2, placeholder_text=('enter your column'))
#entry_c3.pack()

#entry_c4= ctk.CTkEntry(scrollable_frame2, placeholder_text=('enter your column'))
#entry_c4.pack()


combo_death=ttk.Combobox(scrollable_frame2, values=('Date_reported','New_deaths'))
combo_death.pack()

#comboy=ttk.Combobox(scrollable_frame2, values=('Date_reported','New_deaths'))
#combo.pack()




mean_button=ctk.CTkButton(scrollable_frame2,text='mean',width=500,command=mean)
mean_button.pack(pady=10)

median_button=ctk.CTkButton(scrollable_frame2,text='median',width=500,command=median)
median_button.pack(pady=10)


root.mainloop()