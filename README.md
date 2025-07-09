# project1
<br>
//LEVEL-1 TASK-1 NUMBER GAME

<br>
import java.util.Scanner;
<br>
import java.util.Random;
<br>

public class NumberGuessingGame {
<br>
    public static void main(String[] args) {
    <br>
        Scanner scanner = new Scanner(System.in);
        <br>
        Random random = new Random();

        int lowerBound = 1;
        int upperBound = 100;
        int maxAttempts = 7;
        int roundsPlayed = 0;
        int roundsWon = 0;

        System.out.println("🎯 Welcome to the Number Guessing Game!");

        boolean playAgain = true;
        while (playAgain) {
            int targetNumber = random.nextInt(upperBound - lowerBound + 1) + lowerBound;
            int attempts = 0;
            boolean guessedCorrectly = false;

            System.out.println("\n🔁 Round " + (roundsPlayed + 1));
            System.out.println("I'm thinking of a number between " + lowerBound + " and " + upperBound + ".");
            System.out.println("You have " + maxAttempts + " attempts to guess it!");

            while (attempts < maxAttempts) {
                System.out.print("Enter guess #" + (attempts + 1) + ": ");
                
                if (!scanner.hasNextInt()) {
                    System.out.println("Invalid input. Please enter a number.");
                    scanner.next(); // discard invalid input
                    continue;
                }

                int guess = scanner.nextInt();
                attempts++;

                if (guess == targetNumber) {
                    System.out.println("✅ Correct! You've guessed the number!");
                    guessedCorrectly = true;
                    roundsWon++;
                    break;
                } else if (guess < targetNumber) {
                    System.out.println("📉 Too low!");
                } else {
                    System.out.println("📈 Too high!");
                }
            }

            if (!guessedCorrectly) {
                System.out.println("❌ You're out of attempts. The number was: " + targetNumber);
            }

            roundsPlayed++;

            System.out.print("Do you want to play another round? (yes/no): ");
            scanner.nextLine(); // consume leftover newline
            String response = scanner.nextLine().trim().toLowerCase();
            playAgain = response.equals("yes") || response.equals("y");
        }

        System.out.println("\n🎉 Game Over!");
        System.out.println("Total Rounds Played: " + roundsPlayed);
        System.out.println("Rounds Won: " + roundsWon);
        System.out.println("Thanks for playing!");

        scanner.close();
    }
}



// TASK-2 STUDENT GRADE CALCULATOR

<br>
import java.util.Scanner;

public class GradeCalculator {

    public static char calculateGrade(double percentage) {
        if (percentage >= 90) {
            return 'A';  // A+
        } else if (percentage >= 80) {
            return 'B';  // A
        } else if (percentage >= 70) {
            return 'C';  // B
        } else if (percentage >= 60) {
            return 'D';  // C
        } else {
            return 'F';  // Fail
        }
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.print("Enter number of subjects: ");
        int numSubjects = scanner.nextInt();

        double[] marks = new double[numSubjects];
        double totalMarks = 0;

        for (int i = 0; i < numSubjects; i++) {
            System.out.print("Enter marks for subject " + (i + 1) + " (out of 100): ");
            marks[i] = scanner.nextDouble();

            if (marks[i] < 0 || marks[i] > 100) {
                System.out.println("Invalid input. Marks must be between 0 and 100.");
                scanner.close();
                return;
            }

            totalMarks += marks[i];
        }

        double averagePercentage = totalMarks / numSubjects;
        char grade = calculateGrade(averagePercentage);

        // Display results
        System.out.println("\n--- Result ---");
        System.out.println("Total Marks: " + totalMarks + " / " + (numSubjects * 100));
        System.out.printf("Average Percentage: %.2f%%\n", averagePercentage);
        System.out.println("Grade: " + grade);

        scanner.close();
    }
}



//LEVEL-2 TASK-1 ATM INTERFACE

<br>
import java.util.Scanner;

// Class representing the user's bank account
<br>
class BankAccount {
<br>
    private double balance;

    public BankAccount(double initialBalance) {
        balance = initialBalance;
    }

    public void deposit(double amount) {
        if (amount > 0) {
            balance += amount;
            System.out.println("Deposit successful. New balance: $" + balance);
        } else {
            System.out.println("Invalid deposit amount.");
        }
    }

    public void withdraw(double amount) {
        if (amount <= 0) {
            System.out.println("Invalid withdrawal amount.");
        } else if (amount > balance) {
            System.out.println("Insufficient balance.");
        } else {
            balance -= amount;
            System.out.println("Withdrawal successful. New balance: $" + balance);
        }
    }

    public void checkBalance() {
        System.out.println("Current balance: $" + balance);
    }
}

// Class representing the ATM machine
class ATM {
    private BankAccount account;
    private Scanner scanner;

    public ATM(BankAccount account) {
        this.account = account;
        scanner = new Scanner(System.in);
    }

    public void showMenu() {
        int choice;
        do {
            System.out.println("\n===== ATM Menu =====");
            System.out.println("1. Check Balance");
            System.out.println("2. Deposit");
            System.out.println("3. Withdraw");
            System.out.println("4. Exit");
            System.out.print("Choose an option: ");
            choice = scanner.nextInt();

            switch (choice) {
                case 1:
                    account.checkBalance();
                    break;
                case 2:
                    System.out.print("Enter deposit amount: ");
                    double depositAmount = scanner.nextDouble();
                    account.deposit(depositAmount);
                    break;
                case 3:
                    System.out.print("Enter withdrawal amount: ");
                    double withdrawAmount = scanner.nextDouble();
                    account.withdraw(withdrawAmount);
                    break;
                case 4:
                    System.out.println("Thank you for using the ATM.");
                    break;
                default:
                    System.out.println("Invalid option. Try again.");
            }
        } while (choice != 4);
    }
}

// Main class
<br>
public class SimpleATM {
<br>
    public static void main(String[] args) {
    <br>
        BankAccount myAccount = new BankAccount(1000.00); // Starting balance
        <br>
        ATM atm = new ATM(myAccount);
        <br>
        atm.showMenu();
    }
}

