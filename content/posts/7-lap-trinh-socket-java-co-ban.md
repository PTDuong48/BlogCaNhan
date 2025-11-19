---
title: "Lập Trình Socket Java Cơ Bản"
date: 2025-01-01
category: "network"
tags: ["Java", "Socket", "TCP/IP", "Network Programming", "Server-Client"]
summary: "Hướng dẫn lập trình socket trong Java: tạo server và client, xử lý kết nối TCP, gửi/nhận dữ liệu và xử lý lỗi."
---

Socket programming là kỹ năng cốt lõi trong lập trình mạng. Bài viết này sẽ hướng dẫn bạn tạo ứng dụng client-server sử dụng Java Socket API.

## Socket Là Gì?

Socket là điểm cuối (endpoint) của kết nối hai chiều giữa hai chương trình chạy trên mạng. Java cung cấp các lớp `Socket` (client) và `ServerSocket` (server) trong package `java.net`.

## Server Socket Cơ Bản

```java
import java.net.ServerSocket;
import java.net.Socket;
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.io.PrintWriter;

public class SimpleServer {
    public static void main(String[] args) {
        int port = 12345;

        try (ServerSocket serverSocket = new ServerSocket(port)) {
            System.out.println("Server đang lắng nghe trên port " + port);

            // Chấp nhận kết nối từ client
            Socket clientSocket = serverSocket.accept();
            System.out.println("Client đã kết nối: " + clientSocket.getInetAddress());

            // Đọc dữ liệu từ client
            BufferedReader in = new BufferedReader(
                new InputStreamReader(clientSocket.getInputStream())
            );

            // Gửi dữ liệu đến client
            PrintWriter out = new PrintWriter(
                clientSocket.getOutputStream(), true
            );

            // Nhận và phản hồi
            String message = in.readLine();
            System.out.println("Nhận từ client: " + message);

            out.println("Server đã nhận: " + message);

            // Đóng kết nối
            clientSocket.close();

        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

## Client Socket Cơ Bản

```java
import java.net.Socket;
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.io.PrintWriter;

public class SimpleClient {
    public static void main(String[] args) {
        String hostname = "localhost";
        int port = 12345;

        try (Socket socket = new Socket(hostname, port)) {
            System.out.println("Đã kết nối đến server");

            // Gửi dữ liệu
            PrintWriter out = new PrintWriter(
                socket.getOutputStream(), true
            );
            out.println("Xin chào từ client!");

            // Nhận phản hồi
            BufferedReader in = new BufferedReader(
                new InputStreamReader(socket.getInputStream())
            );
            String response = in.readLine();
            System.out.println("Phản hồi từ server: " + response);

        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

## Server Đa Luồng

Server cơ bản chỉ xử lý một client tại một thời điểm. Để xử lý nhiều client, sử dụng threads:

```java
import java.net.ServerSocket;
import java.net.Socket;
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.io.PrintWriter;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;

public class MultiThreadedServer {
    private static final int PORT = 12345;
    private static final int MAX_CLIENTS = 10;

    public static void main(String[] args) {
        ExecutorService threadPool = Executors.newFixedThreadPool(MAX_CLIENTS);

        try (ServerSocket serverSocket = new ServerSocket(PORT)) {
            System.out.println("Server đang lắng nghe trên port " + PORT);

            while (true) {
                Socket clientSocket = serverSocket.accept();
                System.out.println("Client mới kết nối: " +
                    clientSocket.getInetAddress());

                // Xử lý mỗi client trong thread riêng
                threadPool.execute(new ClientHandler(clientSocket));
            }

        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            threadPool.shutdown();
        }
    }
}

class ClientHandler implements Runnable {
    private Socket clientSocket;

    public ClientHandler(Socket socket) {
        this.clientSocket = socket;
    }

    @Override
    public void run() {
        try (BufferedReader in = new BufferedReader(
                new InputStreamReader(clientSocket.getInputStream()));
             PrintWriter out = new PrintWriter(
                clientSocket.getOutputStream(), true)) {

            String inputLine;
            while ((inputLine = in.readLine()) != null) {
                System.out.println("Nhận từ client: " + inputLine);

                // Xử lý message
                String response = "Echo: " + inputLine;
                out.println(response);

                if ("quit".equalsIgnoreCase(inputLine)) {
                    break;
                }
            }

        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            try {
                clientSocket.close();
            } catch (Exception e) {
                e.printStackTrace();
            }
        }
    }
}
```

## Client Tương Tác

```java
import java.net.Socket;
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.io.PrintWriter;
import java.util.Scanner;

public class InteractiveClient {
    public static void main(String[] args) {
        String hostname = "localhost";
        int port = 12345;

        try (Socket socket = new Socket(hostname, port);
             PrintWriter out = new PrintWriter(socket.getOutputStream(), true);
             BufferedReader in = new BufferedReader(
                 new InputStreamReader(socket.getInputStream()));
             Scanner scanner = new Scanner(System.in)) {

            System.out.println("Đã kết nối đến server. Gõ 'quit' để thoát.");

            // Thread để nhận messages từ server
            Thread receiveThread = new Thread(() -> {
                try {
                    String response;
                    while ((response = in.readLine()) != null) {
                        System.out.println("Server: " + response);
                    }
                } catch (Exception e) {
                    System.out.println("Đã ngắt kết nối");
                }
            });
            receiveThread.start();

            // Gửi messages đến server
            String userInput;
            while (!(userInput = scanner.nextLine()).equals("quit")) {
                out.println(userInput);
            }

            socket.close();

        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

## Gửi/Nhận Object

Sử dụng ObjectInputStream và ObjectOutputStream:

```java
import java.io.Serializable;
import java.net.Socket;
import java.io.ObjectInputStream;
import java.io.ObjectOutputStream;

// Class phải implement Serializable
class Message implements Serializable {
    private String content;
    private String sender;
    private long timestamp;

    public Message(String content, String sender) {
        this.content = content;
        this.sender = sender;
        this.timestamp = System.currentTimeMillis();
    }

    // Getters và setters
    public String getContent() { return content; }
    public String getSender() { return sender; }
    public long getTimestamp() { return timestamp; }

    @Override
    public String toString() {
        return String.format("[%s] %s: %s",
            new java.util.Date(timestamp), sender, content);
    }
}

// Server
public class ObjectServer {
    public static void main(String[] args) {
        try (ServerSocket serverSocket = new ServerSocket(12345);
             Socket clientSocket = serverSocket.accept();
             ObjectOutputStream out = new ObjectOutputStream(
                 clientSocket.getOutputStream());
             ObjectInputStream in = new ObjectInputStream(
                 clientSocket.getInputStream())) {

            // Nhận object
            Message message = (Message) in.readObject();
            System.out.println("Nhận: " + message);

            // Gửi object
            Message response = new Message("Đã nhận", "Server");
            out.writeObject(response);

        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

## Xử Lý Lỗi và Timeout

```java
import java.net.Socket;
import java.net.ServerSocket;

public class RobustServer {
    public static void main(String[] args) {
        int port = 12345;
        int timeout = 5000; // 5 giây

        try (ServerSocket serverSocket = new ServerSocket(port)) {
            serverSocket.setSoTimeout(timeout);
            System.out.println("Server đang lắng nghe...");

            while (true) {
                try {
                    Socket clientSocket = serverSocket.accept();
                    clientSocket.setSoTimeout(10000); // Timeout cho client

                    // Xử lý client...

                } catch (java.net.SocketTimeoutException e) {
                    System.out.println("Timeout - không có client kết nối");
                    // Tiếp tục lắng nghe
                } catch (Exception e) {
                    System.err.println("Lỗi xử lý client: " + e.getMessage());
                }
            }

        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

## UDP Socket (DatagramSocket)

```java
import java.net.DatagramSocket;
import java.net.DatagramPacket;
import java.net.InetAddress;

// UDP Server
public class UDPServer {
    public static void main(String[] args) {
        int port = 12345;

        try (DatagramSocket socket = new DatagramSocket(port)) {
            byte[] buffer = new byte[1024];

            while (true) {
                DatagramPacket packet = new DatagramPacket(buffer, buffer.length);
                socket.receive(packet);

                String message = new String(packet.getData(), 0, packet.getLength());
                System.out.println("Nhận: " + message);

                // Gửi phản hồi
                InetAddress clientAddress = packet.getAddress();
                int clientPort = packet.getPort();
                String response = "Echo: " + message;
                byte[] responseBytes = response.getBytes();

                DatagramPacket responsePacket = new DatagramPacket(
                    responseBytes, responseBytes.length, clientAddress, clientPort);
                socket.send(responsePacket);
            }

        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}

// UDP Client
public class UDPClient {
    public static void main(String[] args) {
        String hostname = "localhost";
        int port = 12345;

        try (DatagramSocket socket = new DatagramSocket()) {
            String message = "Hello UDP Server";
            byte[] messageBytes = message.getBytes();

            InetAddress address = InetAddress.getByName(hostname);
            DatagramPacket packet = new DatagramPacket(
                messageBytes, messageBytes.length, address, port);
            socket.send(packet);

            // Nhận phản hồi
            byte[] buffer = new byte[1024];
            DatagramPacket response = new DatagramPacket(buffer, buffer.length);
            socket.receive(response);

            String responseMessage = new String(
                response.getData(), 0, response.getLength());
            System.out.println("Phản hồi: " + responseMessage);

        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

## Best Practices

1. **Luôn đóng socket:** Sử dụng try-with-resources
2. **Xử lý exception:** Bắt và log lỗi cụ thể
3. **Sử dụng thread pool:** Cho server đa luồng
4. **Thiết lập timeout:** Tránh chờ đợi vô hạn
5. **Validate input:** Kiểm tra dữ liệu từ client
6. **Sử dụng NIO:** Cho ứng dụng high-performance

## Kết Luận

Socket programming là nền tảng của lập trình mạng. Hiểu rõ TCP và UDP sockets giúp bạn xây dựng các ứng dụng mạng như chat applications, game servers, file transfer systems, và nhiều hơn nữa.
