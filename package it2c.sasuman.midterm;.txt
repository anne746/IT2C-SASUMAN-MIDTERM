package it2c.sasuman.midterm;

import java.util.Scanner;

public class Patients {

    private static String resp;

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        while (true) {
            System.out.println("1. ADD");
            System.out.println("2. VIEW");
            System.out.println("3. UPDATE");
            System.out.println("4. DELETE");
            System.out.println("5. EXIT");

            System.out.print("Enter Action: ");
            int action = sc.nextInt();
            sc.nextLine();

            Patients test = new Patients();
            switch (action) {
                case 1:
                    test.addPatientsRecord();
                    break;
                case 2:
                    test.viewPatientsRecord();
                    break;
                case 3:
                    test.viewPatientsRecord();
                    test.updatePatients();
                    break;
                case 4:
                    test.viewPatientsRecord();
                    test.deletePatients();
                    test.viewPatientsRecord();
                    break;
                case 5:
                    System.exit(0);
                    break;
                default:
                    System.out.println("Invalid option. Please try again.");
                    break;
            }

            System.out.print("Continue? (y/n): ");
            resp = sc.next();
            if (!resp.equalsIgnoreCase("y")) {
                break;
            }
        }
        sc.close();
    }

    public void addPatientsRecord() {
        Scanner sc = new Scanner(System.in);
        config conf = new config();
        System.out.print("Patients First Name: ");
        String fname = sc.nextLine();
        System.out.print("Patients Last Name: ");
        String lname = sc.nextLine();
        System.out.print("Patients Date of Birth: ");
        String dbirth = sc.nextLine();
        System.out.print("Patients ContactNum: ");
        String cnum = sc.nextLine();
        System.out.print("Patients Address: ");
        String add = sc.nextLine();

        String sql = "INSERT INTO tbl_patients (p_fname, p_lname, p_dateofbirth, p_contactNum, p_address) VALUES (?, ?, ?, ?, ?)";
        conf.addRecord(sql, fname, lname, dbirth, cnum, add);
    }

    private void viewPatientsRecord() {
        String qry = "SELECT * FROM tbl_patients";
        String[] hdrs = {"ID", "First Name", "Last Name", "Date of Birth", "ContactNum", "Address"};
        String[] clms = {"p_id", "p_fname", "p_lname", "p_dbirth", "p_cnum", "p_add"};

        config conf = new config();
        conf.viewRecords(qry, hdrs, clms);
    }

    private void updatePatients() {
        Scanner sc = new Scanner(System.in);
        System.out.print("Enter the ID to Update: ");
        int id = sc.nextInt();
        sc.nextLine();

        System.out.print("Enter new First Name: ");
        String nfname = sc.nextLine();
        System.out.print("Enter new Last Name: ");
        String nlname = sc.nextLine();
        System.out.print("Enter new Date of Birth: ");
        String ndbirth = sc.nextLine();
        System.out.print("Enter new ContactNum: ");
        String ncnum = sc.nextLine();
        System.out.print("Enter new Address: ");
        String nadd = sc.nextLine();

        String qry = "UPDATE tbl_patients SET p_fname = ?, p_lname = ?, p_dateofbirth = ?, p_contactNum = ?, p_add = ? WHERE p_id = ?";

        config conf = new config();
        conf.updateRecord(qry, nfname, nlname, ndbirth, ncnum, nadd, id);
    }

    private void deletePatients() {
        Scanner sc = new Scanner(System.in);
        System.out.print("Enter the ID to Delete: ");
        int id = sc.nextInt();

        String qry = "DELETE FROM tbl_patients WHERE p_id = ?";

        config conf = new config();
        conf.deleteRecord(qry, id);
    }
}
