# turkcell_se


```
package appPack;

import java.sql.PreparedStatement;
import java.sql.ResultSet;
import javax.swing.JOptionPane;
import props.User;

public class Model {
    
    static User us = new User();
    
    
    public boolean userLogin( String mail, String pass ) {
        boolean statu = false;
        try {
            DB db = new DB();
            String query = "select * from INFORMATION_SCHEMA.user where mail = ? and pass = ?";
            PreparedStatement pre = db.connect(query);
            pre.setString(1, mail);
            pre.setString(2, pass);
            ResultSet rs = pre.executeQuery();
            statu = rs.next();
            if (statu) {
                us.setUid(rs.getInt("uid"));
                us.setName(rs.getString("name"));
                us.setMail(rs.getString("mail"));
            }
            db.close();
        } catch (Exception e) {
            System.err.println("Login Error : " + e);
        }
        return statu;
    }
    
    
    
    // product insert
    public int productInsert( String title, String barcode, String stoc, String price ) {
        
        int rowCount = 0;
        try {
            DB db = new DB();
            String query = "insert into INFORMATION_SCHEMA.product values ( null, ?, ?, ?, ? )  ";
            PreparedStatement pre = db.connect(query);
            pre.setString(1, title);
            pre.setString(2, barcode);
            pre.setInt(3, Integer.parseInt(stoc));
            pre.setDouble(4, Double.parseDouble(price));
            rowCount = pre.executeUpdate();
            db.close();
        } catch (Exception e) {
            System.err.println("Insert Error : " + e);
            JOptionPane.showMessageDialog(null, "Stok(30) not empty, price(10.5) not empty");
        }
        return rowCount;
        
    }
    
    
    
}

```
