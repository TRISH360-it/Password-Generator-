import java.util.*;

public class PasswordGenerator {

    public static String generatePassword(int length, boolean useUpper, boolean useLower, boolean useDigits, boolean useSpecial) {
        String upperCase = "ABCDEFGHIJKLMNOPQRSTUVWXYZ";
        String lowerCase = "abcdefghijklmnopqrstuvwxyz";
        String digits = "0123456789";
        String specialChars = "!@#$%^&*()-_=+<>?";

        StringBuilder characterPool = new StringBuilder();

        if (useUpper) characterPool.append(upperCase);
        if (useLower) characterPool.append(lowerCase);
        if (useDigits) characterPool.append(digits);
        if (useSpecial) characterPool.append(specialChars);

        if (characterPool.length() == 0) {
            throw new IllegalArgumentException("At least one character type must be selected.");
        }

        Random random = new Random();
        StringBuilder password = new StringBuilder();

        for (int i = 0; i < length; i++) {
            int index = random.nextInt(characterPool.length());
            password.append(characterPool.charAt(index));
        }

        return password.toString();
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.print("Enter desired password length: ");
        int length = scanner.nextInt();

        System.out.print("Include uppercase letters? (true/false): ");
        boolean useUpper = scanner.nextBoolean();

        System.out.print("Include lowercase letters? (true/false): ");
        boolean useLower = scanner.nextBoolean();

        System.out.print("Include digits? (true/false): ");
        boolean useDigits = scanner.nextBoolean();

        System.out.print("Include special characters? (true/false): ");
        boolean useSpecial = scanner.nextBoolean();

        try {
            String password = generatePassword(length, useUpper, useLower, useDigits, useSpecial);
            System.out.println("Generated Password: " + password);
        } catch (IllegalArgumentException e) {
            System.out.println("Error: " + e.getMessage());
        }
    }
}
