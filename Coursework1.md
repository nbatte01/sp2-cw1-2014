sp2-cw1-2014
============

/*This fragment of code was completed by Nicholas Jay Batten for Coursework number 1 
 * on 05/10/2014 as part of the software and programming 2 module at Birkbeck University
 */

import java.util.Scanner;
import java.util.Arrays;

public class coursework1
{
    final static int max = 100;
    public static void main(String []args)
    {
        System.out.print("\f"); //clears the terminal window of previous data
        Scanner in = new Scanner(System.in);
        int[] first = new int[max];
        int temp;
        int[] second = new int[max];
        boolean check;
        //Asks the user to enter integers for the first Array. loop exits once the user enters "0".
        for(int i = 0 ; i < first.length ; i++)
        {
            System.out.print("Please enter data for Array 1 (0 to finish): ");
            temp = in.nextInt();
            check = false;
            if(temp !=0)
            {
                 for(int n = 0 ; n < i ; n++)
                 {
                     if(temp == first[n])
                     {
                         check = true;
                     }
                 }
                 if(!check)
                 {
                     first[i] = temp;
                 }
            }
            else
            {
                break;
            }
        }
        //Asks the user to enter integers for the second Array. loop exits once the user enters "0".
        for(int i = 0 ; i < second.length ; i++)
        {
            System.out.print("Please enter data for Array 2 (0 to finish): ");
            temp = in.nextInt();
            check = false;
            if(temp !=0)
            {
                 for(int n = 0 ; n < i ; n++)
                 {
                     if(temp == second[n])
                     {
                         check = true;
                     }
                 }
                 if(!check)
                 {
                     second[i] = temp;
                 }
            }
            else
            {
                break;
            }
        }
        
        //Sends the arrays off to be compressed by removing excess "0"s
        int[]firstCompressed = compress(first);
        int[]secondCompressed = compress(second);
        System.out.println("Values for array 1 is: " + (Arrays.toString(firstCompressed)));
        System.out.println("Values for array 2 is: " + (Arrays.toString(secondCompressed)));
        
        //Sends the compressed arrays to 'compress' method to find the common elements in both Arrays then print
        int[] common = common(firstCompressed, secondCompressed);
        int commonCount = common.length;
        System.out.println("Common data is: " + (Arrays.toString(common)));
        System.out.println("Number of common elements: " + commonCount);
        
        //Sends the compressed arrays to 'unique' method to find the unqiue elements in each and then print 
        int[] unique1 = unique(firstCompressed, secondCompressed);
        System.out.println("the unique elements in the first array: " + (Arrays.toString(unique1)));
        int[] unique2 = unique(secondCompressed, firstCompressed);
        System.out.println("The unique elements in the second array: " + (Arrays.toString(unique2)));
    }
    
    public static int[] compress(int [] data)
    {
        int[] tempData = new int[max];
        int tempCount = 0;
        for(int i = 0 ; i < data.length ; i++)
        {
            int temp = data[i];
            if(data[i] != 0)
            {
                tempData[tempCount] = data[i];
                tempCount++;
            }
        }
        int[] consolidated = new int[tempCount];
        for(int i = 0 ; i < tempCount ; i++)
        {
            consolidated[i] = tempData[i];
        }
        return consolidated;
    }
    
    public static int[] common(int[] data1, int[] data2)
    {
        int length1 = data1.length;
        int length2 = data2.length;
        int largest = Math.max(length1,length2);
        int[] temp = new int[largest];
        boolean check;
        for(int i = 0 ; i < length1 ; i++)
        {
            check = false;
            for(int n = 0; n < length2; n++)
            {
                if(data1[i] == data2[n])
                {
                    check = true;
                }
            }
            if(check)
            {
                temp[i] = data1[i];
            }
        }
        int[] output = compress(temp);
        return output;
    }
    public static int[] unique(int [] data1, int[] data2)
    {
        int length1 = data1.length;
        int length2 = data2.length;
        int largest = Math.max(length1, length2);
        int[] temp = new int[largest];
        boolean check;
        for(int i = 0 ; i< length1 ; i++)
        {
            check = false;
            for( int n = 0 ; n < data2.length ; n++)
            {
                if(data1[i] == data2[n])
                {
                    check = true;
                }
            }
            if(!check)
            {
                temp[i] = data1[i];
            }
        }
        int[] output = compress(temp);
        return output;        
    }
}