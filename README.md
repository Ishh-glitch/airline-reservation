# airline-reservation
import java.util.Scanner;

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

    public void firstClassSeat() // assign first class seat
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
                    System.out.println("Sorry, flight fully booked. Next flight is in 3 hours.");
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

    public void economySeat() // assign an economy seat
    {
        for ( int count = 16; count <= 40; count++ )
        {
            if ( seating[count] == false ) // if false, then a seat is available for assignment
            {
                seating[count] = true; // assign seat
                System.out.println("Economy. Seat# %d\n", count);
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
                    System.out.println("Economy is fully booked. Would you like First Class? 1 for Yes 2 for No");
                    int choice = input.nextInt();
                    if ( choice == 1 )
                    {
                        firstClassSeat();
                        start();
                    }
                    else
                    {
                        System.out.println("Next flight is in 3 hours");
                        System.exit(0);
                    }
                }
            }
        }
    }
}
