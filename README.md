"""Author: Estela Garcia
Date written: 3/7/2025
Assignment: Module 8 Final Project Submission
Short Description: Tip Calculator named "Tippy".
 Helps you calculate the tip per individual with custom amounts
   as well as easy preset buttons of 15% and 18%. """
import tkinter as tk #Import tkinter library for GUI development
from tkinter import Toplevel #Import specific widgets and data types
from PIL import Image, ImageTk #Import Image and ImageTk for handling image display in tkinter
#App
# variable for user information
user_data = {
    "bill_amount": 0, #bill amount
    "custom_tip": 0, #Custom tip percentage
    "party_size": 0 #party size
}
#Function to open main window
main_window = tk.Tk()#create the main window
main_window.title("Tippy") # title
main_window.configure(bg='green') #background color for main window

#image for the first window
img1 = Image.open("C:/Users/egarc/OneDrive/Documents/tipjar.jpg").resize((150, 150), Image.LANCZOS) # first image
photo1 = ImageTk.PhotoImage(img1) #convert the image to a format suitable for tkinter
img_label1 = tk.Label(main_window, image=photo1) #create a label to display the image
img_label1.image = photo1 # keep a reference to avoid the image being garbage collected
img_label1.pack() #pack the image label into the main window

#Function to calculate custom tip
def custom_tip(entry_amount, entry_percentage, party_size, show_results): 
    bill = float(entry_amount.get())#conversion of bill entry to a float
    percentage = float(entry_percentage.get())#conversion of percentage entry to a float
    custom_tip = bill * (percentage / 100) #calculate custom tip based on percentage
    bill_amount = bill + custom_tip #calculate bill amount plus tip
    party_size =int(party_size.get()) # convert party size to an integer
    amount_per_person = bill_amount/party_size #calculation of what each person is to pay   
    show_results(main_window,custom_tip, bill_amount, amount_per_person) # will show results in result window

#Function to calculate preset 15%
def calculate_15_tip(entry_amount, party_size, show_results):
    bill = float(entry_amount.get()) #conversion of bill entry to a float
    percentage = 15 # preset tip of 15%
    custom_tip = bill * (percentage / 100) #calculate custom tip based on percentage
    bill_amount = bill + custom_tip  #calcuation of bill amount and tip
    party_size = int(party_size.get()) #convert party size to an integer
    amount_per_person = bill_amount/party_size #calculation of what each person is to pay 
    show_results(main_window,custom_tip, bill_amount, amount_per_person) # will show results in result window
#Function to calculate preset 18%
def calculate_18_tip(entry_amount, party_size, show_results):
    bill = float(entry_amount.get())#conversion of bill entry to a float
    percentage = 18 #preset tip of 18%
    custom_tip = bill * (percentage / 100) #calculation of custom tip based on percentage of 18%
    bill_amount = bill + custom_tip #calcuation of bill amount and tip
    party_size =int(party_size.get()) #convert the party size entry to an interger
    amount_per_person = bill_amount/party_size#calculation of what each person is to pay 
    show_results(main_window, custom_tip, bill_amount, amount_per_person)# will show results in result window

 # Function to open result window
def answer_window(tip, total, amount_per_person): #window creates result window with tip, total and amount per person cost.
    answer_window = tk.Toplevel(main_window) #create window result window
    answer_window.title("Calculation Results") #title for result window
    answer_window.geometry("300x300")      #size of result window
    answer_window.configure(bg='lightblue') #background for result window
      
    result_label = tk.Label(answer_window, text="Thank you for using Tippy the tip Calculator") #top label for result window
    result_label.pack()
    
    result_label = tk.Label(answer_window, text=f"Tip: ${tip:.2f}\nTotal: ${total:.2f}\nPer Person: ${amount_per_person:.2f}") #labels for result window
    result_label.pack()
    
    close_button = tk.Button(answer_window, text="Close", command=answer_window.destroy) #close button for result window
    close_button.pack()    

#image for result window
    img2 = Image.open("C:/Users/egarc/OneDrive/Documents/thank you.jpg").resize((150, 150), Image.LANCZOS) #image for result window
    photo2 = ImageTk.PhotoImage(img2) #convert the image to a format suitable for tkinter
    img_label2 = tk.Label(answer_window, image=photo2) #create a label to display the image
    img_label2.image = photo2 # keep a reference to avoid the image being garbage collected
    img_label2.pack() #pack the image label into the main window  


def show_results(window,tip,total, amount_per_person):
    answer_window(tip,total,amount_per_person) # call to function to display results
#results in result window
    result_label = tk.Label(answer_window, text=f"Tip: ${tip:.2f}\nTotal: ${total:.2f}")
    result_label.pack()

    close_button =tk.Button(answer_window, text="close", command=answer_window.destroy)
    close_button.pack()

#reset after a new attempt
def reset_fields():
    bill_entry.delete(0,tk.END) # clear the bill amount entry field
    custom_tip_entry.delete(0,tk.END) #clear the custom tip entry field
    party_size_entry.delete(0,tk.END) #clear the party size entry field

#UI elements
bill_label = tk.Label(main_window, text = "Enter Bill Amount:") #label for bill amount on main window
bill_label.pack()

bill_entry = tk.Entry(main_window) #entry box on main window for "Enter Bill Amount"
bill_entry.pack()

party_size_label =tk.Label(main_window, text ="Party Size:") #label for party size
party_size_label.pack()

party_size_entry =tk.Entry(main_window) #entry box for "party size" on main window
party_size_entry.pack()

custom_tip_label = tk.Label(main_window,text= "Enter Custom Tip Percentage:") #Label for custom tip percentage on main window
custom_tip_label.pack()

custom_tip_entry =tk.Entry(main_window) # entry box for custom tip entry on main window
custom_tip_entry.pack()

# Buttons for preset and custom tip
tip_15_button = tk.Button(main_window, text ="15% Tip", command=lambda: calculate_15_tip(bill_entry, party_size_entry, show_results)) #15% button
tip_15_button.pack()

tip_18_button = tk.Button(main_window, text ="18% Tip", command=lambda: calculate_18_tip(bill_entry, party_size_entry, show_results)) #18% button
tip_18_button.pack()

custom_tip_button =tk.Button(main_window, text="Calculate Custom Tip", command=lambda: custom_tip(bill_entry,custom_tip_entry, party_size_entry, show_results)) #custom tip button
custom_tip_button.pack()

#reset button
reset_button = tk.Button(main_window, text="clear", command=reset_fields) #clear button
reset_button.pack()

# run main window
main_window.mainloop() #Start the tkinter main event loop to keep the window open

