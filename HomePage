from tkinter import *
import tkinter.font as font
import tkinter.messagebox as messagebox

import os
from os import path
import ast

import matplotlib.pyplot as plt

###################################################################################
#This class handles the validation of a user trying to login, and adds a new user to the file that contains existing users.
class LoginInfo:

    def __init__(self):
        self.loginData = ""
        self.loginDictionary = dict()
        
        
        if not str(path.isfile("Dictionary.txt")) or os.stat("Dictionary.txt").st_size == 0: #if file does not exist, create it. If it is empty, open it.
            with open("Dictionary.txt", "w") as f:
                f.truncate(0)
                
                    
        else: #file exists, so we update our dictionary with whatever is in the file
            with open("Dictionary.txt", "r") as infile:
                self.loginData = infile.read() #stores what is currently in the file
                print(self.loginData)
                    
            self.updateDict(self.loginData)
            
    def updateDict(self, loginData):
        self.loginDictionary = dict(ast.literal_eval(self.loginData))
        
    
    def updateFile(self, username, password):
    
        self.loginDictionary[username] = password #updates the dictionary
        #this updates the text file so that the next time we run our code, the dictionary will be correct
        with open("Dictionary.txt", "w") as outfile:
            outfile.write(str(self.loginDictionary))
        with open("Dictionary.txt", "r") as infile:
            for line in infile:
                print(line)
        for x, y in self.loginDictionary.items():
            print(x, y)
        
        
    def deleteContents(self):
        f = open('Dictionary.txt', 'r+')
        f.truncate(0)


###################################################################################

updateLogin = LoginInfo() #we first want to update the login information. We will create a login info object called "updateLogin"

class Controller(Frame):
    def __init__(self, master):
        Frame.__init__(self, master)
        
        #create user page
        self.userPage = UserPage(self)
        self.userPage.place(relwidth=1, relheight=1)
               
        #create welcome page
        self.welcomePage = WelcomePage(self)
        self.welcomePage.place(relwidth=1, relheight=1)
       
        self.welcomePage.tkraise() #show the welcome page first
        
        
        
###################################################################################


#the below class and its functions all deal with operations that occur on the welcome page
class WelcomePage(Frame):
    def __init__(self, master):
        Frame.__init__(self, master)
        self.createWidgets()
        self.configure(bg = "Aquamarine")
        

    def createWidgets(self):
        self.welcomeLabel = Label(self, text = "Welcome to Your\n Personal Fitness Tracker", bg = "Aquamarine", fg = "Aquamarine4")
        self.welcomeFont = font.Font(family = "Helvetica", size = 30, weight = "bold")
        self.welcomeLabel['font'] = self.welcomeFont
        self.welcomeLabel.pack(pady = "40")
    
        #create the login fields
        self.usernameLabel = Label(self, text = "Username:", bg = "Aquamarine", fg = "Aquamarine4").pack()
        self.usernameEntry = Entry(self, border = 0)
        self.usernameEntry.pack()
    
    
        self.passwordLabel = Label(self, text = "Password:", bg = "Aquamarine", fg = "Aquamarine4").pack()
        self.passwordEntry = Entry(self, show = '*', border = 0)
        self.passwordEntry.pack()
        self.passwordEntry.bind('<Return>', self.validateLogin)
        
        #creates checkbox for first login users
        self.newLoginButton = Checkbutton(self, text = "Create new login with this username and password?", bg = "Aquamarine", fg = "Aquamarine4")
        self.newLoginButton.pack(pady = "10")
        self.newLoginButton.bind('<Button-1>', self.appendDict)
        
        #creates Login button and calls the validateLogin function
        self.loginButton = Button(self, text = "Login")
        self.loginButton.pack()
        self.loginButton.bind('<Button-1>', self.validateLogin)
        
    #uses the dictionary to validate username and password
    def validateLogin(self, event):
        username = self.usernameEntry.get() #stores username
        password = self.passwordEntry.get() #stores password
    
        
        if username in updateLogin.loginDictionary and updateLogin.loginDictionary[username] == password: #validates key exists and its value mathes the password given
            print("Logging in...")
            self.createUserFile()
            self.destroy()
        
        else:
            messagebox.showinfo('Invalid Login Information', 'Username or Password Not Found')
    
    
    #appends a new username and password to the existing dictionary
    
    def appendDict(self, event):
        u = self.usernameEntry.get()
        p = self.passwordEntry.get()
        self.newLoginButton.deselect()
        
        if u in updateLogin.loginDictionary:
            messagebox.showinfo('Username Already Taken', 'Username is already taken. Pick a new one.')
            self.newLoginButton.deselect()
        elif u == "":
            messagebox.showinfo('Username Cannot Be Blank', 'Username cannot be nothing.')
            self.newLoginButton.deselect()
        elif p == "":
            messagebox.showinfo('Password Cannot Be Blank', 'Password cannot be nothing.')
            self.newLoginButton.deselect()
            
        else:
        
            updateLogin.updateFile(u, p)
    
    
    #each user will have a file associated with their profile. This function creates it.
    def createUserFile(self):
        u = self.usernameEntry.get()
        
        if not str(path.isfile(u + ".txt")):
            with open(u + ".txt", "x") as file: #x as a parameter makes this step fail if the file already exists
                file.write("This is your raw data. Please do not alter the contents of this file.\n")
                
            
            
 ###################################################################################
class UserPage(Frame):
    def __init__(self, master):
        Frame.__init__(self, master)
        #member functions
        self.createEntries()
        self.createRadios()
        self.createTotals()
        
        
    def createEntries(self):
        entriesFrame = Frame(self)
        entriesFrame.configure(bg = "blue")
        entriesFrame.place(anchor = 'nw')
        walkingLabel = Label(entriesFrame, text = "Enter Walking Mileage for the week:")
        walkingLabel.pack()
        walkingEntry = Entry(entriesFrame)
        walkingEntry.pack()
        
        runningLabel = Label(entriesFrame, text = "Enter Running Mileage for the week:")
        runningLabel.pack()
        runningEntry = Entry(entriesFrame)
        runningEntry.pack()
        
        bikingLabel = Label(entriesFrame, text = "Enter Biking Mileage for the week:")
        bikingLabel.pack()
        bikingEntry = Entry(entriesFrame)
        bikingEntry.pack()
        
        swimmingLabel = Label(entriesFrame, text = "Enter Swimming Mileage for the week:")
        swimmingLabel.pack()
        swimmingEntry = Entry(entriesFrame)
        swimmingEntry.pack()
        
    
    def createTotals(self):
        walkTotal = 16
        runTotal = 24
        bikeTotal = 38
        swimTotal = 3
        totalsFrame = Frame(self)
        totalsFrame.configure(bg = 'red')
        totalsFrame.place(relx = 0.5, rely = 0)
        wTotal = Label(totalsFrame, text = "Total Miles Walked: %d" % (walkTotal))
        wTotal.pack()
        
        rTotal = Label(totalsFrame, text = "Total Miles Ran: %d" % (runTotal))
        rTotal.pack()
        
        bTotal = Label(totalsFrame, text = "Total Miles Biked: %d" % (bikeTotal))
        bTotal.pack()
        
        sTotal = Label(totalsFrame, text = "Total Miles Swam: %d" % (swimTotal))
        sTotal.pack()

    
    
    
    def createRadios(self):
        v = IntVar()
        radio1 = Radiobutton(self, text = "Walking Progress", variable = v, value = 1, command = lambda : self.displayGraph(v))
        radio1.pack(side = LEFT)
        radio2 = Radiobutton(self, text = "Running Progress", variable = v, value = 2, command = lambda : self.displayGraph(v))
        radio2.pack(side = LEFT)
        radio3 = Radiobutton(self, text = "Biking Progress", variable = v, value = 3, command = lambda : self.displayGraph(v))
        radio3.pack(side = LEFT)
        radio4 = Radiobutton(self, text = "Swimming Progress", variable = v, value = 4, command = lambda : self.displayGraph(v))
        radio4.pack(side = LEFT)
        
    
    def displayGraph(self, v):
        if v.get() == 1:
            plt.plot([1, 2, 3, 4])
            plt.ylabel('some numbers')
            plt.show()
        elif v.get() == 2:
            print("2 works")
        elif v.get() == 3:
            print("3 works")
        elif v.get() == 4:
            print("4 works")
    
    
            
###################################################################################
#This function creates the file for each user and stores
#def getUserData:
    



    
        
        
 ###################################################################################

def main():
    root = Tk()
    root.title("Fitness Tracker")
    root.geometry('800x600')
    app = Controller(root)
    app.pack(expand = True, fill = BOTH)
    root.mainloop()

if __name__ == '__main__':
    main()
