from tkinter import *
import string
window = Tk()
window.geometry('700x500')
message = False
def has_special_chars(word):
    for i in word:
        if i in string.punctuation:
            return True
    else:
        return False
def checker():
    global message
    username = entry1.get()
    pass_flag = True
    counter = 0
    for i in username:
        if i in string.digits:
            counter += 1
    if len(username) < 3 or len(username) > 20:
        pass_flag = False
        if message:
            message['text'] = 'Username must be between 3-20 chars long'
        else:
            message = Message(text = 'Username must be between 3-20 chars long' , font = 24 , foreground = 'red' , width = 350)
            message.pack()
    elif has_special_chars(username) and pass_flag:
        pass_flag = False
        if message:
            message['text'] = 'Username must not contain special chars'
        else:
            message = Message(text = 'Username must not contain special chars' , font = 24 , foreground = 'red' , width = 350)
            message.pack()
    elif counter == len(username):
        pass_flag = False
        if message:
            message['text'] = 'Username may contain sensitive information'
        else:
            message = Message(text = 'Username may contain sensitive information' , font = 24 , foreground = 'red' , width = 350)
            message.pack()
    if pass_flag:
        window.destroy()
        def pass_checker():
            global message
            password = entry2.get()
            re_password = entry3.get()
            if password != re_password:
                if message:
                    message['text'] = 'Passwords are not matching'
                else:
                    message = Message(text = 'Passwords are not matching' , font = 24 , foreground = 'red' , width = 350)
                    message.pack()
            else:
                root.destroy()
        root = Tk()
        root.geometry('700x500')
        label = Label(text = 'Password:' , font = 24)
        label.pack()
        entry2 = Entry()
        entry2.pack()
        label = Label(text = 'Confirm Password:' , font = 24)
        label.pack()
        entry3 = Entry()
        entry3.pack()
        button = Button(text = 'Enter' , font = 24 , width = 10 , command = pass_checker)
        button.pack(pady = 10)
        root.mainloop()
label = Label(text = 'Welcome!' , font = 24)
label.pack()
label = Label(text = 'Username:', font = 24)
label.pack()
entry1 = Entry()
entry1.pack()
button = Button(text = 'Enter' , font = 24 , width = 10 , command = checker)
button.pack(pady = 10)
window.mainloop()
