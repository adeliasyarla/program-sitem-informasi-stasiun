package ProyekStasiun;

import javax.swing.*;
import java.sql.*;

public class Connector {
    String DBurl      = "jdbc:mysql://localhost/stasiun_db";
    String DBusername = "root";
    String DBpassword = "";
    Connection koneksi;
    Statement statement;

    public Connector() {
        try{
            Class.forName("com.mysql.cj.jdbc.Driver");
            koneksi = (Connection) DriverManager.getConnection(DBurl,DBusername,DBpassword);
        }catch(Exception ex){
            System.out.println("Koneksi gagal, " + ex.getMessage());
        }
    }

    public String[][] ItemList() {
        try {
            int jmlData = 0;

            String data[][] = new String[getBanyakData()][7];

            String query = "SELECT * FROM schedule";
            ResultSet resultSet = statement.executeQuery(query);
            while (resultSet.next()) {
                data[jmlData][0] = resultSet.getString("kode_jadwal");
                data[jmlData][1] = resultSet.getString("nama_kereta");
                data[jmlData][2] = resultSet.getString("kelas");
                data[jmlData][3] = resultSet.getString("tujuan_akhir");
                data[jmlData][4] = resultSet.getString("jadwal_kereta");
                data[jmlData][5] = resultSet.getString("jam_keberangkatan");
                data[jmlData][6] = resultSet.getString("waktu_tempuh");
                jmlData++;
            }
            return data;

        } catch (SQLException e) {
            System.out.println(e.getMessage());
            System.out.println("SQL Error");
            return null;
        }
    }

    public void insertItem(String kode, String nama, String kelas, String tujuan, String jadwal, String jam, String waktu) {
        int jmlData = 0;
        double fwaktu = Float.parseFloat(waktu);
        try {
            String query = "SELECT * FROM schedule WHERE kode_jadwal='" + kode + "'";
            ResultSet resultSet = statement.executeQuery(query);

            while (resultSet.next()) {
                jmlData++;
            }

            if (jmlData == 0) {
                query = "INSERT INTO schedule VALUES ('" + kode + "', '" + nama + "', '" + kelas + "', '" + tujuan + "', '" + jadwal + "', '" + jam + "', '" + fwaktu + "')";
                statement = (Statement) koneksi.createStatement();
                statement.executeUpdate(query);
                System.out.println("Berhasil ditambahkan");
                JOptionPane.showMessageDialog(null, "Data berhasil ditambahkan");
            }
            else {
                JOptionPane.showMessageDialog(null, "Data Sudah Ada");
            }
        } catch (Exception sql) {
            System.out.println(sql.getMessage());
            JOptionPane.showMessageDialog(null, sql.getMessage());
        }
    }

    public void updateItem(String kode, String nama, String kelas, String tujuan, String jadwal, String jam, String waktu) {
        int jmlData = 0;
        double fwaktu = Float.parseFloat(waktu);
        try {
            String query = "SELECT * FROM schedule WHERE kode_jadwal='" + kode + "'";
            ResultSet resultSet = statement.executeQuery(query);

            while (resultSet.next()) {
                jmlData++;
            }

            if (jmlData == 1) {
                query = "UPDATE schedule SET nama_kereta='" + nama + "', kelas='" + kelas + "', tujuan_akhir='" + tujuan + "', jadwal_kereta='" + jadwal + "', jam_keberangkatan='" + jam + "', waktu_tempuh='" + fwaktu + "' WHERE kode_jadwal='" + kode + "'";
                statement = (Statement) koneksi.createStatement();
                statement.executeUpdate(query);
                System.out.println("Berhasil diupdate");
                JOptionPane.showMessageDialog(null, "Data berhasil diupdate");
            }
            else {
                JOptionPane.showMessageDialog(null, "Data Tidak Ada");
            }
        } catch (Exception sql) {
            System.out.println(sql.getMessage());
            JOptionPane.showMessageDialog(null, sql.getMessage());
        }
    }

    public void deleteItem(String kode) {
        int jmlData = 0;
        try {
            String query = "SELECT * FROM schedule WHERE kode_jadwal='" + kode + "'";
            ResultSet resultSet = statement.executeQuery(query);

            while (resultSet.next()) {
                jmlData++;
            }

            if (jmlData == 1) {
                query = "DELETE FROM schedule WHERE kode_jadwal='" + kode + "'";
                statement = (Statement) koneksi.createStatement();
                statement.executeUpdate(query);
                System.out.println("Berhasil dihapus");
                JOptionPane.showMessageDialog(null, "Data berhasil dihapus");
            }
            else {
                JOptionPane.showMessageDialog(null, "Data Tidak Ada");
            }
        } catch (Exception sql) {
            System.out.println(sql.getMessage());
            JOptionPane.showMessageDialog(null, sql.getMessage());
        }
    }

    public int getBanyakData() {
        int jmlData = 0;
        try {
            statement = koneksi.createStatement();
            String query = "SELECT * FROM schedule";
            ResultSet resultSet = statement.executeQuery(query);
            while (resultSet.next()) {
                jmlData++;
            }
            return jmlData;

        } catch (SQLException e) {
            System.out.println(e.getMessage());
            System.out.println("SQL error");
            return 0;
        }
    }

}
