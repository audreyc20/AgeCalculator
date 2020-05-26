# AgeCalculator
Have you ever wondered how many days or months you have been alive or will be alive on a certain date? Use this calculator to find out.

    #imports
    import simplegui

    #set varriables
    userBDay = ""

    current_year = 0
    current_month = 0
    current_day = 0

    yearBorn = 0
    monthBorn = 0
    dayBorn = 0

    dayBorn2 = 0
    current_day2 = 0

    numYears = 0
    numMonths = 0
    numDays = 0

    #helper functions
    def slice_userBDay_string():							#functions that separates the year, month, and day the user was born
        global yearBorn, monthBorn, dayBorn, dayBorn2, current_day2
        #Slices the string of the userBDay to find the month day and year separatly
        yearBorn = userBDay[4:]
        yearBorn = int(yearBorn)

        monthBorn = userBDay[0:2]
        monthBorn = int(monthBorn)

        dayBorn = userBDay[2:4]
        dayBorn = int(dayBorn)

        dayBorn2 = ((monthBorn - 1) * 30) + dayBorn
        current_day2 =((current_month - 1) * 30) + current_day

    def yearsAlive():										#function that calculates the numbers of years alive
        global numYears
        if dayBorn2 < current_day:      					#in case they were born before the date we are calculating from
            numYears = (current_year - yearBorn) - ((dayBorn2 - current_day2)/365)
        else:
            numYears = (current_year - yearBorn) - ((monthBorn - (current_month+1))/12) - ((dayBorn2 - current_day2)/365)

    def monthsAlive():										#function that calculates the numbers of months alive
        global numMonths
        numMonths = numYears*12

    def daysAlive():										#function that calculates the number of days alive 
        global numDays
        numDays = numYears*365

    def display():											#function thatcalls the other functions and displays the information
        print ("you have been alive for:")		
        yearsAlive()
        print (str(numYears) + " years")
        monthsAlive()
        print ("or " + str(numMonths) + " months")
        daysAlive()
        print ("or " + str(numDays) + " days")

    #event handlers
    def draw(canvas):										 #draw handler
        canvas.draw_text("Welcome to Age Calculator!", (65,75), 50, "white")
        canvas.draw_text("Enter today's date, your birthday, and click calculate!", (125,120), 20, "#fcba03")

        canvas.draw_text(("Today's Year: " + str(current_year)), (25,200), 20, "#dec1e3")
        canvas.draw_text(("Today's Month: " + str(current_month)), (25,230), 20, "#dec1e3")
        canvas.draw_text(("Today's Day: " + str(current_day)), (25,260), 20, "#dec1e3")

        canvas.draw_text(("Birth Year: " + str(yearBorn)), (200,200), 20, "#dec1e3")
        canvas.draw_text(("Birth Month: " + str(monthBorn)), (200,230), 20, "#dec1e3")
        canvas.draw_text(("Birth Day: " + str(dayBorn)), (200,260), 20, "#dec1e3")

        canvas.draw_text(("Age in Years: " + str(numYears)), (375,200), 20, "#dec1e3")
        canvas.draw_text(("Age in Months: " + str(numMonths)), (375,230), 20, "#dec1e3")
        canvas.draw_text(("Age in Days: " + str(numDays)), (375,260), 20, "#dec1e3")

    def input_todays_year_handler(year):					 #event handler for todays year
        global current_year
        current_year = int(year)

    def input_todays_month_handler(month):					 #event handler for todays month
        global current_month
        current_month = int(month)

    def input_todays_day_handler(day):					 	 #event handler for todays day
        global current_day
        current_day = int(day)

    def input_userBDay_handler(birthday):					 #event handler for the users birthday
        global userBDay
        userBDay = birthday
        slice_userBDay_string()

    def button_calculate_handler():							#event handler for when the calculate button is clicked
        display()

    #create the frame
    frame = simplegui.create_frame('Age Calculator', 700, 300)

    #set and create the handlers
    frame.set_canvas_background("#7809b0")					 #sets the background color of the canvas
    frame.set_draw_handler(draw)							 #sets the draw handler
    frame.add_input("Today's Year (number)",input_todays_year_handler,170)
    frame.add_input("Today's Month (number)",input_todays_month_handler,170)
    frame.add_input("Today's Day (number)",input_todays_day_handler,170)
    frame.add_input("Your BDay (eg: 01012001)",input_userBDay_handler,170)
    frame.add_button ("Calculate", button_calculate_handler, 170)

    #start frame
    frame.start()
