# Stage_2_HackBio_internship
link of our Wep Application :  https://labcalchub.shinyapps.io/new_folder/


# **Authors** 
(@slack):Amira Mahmoud Mohamed (amira\\mahmoud\\4463)

Manar Tarek (ManarTj)

Noran Morad (NoranMorad)

Omar holayell sawy ( Holayell)



#Loads the Shiny package which is needed to create interactive web apps in R
library(shiny)   
#The UI part of the code defines how your app will look and what elements (like buttons, inputs, and outputs).
ui <- fluidPage(
  # Add custom CSS
  #Adds custom styles to change the appearance of the app. it sets the background color and font.
  tags$head(
    tags$style(HTML("
      body {
        background-color: #ffffff; 
        color: #000000;
        font-family: 'Arial', sans-serif;
      }
      .title-panel {
        font-family: 'Arial', sans-serif;
        text-align: center;
        color: #ffffff; 
        background-color: #003366; /* Dark Blue */
        padding: 20px;
        border-radius: 8px;
        box-shadow: 0 4px 8px rgba(0, 0, 0, 0.5);
        display: flex;
        align-items: center;
        justify-content: center;
        gap: 20px;
      }
      .title-panel img {
        width: 80px; /* Adjust the size of the image */
        height: auto;
      }
      .well {
        background-color: #f0f0f0;
        padding: 20px;
        border-radius: 8px;
        box-shadow: 0 4px 8px rgba(0, 0, 0, 0.5);
      }
      .main-panel {
        background-color: #f9f9f9;
        padding: 20px;
        border-radius: 8px;
        box-shadow: 0 4px 8px rgba(0, 0, 0, 0.5);
      }
      h3, h4 {
        color: #003366; /* Dark Blue */
        font-family: 'Arial', sans-serif;
      }
      h3 {
        font-size: 28px;
        font-weight: bold;
      }
      h4 {
        font-size: 24px;
        font-weight: bold;
      }
      .btn-primary {
        background-color: #003366; /* Dark Blue */
        border-color: #003366;
        color: #ffffff;
        font-weight: bold;
        border-radius: 4px;
      }
      .btn-primary:hover {
        background-color: #002244; /* Slightly Darker Blue */
        border-color: #002244;
      }
      .shiny-output-error {
        color: #ff4d4d;
        font-weight: bold;
      }
      .about-panel {
        background-color: #f0f0f0;
        padding: 20px;
        border-radius: 8px;
        margin-top: 20px;
        box-shadow: 0 4px 8px rgba(0, 0, 0, 0.5);
      }
      .sidebar-column {
        padding: 20px;
        background-color: #f9f9f9;
        border-radius: 8px;
        box-shadow: 0 4px 8px rgba(0, 0, 0, 0.5);
      }
      .tab-panel-title {
        font-size: 36px;
        font-weight: bold;
        text-align: center;
        color: #003366; /* Dark Blue */
        margin-bottom: 20px;
      }
    "))
  ),
  
  # Title panel
  #Creates a header section with an image (logo) and a title for the app.
  div(
    class = "title-panel",
    img(src = "calc.png", alt = "Laboratory Calculator"),  # Ensure the image file name and path are correct
    titlePanel("LabCalc Hub")
  ),
  
  # Main layout with tabs for Home, About, and Contact Us
  tabsetPanel(
    id = "tabs",
    tabPanel("Home",
             div(
               class = "tab-panel-title",
               "Home"
             ),
             fluidRow(
               column(width = 6, # Half width for each row
                      div(
                        class = "sidebar-column",
                        # Serial Dilution Inputs
                        h3("Serial Dilution Calculator"),
                        textInput("stock_name", "Stock Solution Name"),
                        textInput("diluent_name", "Diluent Name"),
                        numericInput("C0", "Initial Concentration (C₀)", value = 10, step = 0.1),
                        numericInput("Cfinal", "Desired Final Concentration (Cₓ)", value = 1, step = 0.1),
                        numericInput("dilution_factor", "Dilution Factor (DF)", value = 10),
                        numericInput("total_volume", "Total Volume (Vₓ, mL)", value = 100),
                        numericInput("num_dilutions", "Number of Dilutions", value = 1),
                        numericInput("num_replicates", "Number of Replicates (optional)", value = 1),
                        actionButton("calculate_serial", "Calculate Serial Dilution", class = "btn-primary"),
                        
                        # How to Use This Calculator
                        h4("How to Use This Calculator"),
                        p("1. Enter the stock solution name and diluent name."),
                        p("2. Input the initial concentration, desired final concentration, dilution factor, and total volume."),
                        p("3. Enter the number of dilutions and optionally the number of replicates."),
                        p("4. Click 'Calculate Serial Dilution' to see the results."),
                        p("Formula: Vₜ = (C₀ * Vₓ) / (Cₓ * DF)")
                      ),
                      div(
                        class = "main-panel",
                        # Serial Dilution Result
                        h4("Serial Dilution Result"),
                        tableOutput("serial_table")
                      )
               ),
               column(width = 6, # Half width for each row
                      div(
                        class = "sidebar-column",
                        # Stock Solution Dilution Inputs
                        h3("Stock Solution Dilution Calculator"),
                        numericInput("Cstock", "Stock Concentration (Cₛ)", value = 100, step = 0.1),
                        numericInput("Cdesired", "Desired Final Concentration (Cₓ)", value = 10, step = 0.1),
                        numericInput("final_volume", "Final Total Volume (Vₓ, mL)", value = 100),
                        actionButton("calculate_stock", "Calculate Stock Dilution", class = "btn-primary"),
                        
                        # How to Use This Calculator
                        h4("How to Use This Calculator"),
                        p("1. Enter the stock concentration, desired final concentration, and final total volume."),
                        p("2. Click 'Calculate Stock Dilution' to see the results."),
                        p("Formula: Vₛ = (Cₓ * Vₓ) / Cₛ and Vsolvent = Vₓ - Vₛ")
                      ),
                      div(
                        class = "main-panel",
                        # Stock Solution Dilution Result
                        h4("Stock Solution Dilution Result"),
                        tableOutput("stock_table")
                      )
               ),
               column(width = 6, # Half width for each row
                      div(
                        class = "sidebar-column",
                        # Molarity Calculator Inputs
                        h3("Molarity Calculator"),
                        numericInput("mass", "Mass of Solute (g)", value = 10, step = 0.1),
                        numericInput("molar_mass", "Molar Mass of Solute (g/mol)", value = 180, step = 1),
                        numericInput("solution_volume", "Volume of Solution (L)", value = 1, step = 0.1),
                        actionButton("calculate_molarity", "Calculate Molarity", class = "btn-primary"),
                        
                        # How to Use This Calculator
                        h4("How to Use This Calculator"),
                        p("1. Enter the mass of solute, molar mass of solute, and volume of solution."),
                        p("2. Click 'Calculate Molarity' to see the results."),
                        p("Formula: M = mass / (molar_mass * volume)")
                      ),
                      div(
                        class = "main-panel",
                        # Molarity Result
                        h4("Molarity Result"),
                        tableOutput("molarity_table")
                      )
               ),
               column(width = 6, # Half width for each row
                      div(
                        class = "sidebar-column",
                        # Density Calculator Inputs
                        h3("Solution Density Calculator"),
                        numericInput("mass_solution", "Mass of Solution (g)", value = 100),
                        numericInput("volume_solution", "Volume of Solution (mL)", value = 100),
                        actionButton("calculate_density", "Calculate Density", class = "btn-primary"),
                        
                        # How to Use This Calculator
                        h4("How to Use This Calculator"),
                        p("1. Enter the mass of the solution and volume of the solution."),
                        p("2. Click 'Calculate Density' to see the results."),
                        p("Formula: density = mass_solution / volume_solution")
                      ),
                      div(
                        class = "main-panel",
                        # Density Result
                        h4("Density Result"),
                        tableOutput("density_table")
                      )
               )
             )
    ),
    tabPanel("About",
             div(
               class = "tab-panel-title",
               "About"
             ),
             div(
               class = "about-panel",
               h3("About This App"),
               p("This application provides various tools for laboratory calculations, including Serial Dilution, Stock Solution Dilution, Molarity, and Solution Density calculations."),
               h4("Serial Dilution Calculator"),
               p("Calculates the volume to transfer at each step for serial dilution based on initial and final concentrations, dilution factor, and total volume."),
               h4("Stock Solution Dilution Calculator"),
               p("Determines the volume of stock solution and diluent required to achieve a desired final concentration."),
               h4("Molarity Calculator"),
               p("Calculates the molarity of a solution based on the mass of solute, its molar mass, and the volume of the solution."),
               h4("Solution Density Calculator"),
               p("Computes the density of a solution using its mass and volume.")
             )
    ),
    tabPanel("Contact Us",
             div(
               class = "tab-panel-title",
               "Contact Us"
             ),
             div(
               class = "about-panel",
               h3("Contact Us"),
               p("You can reach us at the following email addresses:"),
               tags$ul(
                 tags$li(tags$a(href = "mailto:amiraamahmoud133@gmail.com", "amiraamahmoud133@gmail.com")),
                 tags$li(tags$a(href = "mailto:manar.tarekj@gmail.com", "manar.tarekj@gmail.com")),
                 tags$li(tags$a(href = "mailto:noran.abdallah@ejust.edu.eg", "noran.abdallah@ejust.edu.eg")),
                 tags$li(tags$a(href = "mailto:omarhelil00@gmail.com", "omarhelil00@gmail.com"))
               )
             )
    )
  )
)
#The server part of the code defines how the app will handle user inputs and generate outputs.Defines how the app works (calculations, updates)
server <- function(input, output, session) {
  # Serial Dilution Calculation
  #Executes code when the "Calculate Serial Dilution" button is pressed.
  observeEvent(input$calculate_serial, {
    #Ensures all required inputs are provided before doing calculations.
    req(input$C0, input$Cfinal, input$dilution_factor, input$total_volume, input$num_dilutions)
    #Create a data frame to display the results
    df <- data.frame(
      Step = 1:input$num_dilutions,
      Volume_Stock = numeric(input$num_dilutions),
      Volume_Diluent = numeric(input$num_dilutions),
      stringsAsFactors = FALSE
    )
    
    C0 <- input$C0               #Initial concentration of the stock solution
    Cfinal <- input$Cfinal       #Desired final concentration
    DF <- input$dilution_factor  #how many times the solution is diluted
    Vx <- input$total_volume     #total volume of the solution after dilution
    
    #Calculates the volume of stock solution and diluent needed for each step of the dilution process.
    for (i in 1:input$num_dilutions) {
      df$Volume_Stock[i] <- (C0 * Vx) / (Cfinal * DF)
      df$Volume_Diluent[i] <- Vx - df$Volume_Stock[i]
      C0 <- C0 / DF            #Update the concentration of the stock solution for the next step by reducing by the dilution factor 
    }  
     
    
    #Displays the results in a table on the UI.
    output$serial_table <- renderTable({
      df
    })
  })
  
  # Stock Solution Dilution Calculation
  observeEvent(input$calculate_stock, {
    req(input$Cstock,         #Cs=Concentration of the stock solution
        input$Cdesired,       #Cx=Desired final concentration
        input$final_volume)   #Vx=Final total volume
    
    Vstock <- (input$Cdesired * input$final_volume) / input$Cstock #Calculate the volume of the stock solution needed
    Vsolvent <- input$final_volume - Vstock                        #Calculate the volume of solvent required
    #Create a data frame to display the results
    df <- data.frame(
      Volume_Stock = Vstock,
      Volume_Solvent = Vsolvent,
      stringsAsFactors = FALSE
    )
    
    output$stock_table <- renderTable({
      df
    })
  })
  
  observeEvent(input$calculate_molarity, {
    req(input$mass,            #Mass of the solute (in grams)
        input$molar_mass,      #Molar mass of the solute (in grams per mole)
        input$solution_volume) #Volume of the solution (in liters)
 #Calculate the molarity
    Molarity <- input$mass / (input$molar_mass * input$solution_volume)
 #Create a data frame to display the result
    df <- data.frame(
      Molarity = Molarity,
      stringsAsFactors = FALSE
    )
    
    output$molarity_table <- renderTable({
      df
    })
  })
  
  # Density Calculation

  observeEvent(input$calculate_density, {
    req(input$mass_solution,     #Mass of the solution (in grams)
        input$volume_solution)   #Volume of the solution (in milliliters)
  #Calculate the density
    Density <- input$mass_solution / input$volume_solution
  #Create a data frame to display the result
    df <- data.frame(
      Density = Density,
      stringsAsFactors = FALSE
    )
    
    output$density_table <- renderTable({
      df
    })
  })
}

#Combines the UI and server components and starts the Shiny app.
shinyApp(ui = ui, server = server)





      
