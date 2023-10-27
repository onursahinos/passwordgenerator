import java.security.SecureRandom;
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.SQLException;
import java.util.ArrayList;
import java.util.List;
import java.util.Scanner;

public class PasswordGenerator {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.print("Bir büyük harf girin: ");
        String uppercase = scanner.nextLine();

        System.out.print("Bir küçük harf girin: ");
        String lowercase = scanner.nextLine();

        System.out.print("İki sayı girin: ");
        String digits = scanner.nextLine();

        System.out.print("Bir özel simge girin: ");
        String specialChars = scanner.nextLine();

        String password = generatePassword(uppercase, lowercase, digits, specialChars);

        System.out.println("Oluşturulan Şifre: " + password);

        List<String> passwordsList = new ArrayList<>();
        passwordsList.add(password);

        savePasswordsToDatabase(passwordsList);
    }

    public static String generatePassword(String uppercase, String lowercase, String digits, String specialChars) {
        SecureRandom random = new SecureRandom();
        StringBuilder password = new StringBuilder();

        password.append(uppercase.charAt(random.nextInt(uppercase.length())));
        password.append(lowercase.charAt(random.nextInt(lowercase.length())));

        for (int i = 0; i < 2; i++) {
            password.append(digits.charAt(random.nextInt(digits.length()));
        }

        password.append(specialChars.charAt(random.nextInt(specialChars.length()));

        String allChars = uppercase + lowercase + digits + specialChars;
        for (int i = 0; i < 5; i++) {
            password.append(allChars.charAt(random.nextInt(allChars.length()));
        }

        return password.toString();
    }

    public static void savePasswordsToDatabase(List<String> passwords) {
        String jdbcUrl = "jdbc:mysql://localhost:3306/passworgenerator";
        String username = "admin";
        String password = "admin";

        try (Connection connection = DriverManager.getConnection(jdbcUrl, username, password)) {
            connection.setAutoCommit(false);

            String insertQuery = "INSERT INTO passwords (password, created_at) VALUES (?, NOW())";
            try (PreparedStatement preparedStatement = connection.prepareStatement(insertQuery)) {
                for (String password : passwords) {
                    preparedStatement.setString(1, password);
                    preparedStatement.executeUpdate();
                }
                connection.commit();
                System.out.println("Password(s) saved to the database.");
            } catch (SQLException e) {
                connection.rollback();
                e.printStackTrace();
            }
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
}
