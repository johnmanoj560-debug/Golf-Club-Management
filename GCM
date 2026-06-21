import mysql.connector
import customtkinter as ctk
from tkinter import messagebox

# Function to connect to the database
def connect_db():
    try:
        return mysql.connector.connect(
            host='localhost',
            user='root',
            passwd='password',
            database='golf_club_management'
        )
    except Exception as e:
        messagebox.showerror("Connection Error", str(e))
        return None

def exit_application():
    if mydb is not None and mydb.is_connected():  # Check if the database connection is valid
        mydb.close()  # Close the database connection
    app.quit()  # Terminate the application
    app.destroy()  # Close the application window

# Create main application window
app = ctk.CTk()
app.title("Golf Club Management System")
app.geometry("600x600")

# Global database connection
mydb = connect_db()

# Login Frame
login_frame = ctk.CTkFrame(app)
login_frame.pack(pady=20,padx=20)

ctk.CTkLabel(login_frame, text="ROYAL TEAM", font=("Felix Titling", 50,"bold"),text_color="#00ad4c").pack(pady=10)
ctk.CTkLabel(login_frame, text="Our Golf Club", font=("Eras Medium ITC", 27),text_color="#01A357").pack(pady=10)

ctk.CTkLabel(login_frame, text="Username:",font=("Gill Sans MT", 20)).pack(pady=5)
username_entry = ctk.CTkEntry(login_frame)
username_entry.pack(pady=5)

ctk.CTkLabel(login_frame, text="Password:",font=("Gill Sans MT", 20)).pack(pady=5)
password_entry = ctk.CTkEntry(login_frame, show="*")
password_entry.pack(pady=5)

def login():
    username = username_entry.get().title()
    password = password_entry.get()
    
    mycursor = mydb.cursor()
    mycursor.execute("SELECT * FROM membership_table WHERE Member_Name = %s", (username,))
    result = mycursor.fetchone()

    if username == "Boss" and password == "root@456":
        login_frame.pack_forget()  # Hide the login frame
        show_boss_frame()
    elif result and password == "root@123":
        login_frame.pack_forget()
        show_user_frame()
    else:
        messagebox.showerror("Login Failed", "Invalid username or password.")

login_button = ctk.CTkButton(login_frame, text="Login",font=("Kristen ITC", 15),fg_color="green", corner_radius=50, command=login)
login_button.pack(pady=20)

def create_membership():
    def submit():
        name = name_entry.get().title()
        membership_option = membership_combobox.get()
        
        # Prepare and execute SQL query
        query1="INSERT INTO membership_table VALUES(34,'%s','%s',0,0)"%(name,membership_option)
        query2="alter table membership_table drop Serial_no" # Reset the serial no.
        query3="alter table membership_table add Serial_no integer(10) not null auto_increment primary key"
        query4="alter table membership_table modify Serial_no integer(10) after Member_Name"
        query5="alter table membership_table modify Member_Name varchar(100) after Serial_no;"
        mycursor=mydb.cursor()
        mycursor.execute(query1)
        mycursor.execute(query2)
        mycursor.execute(query3)
        mycursor.execute(query4)
        mycursor.execute(query5)
        mydb.commit()

        status_label.configure(text='You have successfully created a membership. Password : root@123')

    # Create the dialog window
    def create_input_dialog():
        dialog = ctk.CTkToplevel()
        dialog.title("Membership Input")
        dialog.geometry("400x450")

        # Create and place widgets
        name_label = ctk.CTkLabel(dialog, text="Enter Name:",font=("Gill Sans MT", 20))
        name_label.pack(pady=10)
        global name_entry
        name_entry = ctk.CTkEntry(dialog)
        name_entry.pack(pady=5)

        global membership_var
        membership_var = ctk.StringVar()
        membership_label = ctk.CTkLabel(dialog, text="Select the option for Membership",font=("Gill Sans MT", 20))
        membership_label.pack(pady=10)

        global membership_combobox
        membership_combobox = ctk.CTkComboBox(dialog, 
        values=["Weekend Membership", "Standard Membership", "Premium Membership"],font=("Gill Sans MT", 15))
        membership_combobox.pack(pady=20,padx=20)

        submit_button = ctk.CTkButton(dialog, text="Create",font=("Kristen ITC", 15),fg_color="green",corner_radius=50, command=submit)
        submit_button.pack(pady=20)

        global status_label
        status_label = ctk.CTkLabel(dialog, text="")
        status_label.pack(pady=10)

    root = ctk.CTk()

    # Open the input dialog
    create_input_dialog()
        
create_membership_button = ctk.CTkButton(login_frame, text="Create Membership",font=("Kristen ITC", 15),fg_color="green", corner_radius=50, command=create_membership).pack(pady=5)
Exit=ctk.CTkButton(login_frame, text="Exit",font=("Kristen ITC", 15),fg_color="red", corner_radius=50, command=exit_application).pack(pady=20)

    # Main Frame
def show_boss_frame():
    boss_frame = ctk.CTkFrame(app)
    boss_frame.pack(pady=20)

    ctk.CTkLabel(boss_frame, text="Golf Club Management (Admin Frame)", font=("Tw Cen MT", 35),text_color="#00ad4c").pack(pady=10)

    # Buttons for each functionality
    ctk.CTkButton(boss_frame, text="Update Membership",font=("Kristen ITC", 15),fg_color="green", corner_radius=50, command=update_membership).pack(pady=10)
    ctk.CTkButton(boss_frame, text="Show Members",font=("Kristen ITC", 15),fg_color="green", corner_radius=50, command=show_members).pack(pady=10)
    ctk.CTkButton(boss_frame, text="Show Equipment",font=("Kristen ITC", 15),fg_color="green", corner_radius=50, command=show_equipment).pack(pady=10)
    ctk.CTkButton(boss_frame, text="Show Golf Courses",font=("Kristen ITC", 15),fg_color="green", corner_radius=50, command=show_golf_courses).pack(pady=10)
    ctk.CTkButton(boss_frame, text="Requests of updation of membership",font=("Kristen ITC", 15),fg_color="green", corner_radius=50, command=show_requests).pack(pady=10)
    ctk.CTkButton(boss_frame, text="Requests of Exciting the club",font=("Kristen ITC", 15),fg_color="green", corner_radius=50, command=show_requests_remove).pack(pady=10)
    ctk.CTkButton(boss_frame, text="Remove Membership",font=("Kristen ITC", 15),fg_color="green", corner_radius=50, command=remove_membership).pack(pady=10)
    ctk.CTkButton(boss_frame, text="Show Others' Reviews",font=("Kristen ITC", 15),fg_color="green", corner_radius=50, command=show_reviews).pack(pady=10)
    ctk.CTkButton(boss_frame, text="Exit",font=("Kristen ITC", 15),fg_color="red", corner_radius=50, command=exit_application).pack(pady=20)

def show_user_frame():
    user_frame = ctk.CTkFrame(app)
    user_frame.pack(pady=20)

    ctk.CTkLabel(user_frame, text="Golf Club Management (User Frame)", font=("Tw Cen MT", 35),text_color="#00ad4c").pack(pady=10)

    # Buttons for each functionality
    ctk.CTkButton(user_frame, text="Show Members",font=("Kristen ITC", 15),fg_color="green", corner_radius=50, command=show_members).pack(pady=10)
    ctk.CTkButton(user_frame, text="Show Equipment",font=("Kristen ITC", 15),fg_color="green", corner_radius=50, command=show_equipment).pack(pady=10)
    ctk.CTkButton(user_frame, text="Show Accessible Equipment",font=("Kristen ITC", 15),fg_color="green", corner_radius=50, command=show_accessible_equipment).pack(pady=10)
    ctk.CTkButton(user_frame, text="Show Golf Courses",font=("Kristen ITC", 15),fg_color="green", corner_radius=50, command=show_golf_courses).pack(pady=10)
    ctk.CTkButton(user_frame, text="Show Accessible Golf Courses",font=("Kristen ITC", 15),fg_color="green", corner_radius=50, command=show_accessible_golf_courses).pack(pady=10)
    ctk.CTkButton(user_frame, text="Request for Updation of Membership",font=("Kristen ITC", 15),fg_color="green", corner_radius=50, command=request_update).pack(pady=10)
    ctk.CTkButton(user_frame, text="Request for Exiting the Club Form",font=("Kristen ITC", 15),fg_color="green", corner_radius=50, command=request_remove).pack(pady=10)
    ctk.CTkButton(user_frame, text="Feedback",font=("Kristen ITC", 15),fg_color="green", corner_radius=50, command=give_feedback).pack(pady=10)
    ctk.CTkButton(user_frame, text="Exit",font=("Kristen ITC", 15),fg_color="red", corner_radius=50, command=exit_application).pack(pady=20)

# Membership Functions

def update_membership():
    def create_connection():
        return mysql.connector.connect(
            host="localhost",
            user="root",
            password="password",
            database="golf_club_management"
        )
            # Function to load member details based on serial number
    def load_member_details(event=None):
        serial_no = serial_no_entry.get()
        
        if not serial_no:
            result_label.config(text="Please enter a Serial No.", text_color="red")
            return

        # Connect to the database
        mydb = create_connection()
        mycursor = mydb.cursor()

        try:
            query = "SELECT Member_Name, Subscription_Type, Year_as_Member, Games_Played FROM membership_table WHERE Serial_no = %s"
            mycursor.execute(query, (serial_no,))
            result = mycursor.fetchone()

            if result:
                # Populate fields with existing data
                name_entry.delete(0, ctk.END)
                name_entry.insert(0, result[0])

                # Map subscription type to radio button selection
                subscription_type = result[1]
                subscription_map = {
                    'Weekend Membership': 1,
                    'Standard Membership': 2,
                    'Premium Membership': 3
                }
                subscription_var.set(subscription_map.get(subscription_type, 1))  # Default to Weekend if unknown

                years_entry.delete(0, ctk.END)
                years_entry.insert(0, result[2])

                games_entry.delete(0, ctk.END)
                games_entry.insert(0, result[3])

                result_label.configure(text="Member details loaded successfully.", text_color="green")
            else:
                result_label.configure(text="No member found with this Serial No.", text_color="red")
            
        except mysql.connector.Error as err:
            result_label.configure(text=f"Error: {err}", text_color="red")
        finally:
            mycursor.close()
            mydb.close()
        

    # Update membership function
    def update_membership():
        name = name_entry.get().title()
        subscription_type = subscription_var.get()
        years_as_member = years_entry.get()
        games_played = games_entry.get()
        serial_no = serial_no_entry.get()

        subscription_map = {
            1: 'Weekend Membership',
            2: 'Standard Membership',
            3: 'Premium Membership'
        }
        
        subscription = subscription_map.get(subscription_type, 'Unknown Membership')

        # Connect to the database
        mydb = create_connection()
        mycursor = mydb.cursor()

        try:
            queries = [
                "UPDATE membership_table SET Member_Name = %s WHERE Serial_no = %s",
                "UPDATE membership_table SET Subscription_Type = %s WHERE Serial_no = %s",
                "UPDATE membership_table SET Year_as_Member = %s WHERE Serial_no = %s",
                "UPDATE membership_table SET Games_Played = %s WHERE Serial_no = %s"
            ]
            
            mycursor.execute(queries[0], (name, serial_no))
            mycursor.execute(queries[1], (subscription, serial_no))
            mycursor.execute(queries[2], (years_as_member, serial_no))
            mycursor.execute(queries[3], (games_played, serial_no))

            mydb.commit()
            update_window.destroy()
        except mysql.connector.Error as err:
            result_label.configure(text=f"Error: {err}", text_color="red")
        finally:
            mycursor.close()
        update_window.destroy()
        

    # Set up the main application window
    update_window = ctk.CTkToplevel(app)
    update_window.title("Membership Update")
    update_window.geometry("400x450")

    # Create a scrollable frame
    scrollable_frame = ctk.CTkScrollableFrame(update_window)
    scrollable_frame.pack(fill="both", expand=True)

    # Create the input fields in the scrollable frame
    ctk.CTkLabel(scrollable_frame, text="Serial No:",font=("Gill Sans MT", 20)).pack(pady=5)
    serial_no_entry = ctk.CTkEntry(scrollable_frame)
    serial_no_entry.pack(pady=5)

    # Bind the event to load member details when Enter key is pressed
    serial_no_entry.bind("<Return>", load_member_details)

    ctk.CTkLabel(scrollable_frame, text="Enter Name:",font=("Gill Sans MT", 20)).pack(pady=5)
    name_entry = ctk.CTkEntry(scrollable_frame)
    name_entry.pack(pady=5)

    ctk.CTkLabel(scrollable_frame, text="Select Subscription Type:",font=("Gill Sans MT", 20)).pack(pady=5)
    subscription_var = ctk.IntVar(value=1)
    ctk.CTkRadioButton(scrollable_frame, text="Weekend Membership",font=("Kristen ITC", 15), variable=subscription_var, value=1).pack(pady=5)
    ctk.CTkRadioButton(scrollable_frame, text="Standard Membership",font=("Kristen ITC", 15), variable=subscription_var, value=2).pack(pady=5)
    ctk.CTkRadioButton(scrollable_frame, text="Premium Membership",font=("Kristen ITC", 15), variable=subscription_var, value=3).pack(pady=5)

    ctk.CTkLabel(scrollable_frame, text="Years as Member:",font=("Gill Sans MT", 20)).pack(pady=5)
    years_entry = ctk.CTkEntry(scrollable_frame)
    years_entry.pack(pady=5)

    ctk.CTkLabel(scrollable_frame, text="Games Played:",font=("Gill Sans MT", 20)).pack(pady=5)
    games_entry = ctk.CTkEntry(scrollable_frame)
    games_entry.pack(pady=5)

    # Create the Update button
    update_button = ctk.CTkButton(scrollable_frame, text="Update",font=("Kristen ITC", 15),fg_color="green", corner_radius=50, command=update_membership)
    update_button.pack(pady=20)

    # Result label
    result_label = ctk.CTkLabel(scrollable_frame, text="")
    result_label.pack(pady=5)

def show_members():
    # Show existing members in a new window
    members_window = ctk.CTkToplevel(app)
    members_window.title("Existing Members")
    members_window.geometry("800x600")

    # Create a scrollable frame for the table
    scrollable_frame = ctk.CTkScrollableFrame(members_window)
    scrollable_frame.pack(pady=10, padx=10, fill="both", expand=True)

    # Define column names
    columns = ["Serial_no", "Member_Name", "Subscription_Type", "Year_as_Member", "Games_Played"]

    def create_connection():
        return mysql.connector.connect(
            host="localhost",
            user="root",
            password="password",
            database="golf_club_management"
        )

    # Function to fetch and display data (in order to make changes to initial updations)
    def update_table():
        # Clear existing widgets in the scrollable frame
        for widget in scrollable_frame.winfo_children():
            widget.destroy()

        # Create a table header
        for col_index, col_name in enumerate(columns):
            label = ctk.CTkLabel(scrollable_frame, text=col_name, font=("Gill Sans MT", 16, "bold"))
            label.grid(row=0, column=col_index, padx=10, pady=5)

        try:
            mydb = create_connection()
            mycursor = mydb.cursor()
            query = "SELECT * FROM membership_table"
            mycursor.execute(query)
            mydata = mycursor.fetchall()

            # Populate the table with data
            for row_index, row in enumerate(mydata):
                for col_index, item in enumerate(row):
                    label = ctk.CTkLabel(scrollable_frame, text=item)
                    label.grid(row=row_index + 1, column=col_index, padx=10, pady=5)

        except mysql.connector.Error as err:
            error_label = ctk.CTkLabel(scrollable_frame, text=f"Database error: {str(err)}", text_color="red")
            error_label.grid(row=1, columnspan=len(columns), padx=10, pady=5)
        except Exception as e:
            error_label = ctk.CTkLabel(scrollable_frame, text=f"Error fetching data: {str(e)}", text_color="red")
            error_label.grid(row=1, columnspan=len(columns), padx=10, pady=5)
        finally:
            try:
                mycursor.close()
                mydb.close()
            except (NameError, AttributeError):
                pass

        # Schedule the next update
        members_window.after(60000, update_table)  # Refresh every 60 seconds

    # Initial data load
    update_table()

def show_equipment():
   #Show available equipments in a new window
    equipment_window = ctk.CTkToplevel(app)
    equipment_window.title("Equipments")
    equipment_window.geometry("600x600")

    # Create a scrollable frame for the table
    scrollable_frame = ctk.CTkScrollableFrame(equipment_window)
    scrollable_frame.pack(pady=10, padx=10, fill="both", expand=True)

    # Define column names
    columns = ["Sl.no", "Golf Items", "Minimum required subscription"]

    # Create a table header
    for col_index, col_name in enumerate(columns):
        label = ctk.CTkLabel(scrollable_frame, text=col_name, font=("Gill Sans MT", 20))
        label.grid(row=0, column=col_index, padx=10, pady=5)

    try:
        mycursor = mydb.cursor()
        query="select * from equipments_available"
        mycursor.execute(query)
        mydata = mycursor.fetchall()

        # Populate the table with data
        for row_index, row in enumerate(mydata):
            for col_index, item in enumerate(row):
                label = ctk.CTkLabel(scrollable_frame, text=item)
                label.grid(row=row_index + 1, column=col_index, padx=10, pady=5)
    except Exception as e:
        error_label = ctk.CTkLabel(scrollable_frame, text=f"Error fetching data: {str(e)}", text_color="red")
        error_label.grid(row=1, columnspan=len(columns), padx=10, pady=5)
    finally:
        mycursor.close()

def show_accessible_equipment():
    def get_accessible_equipments():
        member_name = member_name_entry.get().title()
        
        if not member_name: # Check if the member name is empty
            messagebox.showwarning("Input Error", "Please enter your name.")
            return
        
        members_window = ctk.CTkToplevel(app)
        members_window.title("Golf Equipments you could access")
        members_window.geometry("600x600")
        
        scrollable_frame = ctk.CTkScrollableFrame(members_window)
        scrollable_frame.pack(pady=10, padx=10, fill="both", expand=True)

        columns = ["Courses you could access"]
        for col_index, col_name in enumerate(columns):
            label = ctk.CTkLabel(scrollable_frame, text=col_name, font=("Gill Sans MT", 20))
            label.grid(row=0, column=col_index, padx=10, pady=5)
        
        mycursor = mydb.cursor()

        try:
            # Fetch subscription type of the member
            query = "SELECT Subscription_Type FROM membership_table WHERE Member_Name = %s"
            mycursor.execute(query, (member_name,))
            subscription_type = mycursor.fetchone()

            if subscription_type:
                subscription_type = subscription_type[0]

                # Define queries based on membership type
                if subscription_type == 'Standard Membership':
                    queries = [
                        "SELECT Golf_Items FROM equipments_available WHERE Subscription_Type = 'Standard Membership'",
                        "SELECT Golf_Items FROM equipments_available WHERE Subscription_Type = 'Weekend Membership'"
                    ]
                elif subscription_type == 'Premium Membership':
                    queries = [
                        "SELECT Golf_Items FROM equipments_available WHERE Subscription_Type = 'Premium Membership'",
                        "SELECT Golf_Items FROM equipments_available WHERE Subscription_Type = 'Standard Membership'",
                        "SELECT Golf_Items FROM equipments_available WHERE Subscription_Type = 'Weekend Membership'"
                    ]
                else:
                    queries = ["SELECT Golf_Items FROM equipments_available WHERE Subscription_Type = 'Weekend Membership'"]

                if queries:
                    row_index = 1   # Start from the second row for data
                    for query in queries:
                        mycursor.execute(query)
                        mydata = mycursor.fetchall()

                        for row in mydata:
                            for col_index, item in enumerate(row):
                                label = ctk.CTkLabel(scrollable_frame, text=item)
                                label.grid(row=row_index, column=col_index, padx=10, pady=5) # Place the label in the grid
                            row_index += 1 # Move to the next row
                else:
                    # If no queries were run, display a message indicating no accessible courses
                    error_label = ctk.CTkLabel(scrollable_frame, text="No accessible equipments found", text_color="red")
                    error_label.grid(row=1, columnspan=len(columns), padx=10, pady=5)
            else:
                error_label = ctk.CTkLabel(scrollable_frame, text="Member not found", text_color="red")
                error_label.grid(row=1, columnspan=len(columns), padx=10, pady=5)
        
        except Exception as e:
            error_label = ctk.CTkLabel(scrollable_frame, text=f"Error fetching data: {str(e)}", text_color="red")
            error_label.grid(row=1, columnspan=len(columns), padx=10, pady=5)
        
        finally:
            mycursor.close()

    access_window = ctk.CTkToplevel(app)
    access_window.title("Show Accessible Equipments")
    access_window.geometry("300x200")

    ctk.CTkLabel(access_window, text="Enter Your Name:", font=("Kristen ITC", 15)).pack(pady=5)
    member_name_entry = ctk.CTkEntry(access_window)
    member_name_entry.pack(pady=5)

    ctk.CTkButton(access_window, text="Show Accessible Equipments", font=("Gill Sans MT", 20), fg_color="green", corner_radius=50,command=get_accessible_equipments).pack(pady=20)

def show_golf_courses():
    #Show available golf courses in a new window
    members_window = ctk.CTkToplevel(app)
    members_window.title("Golf Courses")
    members_window.geometry("400x300")

    # Create a scrollable frame for the table
    scrollable_frame = ctk.CTkScrollableFrame(members_window)
    scrollable_frame.pack(pady=10, padx=10, fill="both", expand=True)

    # Define column names
    columns = ["Sl.no",  "Minimum required subscription","Courses"]

    # Create a table header
    for col_index, col_name in enumerate(columns):
        label = ctk.CTkLabel(scrollable_frame, text=col_name, font=("Gill Sans MT", 20))
        label.grid(row=0, column=col_index, padx=10, pady=5)

    try:
        mycursor = mydb.cursor()
        query="select * from available_golf_court"
        mycursor.execute(query)
        mydata = mycursor.fetchall()

        # Populate the table with data
        for row_index, row in enumerate(mydata):
            for col_index, item in enumerate(row):
                label = ctk.CTkLabel(scrollable_frame, text=item)
                label.grid(row=row_index + 1, column=col_index, padx=10, pady=5)
    except Exception as e:
        error_label = ctk.CTkLabel(scrollable_frame, text=f"Error fetching data: {str(e)}", text_color="red")
        error_label.grid(row=1, columnspan=len(columns), padx=10, pady=5)
    finally:
        mycursor.close()

def show_accessible_golf_courses():
    def get_accessible_courses():
        member_name = member_name_entry.get().title()
        
        if not member_name: # Check if the member name is empty
            messagebox.showwarning("Input Error", "Please enter your name.")
            return
        
        members_window = ctk.CTkToplevel(app)
        members_window.title("Golf Courses you could access")
        members_window.geometry("300x300")
        
        scrollable_frame = ctk.CTkScrollableFrame(members_window)
        scrollable_frame.pack(pady=10, padx=10, fill="both", expand=True)

        columns = ["Courses you could access"]
        for col_index, col_name in enumerate(columns):
            label = ctk.CTkLabel(scrollable_frame, text=col_name, font=("Gill Sans MT", 20))
            label.grid(row=0, column=col_index, padx=10, pady=5)
        
        mycursor = mydb.cursor()

        try:
            # Fetch subscription type of the member
            query = "SELECT Subscription_Type FROM membership_table WHERE Member_Name = %s"
            mycursor.execute(query, (member_name,))
            subscription_type = mycursor.fetchone()

            if subscription_type:
                subscription_type = subscription_type[0]

                # Define queries based on membership type
                if subscription_type == 'Standard Membership':
                    queries = [
                        "SELECT Court_Type FROM available_golf_court WHERE Subscription_Type = 'Standard Membership'",
                        "SELECT Court_Type FROM available_golf_court WHERE Subscription_Type = 'Weekend Membership'"
                    ]
                elif subscription_type == 'Premium Membership':
                    queries = [
                        "SELECT Court_Type FROM available_golf_court WHERE Subscription_Type = 'Premium Membership'",
                        "SELECT Court_Type FROM available_golf_court WHERE Subscription_Type = 'Standard Membership'",
                        "SELECT Court_Type FROM available_golf_court WHERE Subscription_Type = 'Weekend Membership'"
                    ]
                else:
                    queries = ["SELECT Court_Type FROM available_golf_court WHERE Subscription_Type = 'Weekend Membership'"]

                if queries:
                    row_index = 1   # Start from the second row for data
                    for query in queries:
                        mycursor.execute(query)
                        mydata = mycursor.fetchall()

                        for row in mydata:
                            for col_index, item in enumerate(row):
                                label = ctk.CTkLabel(scrollable_frame, text=item)
                                label.grid(row=row_index, column=col_index, padx=10, pady=5) # Place the label in the grid
                            row_index += 1 # Move to the next row
                else:
                    # If no queries were run, display a message indicating no accessible courses
                    error_label = ctk.CTkLabel(scrollable_frame, text="No accessible courses found", text_color="red")
                    error_label.grid(row=1, columnspan=len(columns), padx=10, pady=5)
            else:
                error_label = ctk.CTkLabel(scrollable_frame, text="Member not found", text_color="red")
                error_label.grid(row=1, columnspan=len(columns), padx=10, pady=5)
        
        except Exception as e:
            error_label = ctk.CTkLabel(scrollable_frame, text=f"Error fetching data: {str(e)}", text_color="red")
            error_label.grid(row=1, columnspan=len(columns), padx=10, pady=5)
        
        finally:
            mycursor.close()

    access_window = ctk.CTkToplevel(app)
    access_window.title("Show Accessible Golf Courses")

    ctk.CTkLabel(access_window, text="Enter Your Name:",font=("Gill Sans MT", 20)).pack(pady=5)
    member_name_entry = ctk.CTkEntry(access_window)
    member_name_entry.pack(pady=5)

    ctk.CTkButton(access_window, text="Show Accessible Courses", font=("Kristen ITC", 15), fg_color="green", corner_radius=50,
                  command=get_accessible_courses).pack(pady=20)



def remove_membership():
    def submit_removal():
        Serial_no = Serial_no_entry.get()
        mycursor = mydb.cursor()
        delete_query = "DELETE FROM membership_table WHERE Serial_no = '%s'"%(Serial_no,)
        mycursor.execute(delete_query)
        mydb.commit()
        query1="alter table membership_table drop Serial_no" # reset the serial no.
        query2="alter table membership_table add Serial_no integer(10) not null auto_increment primary key"
        query3="alter table membership_table modify Serial_no integer(10) after Member_Name"
        query4="alter table membership_table modify Member_Name varchar(100) after Serial_no"
        mycursor.execute(query1,query2,query3,query4)
        mydb.commit()
        messagebox.showinfo("Success", "Membership removed successfully.")
        remove_window.destroy()

    remove_window = ctk.CTkToplevel(app)
    remove_window.title("Remove Membership")
    remove_window.geometry("300x200")

    ctk.CTkLabel(remove_window, text="Enter Serial No:",font=("Gill Sans MT", 20)).pack(pady=5)
    Serial_no_entry = ctk.CTkEntry(remove_window)
    Serial_no_entry.pack(pady=5)

    ctk.CTkButton(remove_window, text="Remove",font=("Kristen ITC", 15),fg_color="red", corner_radius=50, command=submit_removal).pack(pady=20)

def give_feedback():
    def submit_feedback():
        name = name_entry.get()
        feedback = feedback_entry.get("1.0", ctk.END).strip()
        if name and feedback:
            with open('Feedback.txt', 'a') as file:
                file.write(name.title())
                file.write(':')
                file.write(feedback)
            messagebox.showinfo("Success", "Feedback submitted successfully!")
            name_entry.delete(0, ctk.END)
            feedback_entry.delete("1.0", ctk.END)
        else:
            messagebox.showwarning("Input Error", "Both name and feedback are required.")

    # Initialize the customtkinter application
    give_feedback = ctk.CTkToplevel()
    give_feedback.title("Feedback Form")
    give_feedback.geometry("400x300")  # Set the window size

    # Name entry
    ctk.CTkLabel(give_feedback, text="Enter Your Name:",font=("Gill Sans MT", 20)).pack(pady=10)
    name_entry = ctk.CTkEntry(give_feedback)
    name_entry.pack(pady=5, padx=20, fill='x')

    # Feedback entry
    ctk.CTkLabel(give_feedback, text="Enter Your Feedback:",font=("Gill Sans MT", 20)).pack(pady=10)
    feedback_entry = ctk.CTkTextbox(give_feedback, height=50)
    feedback_entry.pack(pady=5, padx=20, fill='x')

    # Submit button
    submit_button = ctk.CTkButton(give_feedback, text="Submit Feedback",font=("Kristen ITC", 15),fg_color="green", command=submit_feedback)
    submit_button.pack(pady=20)

def request_update():
    def submit_request():
        name = name_entry.get()
        request = request_entry.get("1.0", ctk.END).strip()
        if name and request:
            with open('Request.txt', 'a') as file:
                file.write(name.title())
                file.write(':')
                file.write(request)
            messagebox.showinfo("Success", "Request submitted successfully!")
            name_entry.delete(0, ctk.END)
            request_entry.delete("1.0", ctk.END)
        else:
            messagebox.showwarning("Input Error", "Both name and request are required.")

    # Initialize the customtkinter application
    request_update = ctk.CTkToplevel()
    request_update.title("Request for updation Form")
    request_update.geometry("400x300")  # Set the window size

    # Name entry
    ctk.CTkLabel(request_update, text="Enter Your Name:",font=("Gill Sans MT", 20)).pack(pady=10)
    name_entry = ctk.CTkEntry(request_update)
    name_entry.pack(pady=5, padx=20, fill='x')

    # Request entry
    ctk.CTkLabel(request_update, text="Enter Your details to be update:",font=("Gill Sans MT", 20)).pack(pady=10)
    request_entry = ctk.CTkTextbox(request_update, height=50)
    request_entry.pack(pady=5, padx=20, fill='x')

    # Submit button
    submit_button = ctk.CTkButton(request_update, text="Submit Request",font=("Kristen ITC", 15),fg_color="green", command=submit_request)
    submit_button.pack(pady=20)

def request_remove():
    def submit_request():
        name = name_entry.get()
        request = request_entry.get("1.0", ctk.END).strip()
        if name and request:
            with open('Request2.txt', 'a') as file:
                file.write(name.title())
                file.write(':')
                file.write(request)
            messagebox.showinfo("Success", "Request submitted successfully!")
            name_entry.delete(0, ctk.END)
            request_entry.delete("1.0", ctk.END)
        else:
            messagebox.showwarning("Input Error", "Both name and request are required.")

    # Initialize the customtkinter application
    request_update = ctk.CTkToplevel()
    request_update.title("Request for Exiting the Club Form")
    request_update.geometry("400x300")  # Set the window size

    # Name entry
    ctk.CTkLabel(request_update, text="Enter Your Name:",font=("Gill Sans MT", 20)).pack(pady=10)
    name_entry = ctk.CTkEntry(request_update)
    name_entry.pack(pady=5, padx=20, fill='x')

    # Request entry
    ctk.CTkLabel(request_update, text="Enter the reason for why you are leaving the club:",font=("Gill Sans MT", 20)).pack(pady=10)
    request_entry = ctk.CTkTextbox(request_update, height=50)
    request_entry.pack(pady=5, padx=20, fill='x')

    # Submit button
    submit_button = ctk.CTkButton(request_update, text="Submit Request",font=("Kristen ITC", 15),fg_color="green", command=submit_request)
    submit_button.pack(pady=20)

def show_reviews():
    # Create a new window
    review_window = ctk.CTkToplevel(app)
    review_window.title("Others' Reviews")

    # Create a CTkTextbox widget to display reviews
    text_box = ctk.CTkTextbox(review_window, wrap='word', width=500, height=300)
    text_box.pack(padx=20, pady=20)

    try:
        with open('Feedback.txt', 'r') as file:
            reviews = file.readlines()  # Read lines to enumerate them

        if reviews:  # Check if there are any reviews
            for index, review in enumerate(reviews, start=1):
                text_box.insert('end', f"Review {index}: {review}\n")
        else:
            text_box.insert('end', "No reviews available.")
    except FileNotFoundError:
        text_box.insert('end', "No reviews available.")
    except IOError as e:
        text_box.insert('end', f"An error occurred while reading the file: {e}")

def show_requests():
    # Create a new window
    request_window = ctk.CTkToplevel(app)
    request_window.title("Others' Request for Updation")

    # Create a CTkTextbox widget to display reviews
    text_box = ctk.CTkTextbox(request_window, wrap='word', width=500, height=300)
    text_box.pack(padx=20, pady=20)

    try:
        with open('Request.txt', 'r') as file:
            reviews = file.readlines()  # Read lines to enumerate them

        if reviews:  # Check if there are any reviews
            for index, review in enumerate(reviews, start=1):
                text_box.insert('end', f"Request {index}: {review}\n")
        else:
            text_box.insert('end', "No reviews available.")
    except FileNotFoundError:
        text_box.insert('end', "No reviews available.")
    except IOError as e:
        text_box.insert('end', f"An error occurred while reading the file: {e}")

def show_requests_remove():
    # Create a new window
    request_window = ctk.CTkToplevel(app)
    request_window.title("Others' Request for removal")

    # Create a CTkTextbox widget to display reviews
    text_box = ctk.CTkTextbox(request_window, wrap='word', width=500, height=300)
    text_box.pack(padx=20, pady=20)

    try:
        with open('Request2.txt', 'r') as file:
            reviews = file.readlines()  # Read lines to enumerate them

        if reviews:  # Check if there are any reviews
            for index, review in enumerate(reviews, start=1):
                text_box.insert('end', f"Request {index}: {review}\n")
        else:
            text_box.insert('end', "No reviews available.")
    except FileNotFoundError:
        text_box.insert('end', "No reviews available.")
    except IOError as e:
        text_box.insert('end', f"An error occurred while reading the file: {e}")
# Start the application
app.mainloop()
