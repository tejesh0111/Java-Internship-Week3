import java.io.*;
import java.util.*;

// Class representing a Bank Account
class Account {
    private String name;
    private String accountNumber;
    private double balance;
    private List<String> transactionHistory;

    public Account(String name, String accountNumber, double initialBalance) {
        this.name = name;
        this.accountNumber = accountNumber;
        this.balance = initialBalance;
        this.transactionHistory = new ArrayList<>();
        transactionHistory.add("Account created with balance: " + initialBalance);
    }

    public void deposit(double amount) {
        balance += amount;
        transactionHistory.add("Deposited: " + amount);
        System.out.println("Money Deposited Successfully!");
    }

    public void withdraw(double amount) {
        if (amount > balance) {
            System.out.println("Insufficient Balance!");
        } else {
            balance -= amount;
            transactionHistory.add("Withdrawn: " + amount);
            System.out.println("Money Withdrawn Successfully!");
        }
    }

    public double getBalance() {
        return balance;
    }

    public void viewTransactionHistory() {
        System.out.println("Transaction History:");
        for (String transaction : transactionHistory) {
            System.out.println(transaction);
        }
    }
}

public class Main {
    private static final Scanner scanner = new Scanner(System.in);
    private static final Map<String, Account> accounts = new HashMap<>();

    public static void main(String[] args) {
        while (true) {
            System.out.println("\nWelcome to Bank Management System");
            System.out.println("1. Create Account");
            System.out.println("2. Deposit Money");
            System.out.println("3. Withdraw Money");
            System.out.println("4. Check Balance");
            System.out.println("5. View Transaction History");
            System.out.println("6. Exit");
            System.out.print("Enter your choice: ");
            
            int choice = scanner.nextInt();
            scanner.nextLine(); // Consume newline character
            
            switch (choice) {
                case 1:
                    createAccount();
                    break;
                case 2:
                    depositMoney();
                    break;
                case 3:
                    withdrawMoney();
                    break;
                case 4:
                    checkBalance();
                    break;
                case 5:
                    viewTransactionHistory();
                    break;
                case 6:
                    System.out.println("Exiting... Thank you!");
                    return;
                default:
                    System.out.println("Invalid choice! Please try again.");
            }
        }
    }

    private static void createAccount() {
        System.out.print("Enter Name: ");
        String name = scanner.nextLine();
        System.out.print("Enter Account Number: ");
        String accNum = scanner.nextLine();
        System.out.print("Enter Initial Balance: ");
        double balance = scanner.nextDouble();
        scanner.nextLine(); // Consume newline character
        
        if (accounts.containsKey(accNum)) {
            System.out.println("Account Number already exists!");
        } else {
            accounts.put(accNum, new Account(name, accNum, balance));
            System.out.println("Account Created Successfully!");
        }
    }

    private static void depositMoney() {
        System.out.print("Enter Account Number: ");
        String accNum = scanner.nextLine();
        if (accounts.containsKey(accNum)) {
            System.out.print("Enter Deposit Amount: ");
            double amount = scanner.nextDouble();
            scanner.nextLine(); // Consume newline character
            accounts.get(accNum).deposit(amount);
        } else {
            System.out.println("Account Not Found!");
        }
    }

    private static void withdrawMoney() {
        System.out.print("Enter Account Number: ");
        String accNum = scanner.nextLine();
        if (accounts.containsKey(accNum)) {
            System.out.print("Enter Withdrawal Amount: ");
            double amount = scanner.nextDouble();
            scanner.nextLine(); // Consume newline character
            accounts.get(accNum).withdraw(amount);
        } else {
            System.out.println("Account Not Found!");
        }
    }

    private static void checkBalance() {
        System.out.print("Enter Account Number: ");
        String accNum = scanner.nextLine();
        if (accounts.containsKey(accNum)) {
            System.out.println("Current Balance: " + accounts.get(accNum).getBalance());
        } else {
            System.out.println("Account Not Found!");
        }
    }

    private static void viewTransactionHistory() {
        System.out.print("Enter Account Number: ");
        String accNum = scanner.nextLine();
        if (accounts.containsKey(accNum)) {
            accounts.get(accNum).viewTransactionHistory();
        } else {
            System.out.println("Account Not Found!");
        }
    }
}
