---
title: "Quản lý Kết nối Mạng trong Java"
date: 2025-10-06
draft: false
description: "Hướng dẫn sử dụng InetAddress, Socket, ServerSocket để quản lý kết nối mạng trong Java."
image: "/images/blogs/network-address-new.svg"
tags: ["Java", "Network", "Socket"]
---

## InetAddress

InetAddress được sử dụng để đại diện cho một địa chỉ IP.

```java
import java.net.InetAddress;

public class InetAddressExample {
    public static void main(String[] args) {
        try {
            // Lấy địa chỉ IP của localhost
            InetAddress localhost = InetAddress.getLocalHost();
            System.out.println("Hostname: " + localhost.getHostName());
            System.out.println("IP Address: " + localhost.getHostAddress());
            
            // Lấy địa chỉ IP từ hostname
            InetAddress google = InetAddress.getByName("google.com");
            System.out.println("Google IP: " + google.getHostAddress());
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

## Socket

Socket được sử dụng để tạo kết nối giữa client và server.

### Client Socket

```java
import java.net.Socket;
import java.io.*;

public class ClientSocket {
    public static void main(String[] args) {
        try {
            // Kết nối đến server
            Socket socket = new Socket("localhost", 5000);
            
            // Gửi dữ liệu
            PrintWriter out = new PrintWriter(socket.getOutputStream(), true);
            out.println("Xin chào Server!");
            
            // Nhận dữ liệu
            BufferedReader in = new BufferedReader(
                new InputStreamReader(socket.getInputStream())
            );
            String response = in.readLine();
            System.out.println("Server: " + response);
            
            socket.close();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

## ServerSocket

ServerSocket được sử dụng để tạo một server lắng nghe các kết nối từ client.

```java
import java.net.ServerSocket;
import java.net.Socket;
import java.io.*;

public class ServerSocketExample {
    public static void main(String[] args) {
        try {
            // Tạo server lắng nghe trên port 5000
            ServerSocket serverSocket = new ServerSocket(5000);
            System.out.println("Server đang chờ kết nối...");
            
            // Chấp nhận kết nối từ client
            Socket clientSocket = serverSocket.accept();
            System.out.println("Client kết nối!");
            
            // Nhận dữ liệu từ client
            BufferedReader in = new BufferedReader(
                new InputStreamReader(clientSocket.getInputStream())
            );
            String message = in.readLine();
            System.out.println("Client: " + message);
            
            // Gửi dữ liệu cho client
            PrintWriter out = new PrintWriter(clientSocket.getOutputStream(), true);
            out.println("Xin chào Client!");
            
            clientSocket.close();
            serverSocket.close();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

## Server đa kết nối

Để xử lý nhiều client cùng lúc, sử dụng threads:

```java
public class MultiClientServer {
    public static void main(String[] args) {
        try {
            ServerSocket serverSocket = new ServerSocket(5000);
            System.out.println("Server đang chờ kết nối...");
            
            while (true) {
                Socket clientSocket = serverSocket.accept();
                // Tạo thread mới cho mỗi client
                new Thread(new ClientHandler(clientSocket)).start();
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}

class ClientHandler implements Runnable {
    private Socket socket;
    
    public ClientHandler(Socket socket) {
        this.socket = socket;
    }
    
    @Override
    public void run() {
        try {
            BufferedReader in = new BufferedReader(
                new InputStreamReader(socket.getInputStream())
            );
            String message = in.readLine();
            System.out.println("Client: " + message);
            socket.close();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

## Kết luận

Hiểu biết về Socket và ServerSocket là nền tảng để xây dựng các ứng dụng mạng trong Java!

