from tkinter import *
import string
window = Tk()
window.geometry('700x500')
text_present = False
def has_special_chars(word):
    for i in word:
        if i in string.punctuation:
            return True
    else:
        return False
def remove_text(windowname , time , variable=type(Message)):
    def remove():
        variable['text'] = ''
    windowname.after(time, remove)

def checker():
    global text_present
    username = entry1.get()
    pass_flag = True
    counter = 0
    for i in username:
        if i in string.digits:
            counter += 1
    if len(username) < 3 or len(username) > 20:
        pass_flag = False
        if text_present:
            invalid_message['text'] = 'Username must be between 3-20 chars long'
        else:
            invalid_message = Message(text = 'Username must be between 3-20 chars long' , font = 24 , foreground = 'red' , width = 350)
            invalid_message.pack()
            text_present = invalid_message
    elif has_special_chars(username) and pass_flag:
        pass_flag = False
        if text_present:
            invalid_message['text'] = 'Username must not contain special chars'
        else:
            invalid_message = Message(text = 'Username must not contain special chars' , font = 24 , foreground = 'red' , width = 350)
            invalid_message.pack()
            text_present = invalid_message
    elif counter == len(username):
        pass_flag = False
        if text_present:
            invalid_message['text'] = 'Username may contain sensitive information'
        else:
            invalid_message = Message(text = 'Username may contain sensitive information' , font = 24 , foreground = 'red' , width = 350)
            invalid_message.pack()
            text_present = invalid_message
    if not(pass_flag):
        remove_text(window , 1500 , invalid_message)
    if pass_flag:
        window.destroy()
        def pass_checker():
            global text_present
            password = entry2.get()
            re_password = entry3.get()
            if password != re_password:
                if text_present:
                    message['text'] = 'Passwords are not matching'
                else:
                    message = Message(text = 'Passwords are not matching' , font = 24 , foreground = 'red' , width = 350)
                    message.pack()
                    text_present = message
                remove_text(window , 1500 , invalid_message)
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



debuggging



from tkinter import *
import string
window = Tk()
window.geometry('700x500')
text_present = False
def has_special_chars(word):
    for i in word:
        if i in string.punctuation:
            return True
    else:
        return False
def place_error_label(window_name):
    error_label = Label(window_name , text = 'Nothing')
    error_label.pack()
    return error_label
def confirm():
    global text_present
    username = username_box.get()
    def checker(username):
        pass_flag = True
        error_string = False
        counter = 0 
        for i in username:
            if i in string.digits:
                counter += 1
        if len(username) < 3 or len(username) > 20:
            pass_flag = False
            error_string = 'Username must be between 3-20 chars long'
        elif has_special_chars(username) and pass_flag:
            pass_flag = False
            error_string = 'Username must not contain special chars'
        elif counter == len(username):
            pass_flag = False
            error_string = 'Username may contain sensitive information'
        return pass_flag , error_string
    pass_flag , error_string = checker(username)
    if pass_flag == False and error_string:
        if not(text_present):
            error_label['text'] = f'{error_string}'
            error_label.pack()
            text_present = True
        else:
            error_label['text'] = f'{error_string}'
    else:
        window.destroy()
register_label = Label(text = 'Register system' , font = 24)
register_label.pack()
username_label = Label(text = 'Username:' , font = 24)
username_label.pack()
username_box = Entry()
username_box.pack()
confirm_button = Button(text = 'Confirm' , font = 24 , command = confirm)
confirm_button.pack()
window.mainloop()
