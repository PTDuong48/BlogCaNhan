---
title: "Hướng Dẫn Kết Nối MySQL Với Java"
date: 2025-01-05
category: "java"
tags: ["Java", "MySQL", "JDBC", "Database", "Backend"]
summary: "Hướng dẫn chi tiết cách kết nối và làm việc với MySQL database trong Java sử dụng JDBC, bao gồm CRUD operations."
---

Kết nối Java với MySQL là kỹ năng cơ bản trong phát triển ứng dụng backend. Bài viết này sẽ hướng dẫn bạn từng bước.

## Chuẩn Bị

### 1. Cài Đặt MySQL

Tải và cài đặt MySQL từ [mysql.com](https://www.mysql.com/downloads/), hoặc sử dụng Docker:

```bash
docker run --name mysql-container -e MYSQL_ROOT_PASSWORD=password -d -p 3306:3306 mysql:latest
```

### 2. Thêm MySQL Connector

Thêm dependency vào `pom.xml` (Maven) hoặc `build.gradle` (Gradle):

**Maven:**

```xml
<dependency>
    <groupId>com.mysql</groupId>
    <artifactId>mysql-connector-j</artifactId>
    <version>8.0.33</version>
</dependency>
```

**Gradle:**

```gradle
implementation 'com.mysql:mysql-connector-j:8.0.33'
```

Hoặc tải JAR từ [Maven Repository](https://mvnrepository.com/artifact/com.mysql/mysql-connector-j).

## Kết Nối Cơ Bản

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;

public class MySQLConnection {
    private static final String URL = "jdbc:mysql://localhost:3306/mydatabase";
    private static final String USERNAME = "root";
    private static final String PASSWORD = "password";

    public static Connection getConnection() throws SQLException {
        return DriverManager.getConnection(URL, USERNAME, PASSWORD);
    }

    public static void main(String[] args) {
        try (Connection conn = getConnection()) {
            if (conn != null) {
                System.out.println("Kết nối MySQL thành công!");
            }
        } catch (SQLException e) {
            System.err.println("Lỗi kết nối: " + e.getMessage());
        }
    }
}
```

## Tạo Bảng

```java
import java.sql.Connection;
import java.sql.Statement;

public class CreateTable {
    public static void main(String[] args) {
        String sql = """
            CREATE TABLE IF NOT EXISTS users (
                id INT AUTO_INCREMENT PRIMARY KEY,
                name VARCHAR(100) NOT NULL,
                email VARCHAR(100) UNIQUE NOT NULL,
                age INT,
                created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
            )
        """;

        try (Connection conn = MySQLConnection.getConnection();
             Statement stmt = conn.createStatement()) {

            stmt.execute(sql);
            System.out.println("Bảng users đã được tạo!");

        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
}
```

## INSERT - Thêm Dữ Liệu

### Sử dụng Statement

```java
import java.sql.Connection;
import java.sql.Statement;

public class InsertData {
    public static void main(String[] args) {
        String sql = "INSERT INTO users (name, email, age) VALUES " +
                    "('Nguyễn Văn A', 'a@example.com', 25)";

        try (Connection conn = MySQLConnection.getConnection();
             Statement stmt = conn.createStatement()) {

            int rowsAffected = stmt.executeUpdate(sql);
            System.out.println("Đã thêm " + rowsAffected + " dòng");

        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
}
```

### Sử dụng PreparedStatement (Khuyến nghị)

```java
import java.sql.Connection;
import java.sql.PreparedStatement;

public class InsertWithPreparedStatement {
    public static void main(String[] args) {
        String sql = "INSERT INTO users (name, email, age) VALUES (?, ?, ?)";

        try (Connection conn = MySQLConnection.getConnection();
             PreparedStatement pstmt = conn.prepareStatement(sql)) {

            pstmt.setString(1, "Trần Thị B");
            pstmt.setString(2, "b@example.com");
            pstmt.setInt(3, 30);

            int rowsAffected = pstmt.executeUpdate();
            System.out.println("Đã thêm " + rowsAffected + " dòng");

        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
}
```

## SELECT - Đọc Dữ Liệu

```java
import java.sql.Connection;
import java.sql.PreparedStatement;
import java.sql.ResultSet;

public class SelectData {
    public static void main(String[] args) {
        String sql = "SELECT id, name, email, age FROM users WHERE age > ?";

        try (Connection conn = MySQLConnection.getConnection();
             PreparedStatement pstmt = conn.prepareStatement(sql)) {

            pstmt.setInt(1, 20);
            ResultSet rs = pstmt.executeQuery();

            while (rs.next()) {
                int id = rs.getInt("id");
                String name = rs.getString("name");
                String email = rs.getString("email");
                int age = rs.getInt("age");

                System.out.printf("ID: %d, Name: %s, Email: %s, Age: %d%n",
                    id, name, email, age);
            }

        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
}
```

## UPDATE - Cập Nhật Dữ Liệu

```java
import java.sql.Connection;
import java.sql.PreparedStatement;

public class UpdateData {
    public static void main(String[] args) {
        String sql = "UPDATE users SET age = ? WHERE id = ?";

        try (Connection conn = MySQLConnection.getConnection();
             PreparedStatement pstmt = conn.prepareStatement(sql)) {

            pstmt.setInt(1, 26);
            pstmt.setInt(2, 1);

            int rowsAffected = pstmt.executeUpdate();
            System.out.println("Đã cập nhật " + rowsAffected + " dòng");

        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
}
```

## DELETE - Xóa Dữ Liệu

```java
import java.sql.Connection;
import java.sql.PreparedStatement;

public class DeleteData {
    public static void main(String[] args) {
        String sql = "DELETE FROM users WHERE id = ?";

        try (Connection conn = MySQLConnection.getConnection();
             PreparedStatement pstmt = conn.prepareStatement(sql)) {

            pstmt.setInt(1, 1);

            int rowsAffected = pstmt.executeUpdate();
            System.out.println("Đã xóa " + rowsAffected + " dòng");

        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
}
```

## Connection Pool

Sử dụng HikariCP cho connection pooling:

```java
import com.zaxxer.hikari.HikariConfig;
import com.zaxxer.hikari.HikariDataSource;
import java.sql.Connection;
import java.sql.SQLException;

public class ConnectionPool {
    private static HikariDataSource dataSource;

    static {
        HikariConfig config = new HikariConfig();
        config.setJdbcUrl("jdbc:mysql://localhost:3306/mydatabase");
        config.setUsername("root");
        config.setPassword("password");
        config.setMaximumPoolSize(10);
        config.setMinimumIdle(5);

        dataSource = new HikariDataSource(config);
    }

    public static Connection getConnection() throws SQLException {
        return dataSource.getConnection();
    }

    public static void closeDataSource() {
        if (dataSource != null) {
            dataSource.close();
        }
    }
}
```

## Xử Lý Transaction

```java
import java.sql.Connection;
import java.sql.PreparedStatement;
import java.sql.SQLException;

public class TransactionExample {
    public static void transferMoney(int fromId, int toId, double amount) {
        Connection conn = null;
        try {
            conn = MySQLConnection.getConnection();
            conn.setAutoCommit(false); // Bắt đầu transaction

            // Trừ tiền từ tài khoản nguồn
            String sql1 = "UPDATE accounts SET balance = balance - ? WHERE id = ?";
            PreparedStatement pstmt1 = conn.prepareStatement(sql1);
            pstmt1.setDouble(1, amount);
            pstmt1.setInt(2, fromId);
            pstmt1.executeUpdate();

            // Cộng tiền vào tài khoản đích
            String sql2 = "UPDATE accounts SET balance = balance + ? WHERE id = ?";
            PreparedStatement pstmt2 = conn.prepareStatement(sql2);
            pstmt2.setDouble(1, amount);
            pstmt2.setInt(2, toId);
            pstmt2.executeUpdate();

            conn.commit(); // Commit transaction
            System.out.println("Chuyển tiền thành công!");

        } catch (SQLException e) {
            if (conn != null) {
                try {
                    conn.rollback(); // Rollback nếu có lỗi
                } catch (SQLException ex) {
                    ex.printStackTrace();
                }
            }
            e.printStackTrace();
        } finally {
            if (conn != null) {
                try {
                    conn.setAutoCommit(true);
                    conn.close();
                } catch (SQLException e) {
                    e.printStackTrace();
                }
            }
        }
    }
}
```

## Best Practices

1. **Luôn sử dụng PreparedStatement:** Tránh SQL injection
2. **Sử dụng try-with-resources:** Tự động đóng connection
3. **Connection pooling:** Tối ưu hiệu suất
4. **Xử lý exception đúng cách:** Log và rollback khi cần
5. **Đóng connection:** Tránh memory leak

## Kết Luận

Kết nối Java với MySQL là kỹ năng cơ bản nhưng quan trọng. Hiểu rõ JDBC giúp bạn xây dựng các ứng dụng backend mạnh mẽ và an toàn. Trong lập trình mạng, database thường được sử dụng để lưu trữ thông tin người dùng, logs, và dữ liệu ứng dụng.
