**Documentation of the underlying mathematics formulas and logic used to implement LabCalcHub in R Shiny**

 **Serial Dilution Calculator**         
 Uses a loop to calculate the volume of stock solution, diluent and updating the concentration at each step.  
 **Mathematical Formula:**  
The formula to determine the volume of stock solution to transfer: 𝑉𝑡𝑟𝑎𝑛𝑠𝑓𝑒𝑟=𝐶0×𝑉𝑥𝐶𝑥×𝐷𝐹  
 **Logic in R Shiny:**  
![][image1]
Co <- input$co

#Initial concentration of the stock solution

Cfinal <- input$Cfinal

#Desired final concentration

DF <- input$dilution_factor #

how many times the solution is diluted

Vx <- input$total_volume

#total volume of the solution after dilution

#Calculates the volume of stock solution and diluent needed for each step of the dilution process.

for (i in 1:input$num_dilutions) {

df$Volume_Stock[i] <- (CO * Vx) / (Cfinal * DF) df$Volume_Diluent[i] <- Vx df$Volume_Stock[i]

CO <- CO / DF

#Update the concentration of the stock solution for the next step by reducing by the dilution factor

}

#Create a data frame to display the results

df <- data.frame(

Step = 1: input$num_dilutions,

Volume_Stock = numeric(input$num_dilutions),

Volume_Diluent = numeric(input$num_dilutions),

stringsAsFactors = FALSE
)



**. Stock Solution Dilution Calculator**  
 Calculates the volumes of stock solution and solvent required to achieve the desired final concentration.  
 **Mathematical Formulas:**  
The formula to determine the Volume of Stock Solution Needed: 𝑉𝑠=𝐶𝑥×𝑉𝑥𝐶𝑠  
The formula to determine the Volume of Solvent Needed:  
Vsolvent=Vx−Vs  
 **Logic in R Shiny:**  
![][image2]
# Stock Solution Dilution Calculation

observeEvent(input$calculate_stock,

req(input$Cstock,

#Cs=Concentration of the stock solution

input$Cdesired,

#Cx=Desired final concentration

input$final_volume)

#Vx=Final total volume

Vstock <- (input$Cdesired * input$final_volume) / input$Cstock #Calculate the volume of the stock solution needed

Vsolvent <- input$final_volume - Vstock

#Calculate the volume of solvent required

)

#Create a data frame to display the results

df <- data.frame(

Volume_Stock = Vstock,

Volume_Solvent = Vsolvent,

stringsAsFactors = FALSE



**. Molarity Calculator**  
 Calculates the concentration of a solution based on the mass of solute and the solution’s volume.  
 **Mathematical Formula:**  
The formula to calculate molarity (M) of a solution: 𝑀=𝑚𝑎𝑠𝑠𝐶𝑚𝑜𝑙𝑎𝑟 𝑚𝑎𝑠𝑠×𝑣𝑜𝑙𝑢𝑚𝑒𝑠  
 **Logic in R Shiny:**  
![][image3] 
observeEvent(input$calculate_molarity, {

req(input$mass,

#Mass of the solute (in grams)

input$molar_mass,

#Molar mass of the solute (in grams per mole)

input$solution_volume)

#Volume of the solution (in liters)

#Calculate the molarity

Molarity <- input$mass / (input$molar_mass * input$solution_volume)

#Create a data frame to display the result

df <- data.frame(

Molarity = Molarity,

stringsAsFactors = FALSE
)
**. Density Calculator**  
 Calculates the density of a solution based on its mass and volume.  
 **Mathematical Formula:**  
The formula to calculate the density (ρ) of a solution: 𝜌=𝑚𝑎𝑠𝑠(𝑠𝑜𝑙𝑢𝑡𝑖𝑜𝑛)𝑣𝑜𝑙𝑢𝑚𝑒(𝑠𝑜𝑙𝑢𝑡𝑖𝑜𝑛)  
**Logic in R Shiny:**

**![][image4]** observeEvent(input$calculate_density, {

req(input$mass_solution,

#Mass of the solution (in grams)

input volume_solution)

#Volume of the solution (in milliliters)

#Calculate the density

Density <- input$mass_solution / input$volume_solution

#Create a data frame to display the result

df <- data.frame(

Density = Density,

stringsAsFactors = FALSE

)

