# .Effgithub
import random
import time
import os
def main():
    def valid_type_only(Number,Type_wanted):
        while True:
            try:
                Number = Type_wanted(Number)
                break
            except ValueError:
                time.sleep(0.5)
                Number = input('Wrong Type!, Try again: ')
        return Number
    op_lst = ['+','-','x','/']
    rand_chance = [True,False]
    difficulty = input('Choose difficulty:\n1) Easy\n2) Medium\n3) Hard\n4) Impossible\nEnter the corresponding number: ')
    difficulty = valid_type_only(difficulty,int)
    while difficulty > 4:
        time.sleep(0.5)
        difficulty = input('Out of index!, Try again: ')
        difficulty = valid_type_only(difficulty,int)
    lives = 5 - difficulty
    points = 0
    time.sleep(1) 
    print("If you would like to quit, type 'exit' in the answer box")
    time.sleep(0.5)
    print("However, your progress won't be saved!")
    time.sleep(0.5)
    print('Starting the Game now!')
    while lives > 0:
        max_num = '1' + '0' * difficulty
        num1 , num2 = random.randint(1,int(max_num)) , random.randint(1,int(max_num))
        if random.choice(rand_chance):
            num1 = '-' + str(num1)
            num1 = int(num1)
        if random.choice(rand_chance):
            num2 = '-' + str(num2)
            num2 = int(num2)
        rand_op = random.choice(op_lst)
        if rand_op != '/' or (rand_op == '/' and (num1 % num2) == 0):
            time.sleep(1)
            user_ans = input(f'What is {num1} {rand_op} {num2}? ')
            if user_ans == str(user_ans) and user_ans.lower() == 'exit':
                print('Thank you for playing the game!')
                time.sleep(0.5)
                print('Exiting the Game now ...')
                exit()
            else:
                if '-' in user_ans and user_ans.count('-') == 1:
                    user_ans = user_ans[1:]
                    user_ans = valid_type_only(user_ans,int)
                    user_ans = '-' + str(user_ans)
                    user_ans = int(user_ans)
                else:
                    user_ans = valid_type_only(user_ans,int)
        else:
            time.sleep(1)
            user_ans = input(f'What is {num1} {rand_op} {num2}? (to 1 d.p) ')
            if user_ans == str(user_ans) and user_ans.lower() == 'exit':
                print('Thank you for playing the game!')
                time.sleep(0.5)
                print('Exiting the Game now ...')
                exit()
            else:
                user_ans = valid_type_only(user_ans,float)
        if rand_op == '+':
            correct_ans = num1 + num2
        elif rand_op == '-':
            correct_ans = num1 - num2
        elif rand_op == 'x':
            correct_ans = num1 * num2
        else:
            correct_ans = num1 / num2
        if round(user_ans,1) == round(correct_ans,1):
            points += 1
            time.sleep(1)
            print(f'Correct!\nYou now have {points} points and {lives} lives')
        else:
            lives -= 1
            time.sleep(1)
            print(f'Incorrect!\nYou now have {points} points and {lives} lives')
def login_system():
    directory = r'\\CC-SRV-CGDC-FS3\CC_Student_HD\N_Gurung18\Documents\User_System'
    print("Welcome to Nischal's Game!")
    time.sleep(1)
    print('Would you like to login or register?')
    choice = input('Enter: ').lower()
    while choice not in ['register','login']:
        choice = input('Not an option!, Try again: ')
    if choice == 'register':
        user_name = input('Enter a username: ')
        while os.path.exists(f'{user_name}.txt'):
            user_name = input('Username already exists!, Try again: ')
        password = input('Enter a password: ')
        while len(password) < 8:
            password = input('Password is too short!, Try again: ')
        re_password = input('Enter your password again: ')
        while re_password != password:
            re_password = input('Password does not match!, Try again: ')
        unique_pin = random.randint(10000000,99999999)
        every_user_pin = []
        for i in os.listdir(directory):
            if not(i.endswith('.py')):
                file = open(i,'r')
                read_pin = file.readlines()[2][5:]
                every_user_pin.append(read_pin)
        while str(unique_pin) in every_user_pin:
            unique_pin = random.randint(10000000,99999999)
        print('This is your unique PIN number')
        time.sleep(1)
        print('Please do not share the PIN with anyone else')
        time.sleep(1)
        print(f'{unique_pin}')
        time.sleep(1)
        saved_pin = input('Press Enter once you have copied the PIN: ')
        file = open(f'{user_name}.txt', 'w')
        file.write(f'Username: {user_name}')
        file.write('\n')
        file.write(f'Password: {password}')
        file.write('\n')
        file.write(f'Pin: {unique_pin}')
        file.close()
    else:
        user_name = input('Enter username: ') + '.txt'
        while not(user_name in os.listdir(directory)):
            time.sleep(0.5)
            user_name = input('Username not found!, Try again: ')
        for i in os.listdir(directory):
            if not(i.endswith('.py')):
                if i == user_name:
                    file = open(user_name , 'r')
                    read_password = file.readlines()[1][10:]
                    file.close()
                    print("If you have forgotten your password, type 'forgot' into the answer box")
                    time.sleep(0.5)
                    password = input('Enter your password: ')
                    attempts = 0
                    pass_flag  = True
                    while password != read_password and pass_flag:
                        if password.lower() == 'forgot':
                            pass_flag = False
                        else:
                            password = input(f'Attempt: {attempts}, Wrong Password!, Try again: ')
                            attempts += 1
                            if attempts == 3:
                                attempts = 0
                                print('Too many failed attempts in a row')
                                print('Timing out for 30 seconds')
                                time.sleep(30)
                    if password.lower() == 'forgot':
                        time.sleep(0.5)
                        print('Since you have forgotten your password, we will now ask you to enter your PIN')
                        file = open(user_name , 'r')
                        read_pin = file.readlines()[2][5:]
                        file.close()
                        input_pin = input('Enter your pin: ')
                        while input_pin != read_pin:
                            input_pin = input(f'Attempt: {attempts}, Wrong PIN!, Try again: ')
                            attempts += 1
                            if attempts == 3:
                                attempts = 0
                                print('Too many failed attempts in a row')
                                time.sleep(1)
                                print('Timing out for 30 seconds')
                                time.sleep(30)
                        new_password = input('Enter a new password: ')
                        while len(new_password) < 8:
                            new_password = input('Password is too short!, Try again: ')
                        new_re_password = input('Enter your new password again: ')
                        while new_re_password != new_password:
                            new_re_password = input('Password does not match!, Try again: ')
                        file = open(user_name , 'r')
                        read_file = file.readlines()
                        read_username = read_file[0][10:].strip()
                        read_pin = read_file[2][5:]
                        file.close()
                        os.remove(user_name)
                        file = open(user_name,'w')
                        file.write(read_username)
                        file.write('\n')
                        file.write(new_password)
                        file.write('\n')
                        file.write(read_pin)
                    
login_system()



