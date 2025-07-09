# project1
<br>
//Number Guessing Game
import java.util.Scanner;
import java.util.Random;

public class NumberGuessingGame {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
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
