# set up UI
from tkinter import *
window=Tk()
window.config(padx=20,pady=20,bg="green")
window.title("pomodoro_project")
window.minsize(600,600)
text=Label(text="TIMER",font=("arial",40,"bold"),fg="blue")
text.place(x=250,y=40)
text.config(bg="yellow")
iv=PhotoImage(file="tomato.png")
imagec=Canvas(height=280,width=300,bg="green",highlightthickness=0)
imagec.create_image(140,150,image=iv)
countm=0
counts=0
global i
# j represent number of time worked
global j 
j=0
i=8
counter=imagec.create_text(140,160,text=f"{countm}:{counts}",font=("arial",40,"bold"))
imagec.place(x=180,y=100)
# setting time machine
work=Label(text="",font=("arial",20,"bold"),bg="green")
work.place(x=280,y=420)
def workt(countmw=24,countsw=60):
    global i
    if i>0:
        if countmw >= 0:
            if countsw > 0:
                work.config(text="work")
                imagec.itemconfig(counter, text=f"{countmw}:{countsw}")


                window.after(1000, workt, countmw, countsw - 1)
            else:
                window.after(1000, workt, countmw - 1)
        else:
            i = i - 1
            countdown(i)
# method for reset button 
def rese():
    checkmark.config(text="")
    work.config(text="CLICK START")
    imagec.itemconfig(counter, text=f"{countm}:{counts}")
    global i
    i=-1
def breakt(countmb=4, countsb=60):
    global i
    if i>0:
        checkmark.config(text="✅"*j)
        work.config(text="break")
        if countmb >= 0:

            if countsb > 0:

                imagec.itemconfig(counter, text=f"{countmb}:{countsb}")



                window.after(1000, breakt, countmb, countsb - 1)
            else:
                window.after(1000, breakt, countmb - 1)
        else:
            i = i - 1
            countdown(i)

# main function
def countdown(i=8):
    global j

    if i%2==0:
        workt()
    elif i==1:
        j = j + 1
        breakt(countmb=19)
        rese()
    elif i>0:
        j = j + 1
        breakt()

    else:

        imagec.itemconfig(counter, text=f"{countm}:{counts}")
        rese()

def cd():
    global i
    i=8
    countdown()

checkmark = Label(text="", font=("arial", 20, "bold"), fg="black", bg="green")
checkmark.place(x=250, y=500)
start=Button(text="start",fg="black",bg="yellow",font=("arial",20,"bold"),command=cd)
start.place(x=150,y=500)
reset=Button(text="reset",fg="black",bg="yellow",font=("arial",20,"bold"),command=rese)
reset.place(x=420,y=500)
window.mainloop()
