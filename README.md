# generateRandomNumber
import java.util.Random;
import java.util.Scanner;

public class GuessTheNumber {
    private static final int MAX_ATTEMPTS = 10; 
    private static final int RANGE_MIN = 1; 
    private static final int RANGE_MAX = 100; 
    private static int score = 0; 

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        boolean playAgain;

        do {
            playAgain = false;
            int randomNumber = generateRandomNumber(RANGE_MIN, RANGE_MAX);
            int attempts = 0;

            System.out.println("Welcome to the Guess the Number Game!");
            System.out.println("I have selected a number between " + RANGE_MIN + " and " + RANGE_MAX + ".");
            System.out.println("You have " + MAX_ATTEMPTS + " attempts to guess it.");

            while (attempts < MAX_ATTEMPTS) {
                System.out.print("Enter your guess: ");
                int userGuess = scanner.nextInt();
                attempts++;

                if (userGuess < RANGE_MIN || userGuess > RANGE_MAX) {
                    System.out.println("Please guess a number within the range of " + RANGE_MIN + " to " + RANGE_MAX + ".");
                } else if (userGuess < randomNumber) {
                    System.out.println("Higher! Try again.");
                } else if (userGuess > randomNumber) {
                    System.out.println("Lower! Try again.");
                } else {
                    System.out.println("Congratulations! You've guessed the number in " + attempts + " attempts.");
                    score += (MAX_ATTEMPTS - attempts + 1); 
                    System.out.println("Your score: " + score);
                    break;
                }

                if (attempts == MAX_ATTEMPTS) {
                    System.out.println("Sorry, you've used all your attempts. The number was " + randomNumber + ".");
                }
            }

            System.out.print("Do you want to play again? (yes/no): ");
            String response = scanner.next().toLowerCase();
            if (response.equals("yes")) {
                playAgain = true;
            }

        } while (playAgain);

        System.out.println("Thank you for playing! Your final score is: " + score);
        scanner.close();
    }

    private static int generateRandomNumber(int min, int max) {
        Random random = new Random();
        return random.nextInt((max - min) + 1) + min;
    }
}
