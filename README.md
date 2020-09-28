# airline-reservation
import java.util.Scanner;
import java.io.*;

public class Airline 
{
    boolean[] seating = new boolean[41]; /* create 40 seat numbers (array[0] will not be used). Empty seat indicated by false*/
    Scanner userinput = new Scanner(System.in);

    public void start()
    {       
        while ( true )
        {
            makeReservation();
        }   
    }

    public void makeReservation()
    {
        System.out.println("Please type 1 for First Class or 2 for Economy: ");
        int section = userinput.nextInt();
        if ( section == 1 )
        {
            firstClassSeat();
        }
        else
        {
            economySeat();
        }
    }

    public void firstClassSeat() // assign a first class seat
    {
        for ( int count = 1; count <= 15; count++ )
        {
            if ( seating[count] == false )  // if false, then a seat is available for assignment
            {
                seating[count] = true;  // assign seat
                System.out.printf("First Class. Seat# %d\n", count);
                break;
            }
            else if ( seating[15] == true ) // If seating[15] is true then first class is fully booked
            {
                if ( seating[40] == true) // If seating[40] is true then economy (and therefore whole flight) is fully booked
                {
                    System.out.println("Sorry this flight is fully booked, please try again in 3 hrs");
                }
                else // ask passenger if they would like an economy ticket instead
                {
                    System.out.println("First Class is fully booked. Would you like Economy? 1 for Yes 2 for No");
                    int choice = input.nextInt();
                    if ( choice == 1 )
                    {
                        economySeat();
                        start();
                    }
                    else
                    {
                        System.out.println("Next flight is in 3 hours.");
                        System.exit(0);
                    }
                }
            }
        }
    }   

    public void economySeat() // assigns a economy seat
    {
        for ( int count = 16; count <= 40; count++ )
        {
            if ( seating[count] == false ) // if its false than a seat can be assgned
            {
                seating[count] = true; // assign a seat
                System.out.printf("Economy. Seat# %d\n", count);
                break;
            }
            else if ( seating[40] == true ) // If seating[40] is true then economy is fully booked
            {
                if ( seating[15] == true) // If seating[15] is true then first class (and therefore whole flight) is fully booked
                {
                    System.out.println("Sorry, flight fully booked. Next flight is in 3 hours.");
                    System.exit(0);
                }
                else // ask if passenger would like a first class ticket instead
                {
                    System.out.println("Economy is fully booked. Would you like to go to First class? 1 for Yes 2 for No");
                    int choice = input.nextInt();
                    if ( choice == 1 ) // this is if the user wants first class
                    {
                        firstClassSeat();
                        start();
                    }
                    else
                    {
                        System.out.println("Next flight is in 3 hours"); // tells user that another flight is available in 3 hrs
                        System.exit(0);
                    }
                }
            }
        }
    }
}
