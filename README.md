package com.mycompany.booking;

/**
 *
 * @author dell user
 */
import java.util.*;




public class Airline {
 static boolean[] seating = new boolean[41]; /* creates 40 seat numbers (array[0] will not be used). Empty seat indicated by false*/
 static Scanner userinput = new Scanner(System.in);
 
static public int seat;
static public String trip;
static public String departure;
static public String destination;
static public String customer;
static public String Full_name;
static private int card_number;
static private int expiration_date;
static private int security_number;
static public String plan;

public static void Booking_information(){
System.out.println("WELCOME TO AIRBOOKING SERVICE HOW MAY WE HELP YOU TODAY\n To use our services you first have to register ");
register();
}

    public static void start()
    {       
        while ( true )
        {
            Booking_information();
        }   
    }
    public static void register()
    {
        System.out.println("--------------------------------------------------------------------------");
       System.out.println("To register please enter in a username:");//prompts user to enter in a username
    
     String username;
     username = userinput.next();
     System.out.println("Please enter a password:");//prompts user to enter in a password
     String password;
     password = userinput.next();
    System.out.println("Thank you if you now want to make a reservation please type 1 if not type 2:");// System asks user if they want to make a reservation
     int user;
     user = userinput.nextInt();
     if (user ==1)
     {
         makeReservation();
     }
     else
     { 
         System.exit(0);
     }
     System.out.println("-----------------------------------------------------------------------------");
    }
    public static void departure_place()
    {
        System.out.println("Type your departure place either Standsted for London Stansted, JFK for New york (JFK) International Airport, Sydney airport for Sydney Sydney Airport:");//System prompts the user to type one of these airports as their departure place
         departure = userinput.next();
        if (departure == "stansted" ){
            System.out.println("You have chosen London Stansted");     //whichever airport is chosen the system shows a message informing the user of what they picked
    }
        else if (departure == "JFK"){
      System.out.println("You have chosen New york JFK International Airport");
        }
        else if (departure == "sydney airport"){
        System.out.println("You have chosen Sydney Sydney Airport");
        }
        Arrival_destination();
    }
    public static void Arrival_destination(){
    System.out.println("Now please enter in your destination:");//System asks user to enter in their destination
   destination = userinput.next();
    System.out.printf("You have chosen. %S", destination);
    System.out.println("\nWhat class would you like to be seated in first class or economy type it in");// the system prompts the user to pick either first class or economy 
     customer = userinput.next();
    if(customer == "first class"){
    firstClassSeat();
    }
    else  {
    economySeat();
    }
    
    }

    public static void makeReservation()
    {
      System.out.println("To start reservation type 1 if not type 2:");
        int section = userinput.nextInt();
        if ( section == 1 )
        {
            departure_place();
        }
        else
        {
            start();
        }
    }
    
    public static void firstClassSeat() // assign a first class seat
    {
         
        for (  seat = 1; seat <= 15; seat++ )
        {
            if ( seating[seat] == false )  // if false, then a seat is available for assignment
            {
                seating[seat] = true;  // assign seat
                System.out.printf("First Class. Seat# %d\n", seat);
                roundway_oneway();
                break;
            }
            else if ( seating[15] == true ) // If seating[15] is true then first class is fully booked
            {
                if ( seating[40] == true) // If seating[40] is true then economy (and therefore whole flight) is fully booked
                {
                    System.out.println("Sorry this flight is fully booked, please try again in 3 hrs");
                }
                else //  gives the user a choice if they would want to book an economy seat.
                {
                    System.out.println("First Class is fully booked. Would you like Economy? 1 for Yes 2 for No");  
                    int choice = userinput.nextInt();
                    if ( choice == 1 )
                    {
                        economySeat();
                       
                    }
                    else
                    {
                        System.out.println("Next flight is in 3 hours.");// informs the user that a flight is coming in 3 hrs
                         
                        start();// goes back to start
                    }
                }
            }
        }
    }   

    public static void economySeat() // assigns an economy seat
    {
         
        for ( seat = 16; seat <= 40; seat++ )
        {
            if ( seating[seat] == false ) // if its false than a seat can be assgned
            {
                seating[seat] = true; // assigns a seat
                System.out.printf("Economy. Seat# %d\n", seat);
                System.out.println("Thank you for purchasing a seat. ");
                roundway_oneway();
               break;
            }
            else if ( seating[40] == true ) // If seating[40] is true then economy class is fully booked
            {
                if ( seating[15] == true) // If seating[15] is true then first class (therefore whole flight) is fully booked
                {
                    System.out.println("Sorry, flight fully booked. Next flight is in 3 hours.");
                    System.exit(0);// exits program
                }
                else // ask if passenger would like a first class ticket instead
                {
                    System.out.println("Economy is fully booked. Would you like to go to First class? 1 for Yes 2 for No");
                    int choice = userinput.nextInt();
                    if ( choice == 1 ) // this is if the user wants a first class seat
                    {
                        firstClassSeat();
                      
                    }
                    else
                    {
                        System.out.println("Next flight is in 3 hours"); // tells user that another flight is available in 3 hrs
                       
                        start();// goes back to start
                    }
                }
            }
        }
        
    }
    public static void roundway_oneway()
    {
      System.out.println("What trip would you like one way or round way:");//system asks user if they want a round way or one way trip
       trip = userinput.next();
      if (trip == "one way"){
          System.out.println("You have chosen a one way trip thank you for you joining us today.");
      }
      else { 
              System.out.println("You have chosen a round way trip thank you for joining us today.");    
          }
      showInfo();
      }

    /**
     *
     */
    public static void showInfo()// this method shows the users booking plan.
    {
    System.out.println("HERE IS YOUR PLAN :");
    plan = userinput.next();
   
        System.out.printf("Place of departure is:%s\n", departure);
        System.out.printf("Destination place is: %s\n", destination);
        System.out.printf("What class: %s\n", customer );
        System.out.printf("Seat number is: %d\n", seat);
        System.out.printf("type of trip: %s\n", trip );
    Payment();
    
    
    }
   public static void Payment(){//System prompts the user to type in their card details in order to pay.
   System.out.println("PLEASE ENTER YOUR FULL NAME:");
   Full_name = userinput.next();
   System.out.println("PLEASE ENTER A CARD NUMBER:");
   card_number = userinput.nextInt();
   if(card_number > 11){System.out.println("Error invalid input");
   Payment();
   }
   System.out.println("PLEASE ENTER AN EXPIRATION DATE:");
   expiration_date = userinput.nextInt();
   if(expiration_date > 4){System.out.println("Error invalid input");
   Payment();
   }
      System.out.println("PLEASE ENTER THE CARDS SECURITY NUMBER:");
   security_number = userinput.nextInt();
   if(security_number > 11){System.out.println("Error invalid input");
   Payment();
   }
  
  System.out.println("\nTHANK YOU FOR USING OUR SERVICES");
   
   System.exit(0);
   }
    
      public static void main(String[] args) {
        
      start();// start method in order to beginthe process
        
    }
    
    }
