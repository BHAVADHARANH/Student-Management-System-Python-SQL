# Student-Management-System-Python-SQL
Python-based student management system (CRUD) using SQL for efficient CRUD operations on student records.

=> INSTALLATION :
       Install WAMP SERVER from website and login to login page
       
=>CREATING DATABASE :

     To build a database in WampServer, which includes creating a new database, creating tables, and inserting data, you can follow these steps:

          *  Start WampServer: Start the WampServer application on your computer. You should see the WampServer icon in your system tray.
          *  Open phpMyAdmin: Click on the WampServer icon in the system tray and select "phpMyAdmin" from the menu. This will open the phpMyAdmin interface in your 
             web browser.
          *  Login to phpMyAdmin: If prompted, enter your MySQL username and password. By default, the username is "root" and there is no password (leave the password 
             field blank).
          * Create a new database: In the phpMyAdmin interface, click on the "Databases" tab and enter a name for your new database in the "Create database" field. 
             Click the "Create" button 
         * to create the database.
            Create tables: With your new database selected in the left-hand sidebar, click on the "SQL" tab. Here, you can enter SQL commands to create tables in your 
            database. For example, 
        
        to create a table for student records, you can use the following SQL command:
        _______________________________________________________________________________________________________________________________________________________________________
                                    CREATE TABLE students (
                                                       id INT AUTO_INCREMENT PRIMARY KEY,
                                                       name VARCHAR(255) NOT NULL,
                                                       address VARCHAR(255) NOT NULL,
                                                       contact VARCHAR(20) NOT NULL,
                                                       mail VARCHAR(20) NOT NULL
                                                       );
_______________________________________________________________________________________________________________________________________________________________________                                                 
       * Click the "Go" button to execute the SQL command and create the table.
       * Insert data: To insert data into your tables, click on the "Insert" tab. Enter the data for each column in the table and click the "Go" button to insert the 
         data.
       * Verify the database: You can verify that your database and tables have been created by clicking on the database name in the left-hand sidebar. You should see 
         your tables listed under the database name.
       * Use the database in your application: Once you have created your database and tables, you can use them in your application by connecting to the database using 
         the appropriate connection settings.
         
=> INTEGRATING SQL WITH PYTHON :

         * open pycharm ,select new project,give  project name(eg..,project.py)
         * Go settings -> python interpreter -> install ( mysql-python-connector)
         
=> CODING:
        # import mysql and tabular package :

                    import mysql.connector
                    from tabulate import tabulate
                    con = mysql.connector.connect(host="localhost", user="root", password="", database="registration") 

        # application of CRUDE operations:

                  #INSERT():
                         def insert():
                             name = input("Enter name:")
                             age = input("Enter age:")
                             address = input("Enter address:")
                             contact = input("Enter contact:")
                             mail = input("Enter mail:")

                        res = con.cursor()
                        sql = "insert into registration.data(name, age, address, contact, mail) values (%s, %s, %s, %s, %s)"
                        res.execute(sql, (name, age, address, contact, mail))
                        con.commit()
                        print("\n")
                        print("Record Insert Successfully")
                        
                  #SELECT():
                  
                             def select():
                                     res = con.cursor()
                                     sql = "SELECT * from data"
                                     res.execute(sql)
                                     result=res.fetchall()
                                     print("/n")
                                   print(tabulate(result,headers=["ID","NAME","AGE","ADDRESS","CONTACT","MAIL"]))
                #UPDATE():
                
                            def update():
                                   print("1. Name")
                                   print("2. Age")
                                   print("3. Address")
                                   print("4. Contact")
                                   print("5. Mail")
                         option = int(input("\nWhich field do you want to update?: "))
                         pid = input("Enter ID of the record you want to update: ")

                        if option == 1:
                                 new_name = input("Enter new name: ")
                                 sql = "UPDATE registration.data SET name = %s WHERE pid = %s"
                       elif option == 2:
                                 new_age = input("Enter new age: ")
                                 sql = "UPDATE registration.data SET age = %s WHERE pid = %s"
                      elif option == 3:
                                 new_address = input("Enter new address: ")
                                 sql = "UPDATE registration.data SET address = %s WHERE pid = %s"
                      elif option == 4:
                               new_contact = input("Enter new contact: ")
                               sql = "UPDATE registration.data SET contact = %s WHERE pid = %s"
                      elif option == 5:
                               new_mail = input("Enter new mail: ")
                               sql = "UPDATE registration.data SET mail = %s WHERE pid = %s"
                       else:
                                 print("Invalid option")
                                 return


                       cur = con.cursor()
                       cur.execute(sql, (new_name, pid) if option == 1 else
                             (new_age, pid) if option == 2 else
                             (new_address, pid) if option == 3 else
                            (new_contact, pid) if option == 4 else
                            (new_mail, pid))
                      con.commit()
                      select()
                          print("\nRecord Updated Successfully")
                          
                          
             #DELETE() :  
        
                          def delete():
                                  pid=input("Enter your ID:")
                                  res=con.cursor()
                                  sql="delete from data where pid=%s"
                                  res.execute(sql,(pid,))
                                  con.commit()
                                    print("\n")
                                    print("Record Deleted successfully...!!!")
                                    

             #CONDITION:                                   

                              while True:
                                      print("\n")
                                      print("1. Insert Record")
                                      print("2. Select Record")
                                      print("3. Update Record")
                                      print("4. Delete Record")
                                      print("5. Exit")
                                      print("\n")
                             choice = int(input("Enter your choice:"))
                             if choice == 1:
                                   insert()
                             elif choice == 2:
                                    select()
                             elif choice == 3:
                                   update()
                             elif choice == 4:
                                   delete()
                             elif choice == 5:
                                  print("Exiting...")
                                   break
                              else:
                                     print("Invalid Option...!!!")
                    

         



       
