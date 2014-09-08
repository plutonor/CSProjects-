CSProjects-
===========
/**
 * One100.java
 * @version 09/06/14
 * @author Thomas Noble
 */
import java.util.*;
import java.io.*;
import java.awt.*;

public class One100 {
   public static final int MAX/*1 to 2147483647*/= 100;
   public static void main(String[] args) {
      int num = 1;
      while (num != 0) {
      //makes the code run until you quit
         num = askNum();
         //num = 0 if responce was "quit" or "Quit"
         if (num != 0) {
            ArrayList factors = getFactors(num);
            toText(factors);
         }
      }
   }
   
   public static int askNum() {
   //asks and stores a number between 1 and MAX
      Scanner console = new Scanner(System.in);
      int num = 0;
      boolean good = true;
      //good is used to check that the input is a number between 1 and MAX or quit
      boolean quit = false;
      //quit is to tell if the input was quit
      System.out.println("Please input an integer from 1 to " + MAX + ".");
      String text = console.next();
      if (text.equals("quit") || text.equals("Quit")) {
      //checks if the input was quit
         quit = true;
      } else {
      //if the input wasn't quit, it figures out the number
         for (int i = 0; i < text.length(); i++) {
            if (text.charAt(i) - 48 > 9 || text.charAt(i) - 48 < 0) {
            //checks if the character is a number
               good = false;
               //if the character isn't a number, the input isn't "good"
            } else {
               num += ((text.charAt(i) - 48) * ((int) Math.pow(10, text.length() - 1 - i)));
               //This adds the number in the correct decimal place
            }
         }
      }
      if (!good || (num < 1 || num > MAX) && !quit) {
      //gives an error message for a bad entry and asks again
         System.out.println("ERROR! invalid entry");
         num = askNum();
      }
      if (quit) {
      //sets the number as 0 if the user wants to quit
         num = 0;
      }
      return num;
   }
   
   public static ArrayList getFactors(int num) {
      ArrayList factors = new ArrayList();
      ArrayList reverse = new ArrayList();
      for (double pFact = 1.; pFact <= Math.sqrt(num); pFact++) {
      //checks all ints between 1 and sqrt of the number for factors
      //pFact = possible Factor
         if (num / pFact == num / (int) pFact) {
         //checks that pFact is a factor
            factors.add((int) pFact);
            if (num / pFact != pFact) {
            //adds the complimetary factor to reverse if pFact ISN'T the sqrt
               reverse.add(num / (int) pFact);
            }
         }
      }
      for (int pFact = reverse.size() - 1; pFact >= 0; pFact--) {
      //reverses revers and adds the factors to factors
         factors.add(reverse.get(pFact));
      }
      factors.add(num);
      //for some reason, reverse doesn't include the original number
      return factors;
   }
   
   public static void toText(ArrayList factors) {
      System.out.print("factors: ");
      System.out.print("" + factors.get(0));
      //end post
      for (int current = 1; current < factors.size() - 1; current++) {
      //simple to text for loop
         System.out.print(", " + factors.get(current));
      }
      System.out.println();
      //prepares for next input
   }
}
