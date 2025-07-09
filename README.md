# project1
<br>
//NUMBER GAME
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



//STUDENT GRADE CALCULATOR
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
