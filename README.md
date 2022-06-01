# BankApplication
Simple Bank application using Java

/* 1. Display a welcome message to the user with his or her name
 * 2. There are 5 options available for the use and they are check balance,deposit, withdraw, check previous transaction and exit
 */

import java.util.Scanner;

public class BankingApplication {

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		//create a scanner object and get input from the user
		//Scanner sc1 = new Scanner (System.in);
		//System.out.println("Enter a Character: ");
		//int number = sc1.nextInt();
		//char letter = sc1.next().charAt(0); //Taking signal character from user input of a string
		//System.out.println("Character: " + letter);
		
		//To run this application,we have to create an object of BankAccount class
		//when the object is created, it will load the constructor. so we have to enter the arguments of the constructor as well
		BankAccount execute = new BankAccount("Randima", "BC1070001");
		execute.showMenu(); //call the showMenu method using the object
		
	}
}

		class BankAccount{
			int balance;
			int previousTransaction; //previous withdrawal amount or deposit amount
			String customerName;
			String customerId;
			
			//create a constructor. This will be helpful for the welcome message
			BankAccount(String cName, String cId){
				customerName = cName;
				customerId = cId;
			}
			
			//Declare the first method (Function): method to deposit money
			void deposit(int amountDeposited) {
				//when not deposited, we don't want this code to run. Therefore if condition is used
				if (amountDeposited != 0) {
				balance = balance + amountDeposited;
				previousTransaction = amountDeposited;	
				}
			}
			
			//method to withdraw money
			void withdraw (int amountWithdrawn) {
				if (amountWithdrawn != 0) { //we don't want withdraw zero amount
					balance = balance - amountWithdrawn;
					previousTransaction = -(amountWithdrawn);	//minus sign is used to emphasize withdrawal
					}
			}
			
			//method to get previous transaction
			void getPreviousTransaction() {
				if (previousTransaction > 0) {
					System.out.println("Deposited amount: " + previousTransaction );
				} else if (previousTransaction < 0) {
					System.out.println("Withdrawal amount: " + Math.abs(previousTransaction) );
				}else {
					System.out.println("No transaction happened");
				}
			}
			
			//method to show menu
			void showMenu() {
				//No need to create multiple objects, just create one object and call the actions through it
				Scanner sc = new Scanner(System.in); 
				
				char option = '\0'; 
				//(char) 0 and '\0' is the same value, but '\0' is most used, 
				//because this is the char intended for null character.
				
				System.out.println("Welcome " + customerName + "!");
				System.out.println("Your customer ID is " + customerId );
				System.out.println("A: Check Balance");
				System.out.println("B: Deposit");
				System.out.println("C: Withdraw");
				System.out.println("D. Previous Transaction");
				System.out.println("E: Exit");
			
			
			//Do while loop is used as no of iterations unknown
			//While loop is not used as we need at least one time showing the menu. so do while loop is used
			do{
				System.out.println("..............................................");
				System.out.println("Enter an option: ");
				System.out.println("..............................................");
				option = sc.next().charAt(0);
				System.out.println ("\n");
				
				switch (option) {
				
				case 'A':
					System.out.println("..............................................");
					System.out.println("Balance: " + balance);
					System.out.println("..............................................");
					System.out.println ("\n");
					break;
					
				case 'B':
					System.out.println("..............................................");
					System.out.println("Enter the amount to be deposited: ");
					int amountDeposited  = sc.nextInt();
					deposit(amountDeposited);
					System.out.println ("\n");
					break;
					
				case 'C':
					System.out.println("..............................................");
					System.out.println("Enter the amount to be withdrawn: ");
					int amountWithdrawn  = sc.nextInt();
					withdraw(amountWithdrawn);
					System.out.println ("\n");
					break;
				
				case 'D':
					System.out.println("..............................................");
					getPreviousTransaction();
					System.out.println("..............................................");
					System.out.println ("\n");
					break;
				
				case 'E':
					System.out.println ("********************************************");
					break;
					
				default:
					System.out.println ("Invalid option! Please enter again.");
					break;
				}
				
			} while (option != 'E');
			
			System.out.println("Thank you for using our services!");
			sc.close(); //scanner object should be closed in the relevant method it was created.
			}
		}
		
		
		//warning in this program: resource leak 'sc' is never closed
		//What happens if scanner is not closed?
		//If you do not close the scanner class, it will generate warnings like Resource leak. 
		//Resource leak happens when a program doesn't release the resources it has acquired. 
		//As OS have limit on the no of sockets,file handle,database conn etc thus,
		//its extremely important to manage these non-memory resources explicitly.
		
		//It is recommended to always close the Scanner when we are reading a file. 
		//It ensures that no input or output stream is opened, which is not in use
		
		//java.util.Scanner.close() Method
		//close() method closes this scanner. If this scanner has not yet been closed,
		//then if its underlying readable also implements the Closeable interface then the readable's close method will be invoked.
