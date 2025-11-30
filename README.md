import java.util.Scanner;

public class ATMSystem {

    

    // --- BankAccount Class Definition (Step 4 & Part of Step 3) ---

    /**

     * Represents the user's bank account, storing the balance.

     */

    private static class BankAccount {

        private double balance;



        public BankAccount(double initialBalance) {

            this.balance = initialBalance;

        }



        /**

         * Step 3: Implement checkBalance()

         */

        public double checkBalance() {

            return balance;

        }



        /**

         * Step 3: Implement deposit(amount)

         */

        public void deposit(double amount) {

            // Step 6: Basic validation (ensure positive deposit amount)

            if (amount > 0) {

                balance += amount;

                System.out.printf("\n✅ Successfully deposited $%.2f%n", amount);

            } else {

                System.out.println("\n❌ Deposit amount must be positive."); // Step 7

            }

        }



        /**

         * Step 3: Implement withdraw(amount)

         * Step 6: Validate sufficient balance.

         */

        public boolean withdraw(double amount) {

            // Step 6: Validate sufficient balance

            if (amount > balance) {

                // Step 7: Display appropriate message for failure

                System.out.println("\n❌ Transaction failed: Insufficient balance.");

                return false;

            }



            // Step 6: Basic validation (ensure positive withdrawal amount)

            if (amount <= 0) {

                System.out.println("\n❌ Withdrawal amount must be positive."); // Step 7

                return false;

            }



            balance -= amount;

            System.out.printf("\n✅ Successfully withdrew $%.2f%n", amount); // Step 7

            return true;

        }

    }

    // -----------------------------------------------------------------





    // --- ATM Class Logic (Steps 1, 2, 5, 7) ---

    private BankAccount account;

    private Scanner scanner;



    /**

     * Step 1: Create a class (or logic) to represent the ATM machine.

     * Step 5: Connects the ATM logic with the BankAccount class.

     */

    public ATMSystem(BankAccount account) {

        this.account = account;

        this.scanner = new Scanner(System.in);

    }



    /**

     * Step 2: Design the user interface, displaying options.

     */

    private void displayMenu() {

        System.out.println("\n=== Welcome to the ATM Interface ===");

        System.out.println("1. Check Balance");

        System.out.println("2. Deposit");

        System.out.println("3. Withdraw");

        System.out.println("4. Exit");

        System.out.println("====================================");

        System.out.print("Enter your choice (1-4): ");

    }



    public void run() {

        int choice;

        do {

            displayMenu();

            try {

                choice = scanner.nextInt();

                

                switch (choice) {

                    case 1:

                        checkBalanceOption();

                        break;

                    case 2:

                        depositOption();

                        break;

                    case 3:

                        withdrawOption();

                        break;

                    case 4:

                        // Step 7: Display appropriate message

                        System.out.println("Thank you for using the ATM. Goodbye!");

                        break;

                    default:

                        // Step 7: Display appropriate message

                        System.out.println("Invalid choice. Please enter a number between 1 and 4.");

                }

            } catch (java.util.InputMismatchException e) {

                // Step 7: Handle non-integer input

                System.out.println("Invalid input. Please enter a valid number.");

                scanner.next(); // Clear the invalid input from the scanner

                choice = 0; // Set choice to non-exit value to loop again

            }

        } while (choice != 4);

    }



    private void checkBalanceOption() {

        double currentBalance = account.checkBalance();

        // Step 7: Display appropriate message

        System.out.printf("\n✅ Your current balance is: $%.2f%n", currentBalance);

    }



    private void depositOption() {

        System.out.print("Enter amount to deposit: $");

        try {

            double amount = scanner.nextDouble();

            // The deposit method handles Step 6 (validation) and Step 7 (messages)

            account.deposit(amount); 

        } catch (java.util.InputMismatchException e) {

            // Step 7: Handle non-double input

            System.out.println("❌ Invalid input for deposit amount.");

            scanner.next(); // Clear the invalid input

        }

    }



    private void withdrawOption() {

        System.out.print("Enter amount to withdraw: $");

        try {

            double amount = scanner.nextDouble();

            // The withdraw method handles Step 6 (validation) and Step 7 (messages)

            account.withdraw(amount); 

            // Note: withdraw() prints success/failure message directly.

        } catch (java.util.InputMismatchException e) {

            // Step 7: Handle non-double input

            System.out.println("❌ Invalid input for withdrawal amount.");

            scanner.next(); // Clear the invalid input

        }

    }



    // --- Execution Entry Point ---

    public static void main(String[] args) {

        // Initialize a bank account with an initial balance

        BankAccount userAccount = new BankAccount(1000.00);

        

        // Create the ATM system, linking it to the user's account

        ATMSystem atmMachine = new ATMSystem(userAccount);

        

        // Start the ATM simulation

        atmMachine.run();

    }

}
