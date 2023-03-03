# Pizza-ordering-System
Pizza Ordering System Code
//Name:		 - Ankit Singh- 2020B0123006
//Program:		Project two - Pizza
//Module:		CSC1021 - Programming I
//Description:	This class models a pizza and has calculations for finding its costs and total costs.

import java.util.ArrayList;

public class Pizza
{																				
	private ArrayList<PizzaTopping> tops = new ArrayList<PizzaTopping>();		//Initializing Array list for storing PizzaToppings.
	private PizzaBase base;								//Initializing the base using parameters declared in the PizzaBase class constructor..
	private int bInput;								//Initializing selection variable for PizzaChoice method.
	private int tInput;								//Initializing selection variable for PizzaChoice method.
	private int pIn;								//Initializing selection variable for PizzaMenu method.
	
	
	public Pizza()									//Initializing Constructor for the pizza object.
	{										//There is no main method in this class.
		this.setPizzaBase(base);						//Calls set method for base.
		this.tops = new ArrayList<PizzaTopping>();				//toppings in this method = t throughout this class.
	}

	public void setPizzaBase(PizzaBase base)					//Set method for pizza base.
	{
		this.base = base;							//base in this method = base used throughout this class.
	}

	public void addTopping(PizzaTopping topping)					//Method for adding toping to the pizza topping list.
	{
		tops.add(topping);
	}
	
	public double pizzaCost()							//Method for finding the cost of the pizza.
	{
		double cost = base.getCost();						//Declares cost and calls get cost method for the pizza base.
		for(PizzaTopping topping : tops)					//For loop for each element in the pizza toping array list.
		{
			cost += topping.getCost();					//Toping cost getter that adds onto the cost variable.
		}
		return cost;								//returns the cost of the pizza.
	}
	
	public void total()								//Method for order summary.
	{

		boolean Tveg = false;
		
		String newLine = System.getProperty("line.separator");			//Initialize "newLine" to enter a newline when entered in a system.out statement.
		System.out.print("\t---------------------------------" + newLine);	//Prints top border.
		System.out.format("\t%15s%21s", "-Ingredients-",  "-Price- "+ newLine);		//Prints header for the table.
		System.out.print("\t---------------------------------" + newLine);	//Prints border.
		System.out.printf("\t%-15s:%15s", base.getName(), base.getCost());	//Print the pizza Base.
		for(PizzaTopping topping : tops)					//for loop for every pizza topping.
		{
			System.out.printf(newLine + "\t%-15s:%15s", topping.getName(), topping.getCost());	//Prints every pizza topping and its price.
			if(topping.getVeg() == true)					//If topping is vegetarian set Tveg to true for if loop later.
			{
				Tveg = true;
			}
		}

		if(base.getVeg() == true || Tveg == true)				//If base or any topping is not vegetarian, print statement.
		{
			System.out.println("\n\n\tNot suitable for vegetarians");
		}
		else if(base.getVeg() == false && Tveg == false)			//If both base and all toppings are false, print statement.
		{
			System.out.println("\n\n\tSuitable for vegetarians");
		}
		
		System.out.printf(newLine + "\t%-15s:%15s","Total Cost", pizzaCost());		//displays total pizza dcost.
		System.out.print(newLine + "\t---------------------------------" + newLine);	//Prints border.
	}
	
	//******************************Get and set methods for other pizzaChoice and pizzaMenu class selections******************************//

    public int getbInput()							//Get base input method for the PizzaChoice class.
    {
    	return bInput;
    }	
	public void setbInput(int bInput)					//Set base input method for the pizzaChoice class.
    {	
    	this.bInput = bInput;      	
    }
    
    public int gettInput()							//Get topping input method for the pizzaChoice class.
    {
    	return tInput;
    }	
	public void settInput(int tInput)					//Get topping input method for the pizzaChoice class.
    {	
    	this.tInput = tInput;      	
    }
	
    public int getpIn()														
    {
    	return pIn;
    }	
	public void setpIn(int pIn)												
    {	
    	this.pIn = pIn;      	
    }

}
PizzaBase.java
//Name:		Ankit Singh - 2020B0123006
//Program:		Project two - PizzaBase
//Module:		CSC1021 - Programming I
//Description:	This class models a pizza base and topping.

public class PizzaBase 
{
	private String Name;				//Declare cost name.
	private double Cost;				//Declare base cost.
	private boolean vegetarian;			//Declare vegetarian boolean.
	
							//No main method
	
	public PizzaBase()				//Constructor for pizza base.
	{
		setName(Name);				//Sets object's name using a setter method.
		setCost(Cost);				//Sets object's cost using a setter method.
		setVeg(vegetarian);			//Sets object's boolean for vegetarian using a setter method.
	}
	
	public String getName()				//Base name getter method.
	{
		return Name;
	}
	
	public void setName(String Name)		//Base name setter method.
	{
		this.Name = Name;			//Base name in this method = Base name throughout this class.
	}
	
	public double getCost()				//Base cost getter method.
	{
		return Cost;				//Base cost in this method = Base cost throughout this class.
	}
	
	public void setCost(double Cost)		//Base cost setter method.
	{
		this.Cost = Cost;
	}
	
	public boolean getVeg()				//Vegetarian boolean getter method.
	{
		return vegetarian;	//Vegetarian boolean in this method = Vegetarian boolean throughout this class.
	}
	
	public void setVeg(boolean vegetarian)		//Vegetarian boolean setter method.
	{
		this.vegetarian = vegetarian;
	}

}
PizzaBuild.java
//Name:		Ankit Singh - 2020B0123006
//Program:		Project two - PizzaBuild
//Module:		CSC1021 - Programming I
//Description:	A pizza build program that will build a predefined pizza to demonstrate
//				the Pizza, PizzaTopping and PizzaBase classes.

public class PizzaBuild 
{

	public static void main(String[] args) 						//Main method.
	{
		Pizza pizza = new Pizza();						//New pizza object.
		pizza.setPizzaBase(new PizzaTopping("thin", 2.50, false));		//Creates and adds base object to the pizza object.
		pizza.addTopping(new PizzaTopping("Tomato Sauce", 0.50, false));	//Creates and adds topping object to the pizza object.		
		pizza.addTopping(new PizzaTopping("Cheese", 0.50, false));		//Creates and adds topping object to the pizza object.
		pizza.addTopping(new PizzaTopping("Ham", 1.25, true));			//Creates and adds topping object to the pizza object.
		pizza.addTopping(new PizzaTopping("Pineapple", 1.25, false));		//Creates and adds topping object to the pizza object.
		pizza.total();								//Calls the total method for the pizza object.
		
	}

}
PizzaChoice.java
//Name:		Ankit Singh - 2020B0123006
//Program:		Project two - PizzaChoice
//Module:		CSC1021 - Programming I
//Description:	A class that will show the user a menu of bases and toppings modeled on previous classes
//				and takes the user selection. It will then build a pizza modeled according to the pizza class
//				and call the method "pizza.total" to show a summary and the total cost of the pizza.

import java.util.ArrayList;
import java.util.Scanner;

public class PizzaChoice
{
	private static ArrayList<PizzaBase> bases = new ArrayList<PizzaBase>();		//Array List for the pizza base menu.
	private static ArrayList<PizzaTopping> tops = new ArrayList<PizzaTopping>();	//Array List for the pizza topping menu.
	private static Scanner keyboard;						//Initialize scanner for user input.
	private static int bInput;							//Integer for user base selection.
	private static int tInput;							//Integer for user topping selection.
	
	public static void addBase(PizzaBase base)					//Method for adding bases to the base menu.
	{
		bases.add(base);
	}
	
	public static void addTop(PizzaTopping topping)					//Method for adding toppings to the topping menu.
	{
		tops.add(topping);
	}
		
	public static void main(String[] args) 						//Main method.
	{
		
		Pizza pizza = new Pizza();						//Creates new pizza object according to the pizza class.
		//************Adds pizza bases to the base menu************//
		addBase(new PizzaTopping("Thin",2.50,false));
		addBase(new PizzaTopping("Thick",3.00,false));
		addBase(new PizzaTopping("Stuffed crust", 4.50,false));
		
		baseMenu(pizza);							//Calls the bases menu.
		
		try
		{
		baseChoice(pizza);							//Tries the baseChoice method.
		}		
        catch(IllegalArgumentException iae)						//Catches error thrown by the baseChoice method.
		{
        		System.out.println("Invalid selection, please select again");	//Shows user error method.
        		baseChoice(pizza);						//Continues baseChoice method.
		}
		
		//************Adds pizza toppings to topping menu************//
		//**************************Sauces**************************//
		addTop(new PizzaTopping("Tomato Sauce",0.50, false));
		addTop(new PizzaTopping("BBQ Sauce", 0.50, false));
		//**************************Cheese**************************//
		addTop(new PizzaTopping("Cheese", 0.50, false));
		//**************************Meats**************************//
		addTop(new PizzaTopping("Ham", 1.25, true));
		addTop(new PizzaTopping("Pepperoni", 1.50, true));
		addTop(new PizzaTopping("Bacon", 2.00, true));
		addTop(new PizzaTopping("Chicken", 1.75, true));
		addTop(new PizzaTopping("Ground Beef", 1.50, true));
		//**************************Veg**************************//
		addTop(new PizzaTopping("Mushrooms", 0.75, false));
		addTop(new PizzaTopping("Onions", 0.75, false));
		addTop(new PizzaTopping("Peppers", 1.00, false));
		addTop(new PizzaTopping("Pineapple", 1.25, false));
		addTop(new PizzaTopping("Sweetcorn", 0.50, false));
		
		toppingMenu(pizza);							//Calls the topping menu method.
		try
		{
		toppingChoice(pizza);							//Tries the toppingChoice method.
		}
        catch(IllegalArgumentException iae)						//Catches the error thrown by toppingChoice method.
		{		
        		System.out.println("Invalid selection, please select again");	//Shows user error message.
        		toppingChoice(pizza);						//Continues toppingChoice method.
		}
		pizza.total();								//Calls total method that shows summary of pizza bases, toppings and price.
	}
	
	public static void baseMenu(Pizza pizza)					//Method for printing table of pizza bases (printing array list).
	{
		int i = 1;								//Int i for labelling bases for user.
		keyboard = new Scanner(System.in);					//Declaring keyboard as scanner, else null pointer exception will occur.
		
		System.out.println("Pizza base selection");											
		String newLine = System.getProperty("line.separator");			//Initialize "newLine" to enter a newline when entered in a system.out statement.
		System.out.print("\t------------------------------------" + newLine);	//Prints top border.
		System.out.format("\t%15s%21s", "-Bases-",  "-Price- "+ newLine);	//Prints header for the table.
		System.out.print("\t------------------------------------" + newLine);	//Prints border.
		
		for(PizzaBase base : bases)									//for loop for every pizza base in bases menu.
		{
			System.out.printf(newLine + "\t%5s. %-15s:%10s", i, base.getName(), base.getCost());	//Prints every pizza base and its price.
			i++;											//Adds 1 to i for base labeling.
		}
		
		System.out.print(newLine + "\t------------------------------------" + newLine);			//Prints border.
	}
	
	public static void baseChoice(Pizza pizza)								//Method for choosing the base.
	{	
		System.out.println("Please enter your choice of base by entering its respective number.");	//System out message for user.
		bInput = keyboard.nextInt();									//Uses user input as bInput.

		if(bInput<1||bInput>3)										//If statement for if the input is not valid.
		{
			throw new IllegalArgumentException("\nMust enter a number between 1 and 3.\nPlease run again.");	//Throws exception.
		}
		else if(bInput == 1)										//Else if loop for setting the pizza base.
		{
			pizza.setPizzaBase(new PizzaTopping("Thin", 2.50, false));				//Creates new pizza base and sets it for pizza.
			System.out.println("You've selected 'Thin'.\n");					//Confirmation message for user.
		}
		else if(bInput == 2)
		{
			pizza.setPizzaBase(new PizzaTopping("Thick", 3, false));				//Creates new pizza base and sets it for pizza.
			System.out.println("You've selected 'Thick'.\n");					//Confirmation message for user.
		}
		else if(bInput == 3)
		{
			pizza.setPizzaBase(new PizzaTopping("Stuffed", 4.50, false));				//Creates new pizza base and sets it for pizza.
			System.out.println("You've selected 'Stuffed crust'.\n");				//Confirmation message for user.
		}
		pizza.setbInput(bInput);									//Sets bInput .		
	}
	
	public static void toppingMenu(Pizza pizza)								//Method for printing table of pizza toppings (printing array list).
	{
		int i = 1;											//Int i for labelling bases for user.
		
		System.out.println("Pizza topping selection");
		String newLine = System.getProperty("line.separator");						//Initialize "newLine" to enter a newline when entered in a system.out statement.
		System.out.print("\t------------------------------------" + newLine);				//Prints top border.
		System.out.format("\t%15s%21s", "-Toppings-",  "-Price- "+ newLine);				//Prints header for the table.
		System.out.print("\t------------------------------------" + newLine);				//Prints border.
		
		for(PizzaTopping topping : tops)								//for loop for every pizza topping.
		{
			System.out.printf(newLine + "\t%5s. %-15s:%10s", i, topping.getName(), topping.getCost());	//Prints every pizza topping and its price.
			i++;											//Adds 1 to i for base labeling.
		}
		
		System.out.print(newLine + "\t------------------------------------" + newLine);			//Prints border.
	}
	
	public static void toppingChoice(Pizza pizza)								//Method for topping selection.
	{	
		System.out.println("Please select your toppings by entering their respective numbers."		//Print out statement for user.
					+ "\nEnter 0 at any time to end the selection.\n");	
		do												//Do while loop for while tInput does not equal 0.
		{
			tInput = keyboard.nextInt();								//Takes user input as tInput.
			pizza.settInput(tInput);								//Sets tInput.
		if(tInput<-1||tInput>13)									//If tInput is outside of selection throws error message.
		{
			throw new IllegalArgumentException("\nMust enter a number between 0 and 13.\nPlease run again.");
		}	
		else if(tInput == 0)										//Else if statement for topping selection.
		{
			System.out.println("End of topping selection.");					//If 0 is entered, break.
			break;
		}
		else if(tInput == 1)										//Topping selections.
		{
			pizza.addTopping(new PizzaTopping("Tomato Sauce", .50, false));				//Creates new topping and adds to pizza.
			System.out.println("You've selected 'Tomato Sauce'.");					//Confirmation message.
		}
		else if(tInput == 2)
		{
			pizza.addTopping(new PizzaTopping("BBQ", .50, false));
			System.out.println("You've selected 'BBQ Sauce'.");
		}
		else if(tInput == 3)
		{
			pizza.addTopping(new PizzaTopping("Cheese", .50, false));
			System.out.println("You've selected 'Cheese'.");
		}
		else if(tInput == 4)
		{
			pizza.addTopping(new PizzaTopping("Ham", 1.25, true));
			System.out.println("You've selected 'Ham'.");
		}
		else if(tInput == 5)
		{
			pizza.addTopping(new PizzaTopping("Pepperoni", 1.50, true));
			System.out.println("You've selected 'Pepperoni'.");
		}
		else if(tInput == 6)
		{
			pizza.addTopping(new PizzaTopping("Bacon", 2.00, true));
			System.out.println("You've selected 'Bacon'.");
		}
		else if(tInput == 7)
		{
			pizza.addTopping(new PizzaTopping("Chicken", 1.75, true));
			System.out.println("You've selected 'Chicken'.");
		}
		else if(tInput == 8)
		{
			pizza.addTopping(new PizzaTopping("Ground Beef", 1.50, true));
			System.out.println("You've selected 'Ground Beef'.");
		}
		else if(tInput == 9)
		{
			pizza.addTopping(new PizzaTopping("Mushrooms", 0.75, false));
			System.out.println("You've selected 'Mushrooms'.");
		}
		else if(tInput == 10)
		{
			pizza.addTopping(new PizzaTopping("Onions", 0.75, false));
			System.out.println("You've selected 'Onions'.");
		}
		else if(tInput == 11)
		{
			pizza.addTopping(new PizzaTopping("Peppers", 1.00, false));
			System.out.println("You've selected 'Peppers'.");
		}
		else if(tInput == 12)
		{
			pizza.addTopping(new PizzaTopping("Pineapple", 1.25, false));
			System.out.println("You've selected 'Pineapple'.");
		}
		else if(tInput == 13)
		{
			pizza.addTopping(new PizzaTopping("Sweetcorn", 0.50, false));
			System.out.println("You've selected 'Sweetcorn'.");
		}
		} while(tInput != 0);	//If tInput is 0 then do...while loop ends.
	}
	
}
PizzaMenu.java
//Name:		Ankit Singh - 2020B0123006
//Program:		Project two - PizzaChoice
//Module:		CSC1021 - Programming I
//Description:	A class that will show the user a menu of bases and toppings modeled on previous classes
//				and takes the user selection. It will then build a pizza modeled according to the pizza class
//				and call the method "pizza.total" to show a summary and the total cost of the pizza.

import java.util.Scanner;

public class PizzaMenu
{
	private static int pIn;					//Initialize variable for pizza selection.
	private static Scanner keyboard;			//Initialize scanner for user input.
	
	public static void main(String[] args) 			//Main method
	{
		Pizza pizza = new Pizza();			//New pizza object.
		menu(pizza);					//Calls menu method.
		try						//Try menu selection method (user input)
		{
			menuSelect(pizza);
		}
        catch(IllegalArgumentException iae)			//Catches error thrown by the menu selection method.
		{
        		System.out.println("Invalid selection, please select again");		//Shows user error method.
        		menuSelect(pizza);							//Continues menu selection method.
		}
		pizza.total();					//Pizza summary method.
	}
	
	public static void menu(Pizza pizza)			//Method for printing table of pizzas.
	{
		keyboard = new Scanner(System.in);		//Declaring keyboard as scanner, else null pointer exception will occur.
		
		System.out.println("Pizza selection");
		String newLine = System.getProperty("line.separator");					//Initialize "newLine" to enter a newline when entered in a system.out statement.
		System.out.print("\t-----------------------------------------" + newLine);		//Prints top border.
		System.out.format("\t%15s%25s", "-Pizzas-",  "-Description- "+ newLine);		//Prints header for the table.
		System.out.print("\t-----------------------------------------" + newLine);		//Prints border.
		
		System.out.format("\t%-5s%1s\t\t%10s", "1.", "Margherita", "Cheese and tomato" + newLine);		//Prints strings that contain pizza name and a brief...
		System.out.format("\t%-5s%1s\t\t%10s", "2.", "Hawaiian", "Ham and pineapple" + newLine);			//... description.
		System.out.format("\t%-5s%1s\t\t%10s", "3.", "Americano", "Chicken, pepperoni and onions" + newLine);
		System.out.format("\t%-5s%1s\t\t%10s", "4.", "TexasBBQ", "Chicken, peppers and Bacon" + newLine);
		System.out.format("\t%-5s%1s\t\t%10s", "5.", "Veggie", "Peppers, mushrooms, onions and sweetcorn" + newLine);
	
		System.out.print(newLine + "\t-----------------------------------------" + newLine);	//Prints border.
	}
	
	public static void menuSelect(Pizza pizza)
	{
		System.out.println("Please enter your pizza by entering its respective number.");	//System out message for user.
		pIn = keyboard.nextInt();								//Uses user input as pIn.

		if(pIn<1||pIn>5)									//If statement for if the input is not valid.
		{
			throw new IllegalArgumentException("\nMust enter a number between 1 and 5.\nPlease run again.");	//Throws exception.
		}
		else if(pIn == 1)									//Else if loop for setting the pizza base.
		{
			margherita(pizza);								//Calls margherita method that builds the pizza.
			System.out.println("You've selected 'Margherita'.\n");				//Confirmation message for user.
		}
		else if(pIn == 2)
		{
			hawaiian(pizza);								//Calls hawaiian method that builds the pizza.																					
			System.out.println("You've selected 'Hawaiian'.\n");				//Confirmation message for user.
		}
		else if(pIn == 3)
		{
			americano(pizza);								//Calls americano method that builds the pizza.
			System.out.println("You've selected 'Americano'.\n");				//Confirmation message for user.
		}
		else if(pIn == 4)
		{
			texasBBQ(pizza);								//Calls texasBBQ method that builds the pizza.
			System.out.println("You've selected 'TexasBBQ'.\n");				//Confirmation message for user.
		}
		else if(pIn == 5)
		{
			veggie(pizza);																//Calls veggie method that builds the pizza.
			System.out.println("You've selected 'Veggie'.\n");				//Confirmation message for user.
		}
		pizza.setpIn(pIn);
	}
	
	
	//******************************Predefined pizza methods for the menu******************************//
	
	public static void margherita(Pizza pizza)
	{
		pizza.setPizzaBase(new PizzaTopping("thin", 2.50, false));			//Creates and adds base object to the pizza object.
		pizza.addTopping(new PizzaTopping("Tomato Sauce",0.50, false));			//Creates and adds topping object to the pizza object.	
		pizza.addTopping(new PizzaTopping("Cheese",0.50, false));			//Creates and adds topping object to the pizza object.	
	}
	
	public static void hawaiian(Pizza pizza)
	{
		pizza.setPizzaBase(new PizzaTopping("thin", 2.50, false));			//Creates and adds base object to the pizza object.
		pizza.addTopping(new PizzaTopping("Tomato Sauce",0.50, false));			//Creates and adds topping object to the pizza object.	
		pizza.addTopping(new PizzaTopping("Cheese",0.50, false));			//Creates and adds topping object to the pizza object.	
		pizza.addTopping(new PizzaTopping("Ham",1.25, true));				//Creates and adds topping object to the pizza object.
		pizza.addTopping(new PizzaTopping("Pineapple",1.25, false));			//Creates and adds topping object to the pizza object.
	}	
	
	public static void americano(Pizza pizza)
	{
		pizza.setPizzaBase(new PizzaTopping("Stuffed crust", 4.50, false));		//Creates and adds base object to the pizza object.
		pizza.addTopping(new PizzaTopping("BBQ Sauce",0.50, false));			//Creates and adds topping object to the pizza object.	
		pizza.addTopping(new PizzaTopping("Cheese",0.50, false));			//Creates and adds topping object to the pizza object.	
		pizza.addTopping(new PizzaTopping("Chicken",1.75, true));			//Creates and adds topping object to the pizza object.
		pizza.addTopping(new PizzaTopping("Pepperoni",1.50, true));			//Creates and adds topping object to the pizza object.
		pizza.addTopping(new PizzaTopping("Onion",0.75, false));			//Creates and adds topping object to the pizza object.
		
	}
	
	public static void texasBBQ(Pizza pizza)
	{
		pizza.setPizzaBase(new PizzaTopping("thick", 3.00, false));			//Creates and adds base object to the pizza object.
		pizza.addTopping(new PizzaTopping("BBQ Sauce",0.50, false));			//Creates and adds topping object to the pizza object.	
		pizza.addTopping(new PizzaTopping("Cheese",0.50, false));			//Creates and adds topping object to the pizza object.	
		pizza.addTopping(new PizzaTopping("Chicken",1.75, true));			//Creates and adds topping object to the pizza object.
		pizza.addTopping(new PizzaTopping("Peppers",1.00, false));			//Creates and adds topping object to the pizza object.
		pizza.addTopping(new PizzaTopping("Bacon",2.00, true));				//Creates and adds topping object to the pizza object.
	}
	
	public static void veggie(Pizza pizza)
	{
		pizza.setPizzaBase(new PizzaTopping("thin", 2.50, false));			//Creates and adds base object to the pizza object.
		pizza.addTopping(new PizzaTopping("Tomato Sauce",0.50, false));			//Creates and adds topping object to the pizza object.	
		pizza.addTopping(new PizzaTopping("Cheese",0.50, false));			//Creates and adds topping object to the pizza object.	
		pizza.addTopping(new PizzaTopping("Peppers",1.00, false));			//Creates and adds topping object to the pizza object.
		pizza.addTopping(new PizzaTopping("Mushrooms",0.75, false));			//Creates and adds topping object to the pizza object.
		pizza.addTopping(new PizzaTopping("Onions",0.75, false));			//Creates and adds topping object to the pizza object.
		pizza.addTopping(new PizzaTopping("Sweetcorn",0.50, false));			//Creates and adds topping object to the pizza object.
	}
	
	
	
}
PizzaTopping.java
//Name:		Ankit Singh - 2020B0123006
//Program:		Project two - PizzaTopping
//Module:		CSC1021 - Programming I
//Description:	This class extends PizzaBase and builds the base and toppings.

public class PizzaTopping extends PizzaBase
{
										//No main method
	
	public PizzaTopping(String Name, double Cost, boolean vegetarian)	//Pizza topping constructor.
	{
		setName(Name);			//Sets the object's name using a set method.
		setCost(Cost);			//Sets the object's cost using a set method.
		setVeg(vegetarian);		//Sets object's boolean for vegetarian using a setter method.
	}

	

}
@2020B0123006
 
