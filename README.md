# Hotel-managemant-system
package jdbc;
import java.sql.*;
import java.util.Scanner;

public class JdbcHotelCrud {

    public static void main(String[] args) {

        String url = "jdbc:mysql://localhost:3306/hotel_db";  // Database name: hotel_db
        String user = "root"; 
        String pass = "@shree101";

        Scanner sc = new Scanner(System.in);

        try {
            // ⿡ Load and register driver
            Class.forName("com.mysql.cj.jdbc.Driver");

            // ⿢ Establish connection
            Connection con = DriverManager.getConnection(url, user, pass);
            System.out.println("✅ Connected to Hotel Management Database!");

            while (true) {
                System.out.println("\n=== Hotel Management Menu ===");
                System.out.println("1. Add Guest Record");
                System.out.println("2. Display All Guests");
                System.out.println("3. Update Guest Details");
                System.out.println("4. Delete Guest Record");
                System.out.println("5. Exit");
                System.out.print("Enter your choice: ");
                int choice = sc.nextInt();

                switch (choice) {

                    case 1:
                        // ➕ INSERT Operation
                        System.out.print("Enter Room No: ");
                        int roomNo = sc.nextInt();
                        sc.nextLine(); // consume newline
                        System.out.print("Enter Guest Name: ");
                        String guestName = sc.nextLine();
                        System.out.print("Enter Days Stayed: ");
                        int days = sc.nextInt();
                        System.out.print("Enter Bill Amount: ");
                        double bill = sc.nextDouble();

                        String insertQuery = "INSERT INTO hotel (room_no, guest_name, days_stayed, bill_amount) VALUES (?, ?, ?, ?)";
                        PreparedStatement psInsert = con.prepareStatement(insertQuery);
                        psInsert.setInt(1, roomNo);
                        psInsert.setString(2, guestName);
                        psInsert.setInt(3, days);
                        psInsert.setDouble(4, bill);

                        int inserted = psInsert.executeUpdate();
                        System.out.println(inserted + " record inserted successfully!");
                        psInsert.close();
                        break;

                    case 2:
                        // 📋 DISPLAY Operation
                        String selectQuery = "SELECT * FROM hotel";
                        Statement stmt = con.createStatement();
                        ResultSet rs = stmt.executeQuery(selectQuery);

                        System.out.println("\nRoom No\tGuest Name\tDays Stayed\tBill Amount");
                        System.out.println("----------------------------------------------------");
                        while (rs.next()) {
                            System.out.println(rs.getInt("room_no") + "\t" +
                                               rs.getString("guest_name") + "\t\t" +
                                               rs.getInt("days_stayed") + "\t\t" +
                                               rs.getDouble("bill_amount"));
                        }
                        rs.close();
                        stmt.close();
                        break;

                    case 3:
                        // ✏ UPDATE Operation
                        System.out.print("Enter Room No to update: ");
                        int updateRoom = sc.nextInt();
                        sc.nextLine();
                        System.out.print("Enter new Guest Name: ");
                        String newGuest = sc.nextLine();
                        System.out.print("Enter new Days Stayed: ");
                        int newDays = sc.nextInt();
                        System.out.print("Enter new Bill Amount: ");
                        double newBill = sc.nextDouble();

                        String updateQuery = "UPDATE hotel SET guest_name=?, days_stayed=?, bill_amount=? WHERE room_no=?";
                        PreparedStatement psUpdate = con.prepareStatement(updateQuery);
                        psUpdate.setString(1, newGuest);
                        psUpdate.setInt(2, newDays);
                        psUpdate.setDouble(3, newBill);
                        psUpdate.setInt(4, updateRoom);

                        int updated = psUpdate.executeUpdate();
                        System.out.println(updated + " record updated successfully!");
                        psUpdate.close();
                        break;

                    case 4:
                        // ❌ DELETE Operation
                        System.out.print("Enter Room No to delete: ");
                        int deleteRoom = sc.nextInt();

                        String deleteQuery = "DELETE FROM hotel WHERE room_no=?";
                        PreparedStatement psDelete = con.prepareStatement(deleteQuery);
                        psDelete.setInt(1, deleteRoom);

                        int deleted = psDelete.executeUpdate();
                        System.out.println(deleted + " record deleted successfully!");
                        psDelete.close();
                        break;

                    case 5:
                        // 🚪 EXIT
                        System.out.println("Exiting Hotel Management System... Goodbye!");
                        con.close();
                        sc.close();
                        System.exit(0);

                    default:
                        System.out.println("❌ Invalid choice! Try again.");
                }
            }

        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
package jdbc;
import java.sql.*;
import java.util.Scanner;

public class JdbcHotelCrud {

    public static void main(String[] args) {

        String url = "jdbc:mysql://localhost:3306/hotel_db";  // Database name: hotel_db
        String user = "root"; 
        String pass = "@shree101";

        Scanner sc = new Scanner(System.in);

        try {
            // ⿡ Load and register driver
            Class.forName("com.mysql.cj.jdbc.Driver");

            // ⿢ Establish connection
            Connection con = DriverManager.getConnection(url, user, pass);
            System.out.println("✅ Connected to Hotel Management Database!");

            while (true) {
                System.out.println("\n=== Hotel Management Menu ===");
                System.out.println("1. Add Guest Record");
                System.out.println("2. Display All Guests");
                System.out.println("3. Update Guest Details");
                System.out.println("4. Delete Guest Record");
                System.out.println("5. Exit");
                System.out.print("Enter your choice: ");
                int choice = sc.nextInt();

                switch (choice) {

                    case 1:
                        // ➕ INSERT Operation
                        System.out.print("Enter Room No: ");
                        int roomNo = sc.nextInt();
                        sc.nextLine(); // consume newline
                        System.out.print("Enter Guest Name: ");
                        String guestName = sc.nextLine();
                        System.out.print("Enter Days Stayed: ");
                        int days = sc.nextInt();
                        System.out.print("Enter Bill Amount: ");
                        double bill = sc.nextDouble();

                        String insertQuery = "INSERT INTO hotel (room_no, guest_name, days_stayed, bill_amount) VALUES (?, ?, ?, ?)";
                        PreparedStatement psInsert = con.prepareStatement(insertQuery);
                        psInsert.setInt(1, roomNo);
                        psInsert.setString(2, guestName);
                        psInsert.setInt(3, days);
                        psInsert.setDouble(4, bill);

                        int inserted = psInsert.executeUpdate();
                        System.out.println(inserted + " record inserted successfully!");
                        psInsert.close();
                        break;

                    case 2:
                        // 📋 DISPLAY Operation
                        String selectQuery = "SELECT * FROM hotel";
                        Statement stmt = con.createStatement();
                        ResultSet rs = stmt.executeQuery(selectQuery);

                        System.out.println("\nRoom No\tGuest Name\tDays Stayed\tBill Amount");
                        System.out.println("----------------------------------------------------");
                        while (rs.next()) {
                            System.out.println(rs.getInt("room_no") + "\t" +
                                               rs.getString("guest_name") + "\t\t" +
                                               rs.getInt("days_stayed") + "\t\t" +
                                               rs.getDouble("bill_amount"));
                        }
                        rs.close();
                        stmt.close();
                        break;

                    case 3:
                        // ✏ UPDATE Operation
                        System.out.print("Enter Room No to update: ");
                        int updateRoom = sc.nextInt();
                        sc.nextLine();
                        System.out.print("Enter new Guest Name: ");
                        String newGuest = sc.nextLine();
                        System.out.print("Enter new Days Stayed: ");
                        int newDays = sc.nextInt();
                        System.out.print("Enter new Bill Amount: ");
                        double newBill = sc.nextDouble();

                        String updateQuery = "UPDATE hotel SET guest_name=?, days_stayed=?, bill_amount=? WHERE room_no=?";
                        PreparedStatement psUpdate = con.prepareStatement(updateQuery);
                        psUpdate.setString(1, newGuest);
                        psUpdate.setInt(2, newDays);
                        psUpdate.setDouble(3, newBill);
                        psUpdate.setInt(4, updateRoom);

                        int updated = psUpdate.executeUpdate();
                        System.out.println(updated + " record updated successfully!");
                        psUpdate.close();
                        break;

                    case 4:
                        // ❌ DELETE Operation
                        System.out.print("Enter Room No to delete: ");
                        int deleteRoom = sc.nextInt();

                        String deleteQuery = "DELETE FROM hotel WHERE room_no=?";
                        PreparedStatement psDelete = con.prepareStatement(deleteQuery);
                        psDelete.setInt(1, deleteRoom);

                        int deleted = psDelete.executeUpdate();
                        System.out.println(deleted + " record deleted successfully!");
                        psDelete.close();
                        break;

                    case 5:
                        // 🚪 EXIT
                        System.out.println("Exiting Hotel Management System... Goodbye!");
                        con.close();
                        sc.close();
                        System.exit(0);

                    default:
                        System.out.println("❌ Invalid choice! Try again.");
                }
            }

        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
