---
title: "Xử Lý Mạng Cơ Bản Trong Java"
date: 2025-01-10
category: "network"
tags: ["Java", "Network", "Socket", "HTTP", "TCP/IP"]
summary: "Học cách sử dụng các lớp java.net để xử lý kết nối mạng, URL, HTTP requests và responses trong Java."
---

Java cung cấp package `java.net` với các lớp mạnh mẽ để xử lý mạng. Hãy cùng khám phá các khái niệm cơ bản về lập trình mạng trong Java.

## Làm Việc Với URL

Lớp `URL` cho phép bạn làm việc với địa chỉ web:

```java
import java.net.URL;
import java.io.BufferedReader;
import java.io.InputStreamReader;

public class URLExample {
    public static void main(String[] args) {
        try {
            URL url = new URL("https://api.example.com/data");
            BufferedReader reader = new BufferedReader(
                new InputStreamReader(url.openStream())
            );

            String line;
            while ((line = reader.readLine()) != null) {
                System.out.println(line);
            }
            reader.close();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

## HTTP GET Request

Sử dụng `HttpURLConnection` để gửi HTTP requests:

```java
import java.net.HttpURLConnection;
import java.net.URL;
import java.io.BufferedReader;
import java.io.InputStreamReader;

public class HttpGetExample {
    public static void main(String[] args) {
        try {
            URL url = new URL("https://jsonplaceholder.typicode.com/posts/1");
            HttpURLConnection conn = (HttpURLConnection) url.openConnection();
            conn.setRequestMethod("GET");
            conn.setRequestProperty("Accept", "application/json");

            int responseCode = conn.getResponseCode();
            System.out.println("Response Code: " + responseCode);

            if (responseCode == 200) {
                BufferedReader in = new BufferedReader(
                    new InputStreamReader(conn.getInputStream())
                );
                String inputLine;
                StringBuilder response = new StringBuilder();

                while ((inputLine = in.readLine()) != null) {
                    response.append(inputLine);
                }
                in.close();

                System.out.println("Response: " + response.toString());
            } else {
                System.out.println("GET request failed");
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

## HTTP POST Request

Gửi dữ liệu với POST request:

```java
import java.net.HttpURLConnection;
import java.net.URL;
import java.io.OutputStream;
import java.io.BufferedReader;
import java.io.InputStreamReader;

public class HttpPostExample {
    public static void main(String[] args) {
        try {
            URL url = new URL("https://jsonplaceholder.typicode.com/posts");
            HttpURLConnection conn = (HttpURLConnection) url.openConnection();
            conn.setRequestMethod("POST");
            conn.setRequestProperty("Content-Type", "application/json");
            conn.setDoOutput(true);

            String jsonInputString = "{\"title\": \"Test\", \"body\": \"Content\", \"userId\": 1}";

            try (OutputStream os = conn.getOutputStream()) {
                byte[] input = jsonInputString.getBytes("utf-8");
                os.write(input, 0, input.length);
            }

            int responseCode = conn.getResponseCode();
            System.out.println("POST Response Code: " + responseCode);

            if (responseCode == 201) {
                BufferedReader in = new BufferedReader(
                    new InputStreamReader(conn.getInputStream())
                );
                String inputLine;
                StringBuilder response = new StringBuilder();

                while ((inputLine = in.readLine()) != null) {
                    response.append(inputLine);
                }
                in.close();

                System.out.println("Response: " + response.toString());
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

## InetAddress - Làm Việc Với IP

Lớp `InetAddress` giúp làm việc với địa chỉ IP:

```java
import java.net.InetAddress;

public class InetAddressExample {
    public static void main(String[] args) {
        try {
            // Lấy địa chỉ IP từ hostname
            InetAddress address = InetAddress.getByName("www.google.com");
            System.out.println("Host Name: " + address.getHostName());
            System.out.println("IP Address: " + address.getHostAddress());

            // Lấy địa chỉ localhost
            InetAddress localhost = InetAddress.getLocalHost();
            System.out.println("Localhost: " + localhost.getHostAddress());

            // Kiểm tra kết nối
            boolean reachable = address.isReachable(5000);
            System.out.println("Reachable: " + reachable);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

## URLConnection với Timeout

Thiết lập timeout cho kết nối:

```java
import java.net.URL;
import java.net.URLConnection;

public class URLConnectionTimeout {
    public static void main(String[] args) {
        try {
            URL url = new URL("https://api.example.com/data");
            URLConnection conn = url.openConnection();

            // Thiết lập timeout (milliseconds)
            conn.setConnectTimeout(5000);  // 5 giây
            conn.setReadTimeout(10000);      // 10 giây

            conn.connect();
            System.out.println("Connected successfully");
        } catch (Exception e) {
            System.err.println("Connection failed: " + e.getMessage());
        }
    }
}
```

## Xử Lý Lỗi Mạng

Luôn xử lý các exception khi làm việc với mạng:

```java
import java.net.URL;
import java.net.UnknownHostException;
import java.net.SocketTimeoutException;
import java.io.IOException;

public class NetworkErrorHandling {
    public static void fetchData(String urlString) {
        try {
            URL url = new URL(urlString);
            // Xử lý kết nối...
        } catch (UnknownHostException e) {
            System.err.println("Không thể tìm thấy host: " + e.getMessage());
        } catch (SocketTimeoutException e) {
            System.err.println("Kết nối quá thời gian chờ: " + e.getMessage());
        } catch (IOException e) {
            System.err.println("Lỗi I/O: " + e.getMessage());
        } catch (Exception e) {
            System.err.println("Lỗi không xác định: " + e.getMessage());
        }
    }
}
```

## Best Practices

1. **Luôn đóng kết nối:** Sử dụng try-with-resources
2. **Thiết lập timeout:** Tránh chờ đợi vô hạn
3. **Xử lý exception:** Bắt và xử lý các lỗi cụ thể
4. **Sử dụng thread pool:** Cho các request đồng thời
5. **Cache kết nối:** Tái sử dụng HttpURLConnection khi có thể

## Kết Luận

Package `java.net` cung cấp các công cụ mạnh mẽ cho lập trình mạng. Hiểu rõ các lớp cơ bản này là nền tảng để phát triển các ứng dụng mạng phức tạp hơn như socket programming, RESTful APIs, và microservices.
