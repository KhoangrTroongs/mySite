---
title: "Thực hành: Xây dựng ứng dụng Chat với TCP và UDP"
date: 2025-10-09
draft: false
description: "Hướng dẫn xây dựng ứng dụng chat đơn giản sử dụng TCP và UDP, bao gồm server, client và xử lý đa kết nối."
image: "/images/blogs/chat-app.svg"
tags: ["Java", "Chat", "TCP", "UDP", "Practice"]
---

## Giới thiệu

Trong bài này, chúng ta sẽ xây dựng một ứng dụng chat đơn giản sử dụng TCP. Ứng dụng này cho phép nhiều client kết nối đến server và gửi tin nhắn cho nhau.

## Kiến trúc ứng dụng

```
Client 1 ----\
              \
Client 2 ---- Server ---- Broadcast tin nhắn
              /
Client 3 ----/
```

## Server Chat (TCP)

```java
import java.net.*;
import java.io.*;
import java.util.*;

public class ChatServer {
    private static List<ClientHandler> clients = new ArrayList<>();
    
    public static void main(String[] args) {
        try {
            ServerSocket serverSocket = new ServerSocket(5000);
            System.out.println("Chat Server đang chạy trên port 5000");
            
            while (true) {
                Socket clientSocket = serverSocket.accept();
                System.out.println("Client mới kết nối: " + clientSocket.getInetAddress());
                
                ClientHandler handler = new ClientHandler(clientSocket);
                clients.add(handler);
                new Thread(handler).start();
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
    
    public static void broadcast(String message, ClientHandler sender) {
        for (ClientHandler client : clients) {
            if (client != sender) {
                client.sendMessage(message);
            }
        }
    }
    
    public static void removeClient(ClientHandler client) {
        clients.remove(client);
    }
}
```

## ClientHandler

```java
import java.net.*;
import java.io.*;

public class ClientHandler implements Runnable {
    private Socket socket;
    private PrintWriter out;
    private BufferedReader in;
    private String username;
    
    public ClientHandler(Socket socket) {
        this.socket = socket;
    }
    
    @Override
    public void run() {
        try {
            out = new PrintWriter(socket.getOutputStream(), true);
            in = new BufferedReader(new InputStreamReader(socket.getInputStream()));
            
            out.println("Nhập tên của bạn:");
            username = in.readLine();
            System.out.println(username + " đã tham gia");
            
            String message;
            while ((message = in.readLine()) != null) {
                System.out.println(username + ": " + message);
                ChatServer.broadcast(username + ": " + message, this);
            }
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            try {
                socket.close();
                ChatServer.removeClient(this);
                System.out.println(username + " đã rời đi");
            } catch (Exception e) {
                e.printStackTrace();
            }
        }
    }
    
    public void sendMessage(String message) {
        out.println(message);
    }
}
```

## Client Chat

```java
import java.net.*;
import java.io.*;
import java.util.Scanner;

public class ChatClient {
    public static void main(String[] args) {
        try {
            Socket socket = new Socket("localhost", 5000);
            
            PrintWriter out = new PrintWriter(socket.getOutputStream(), true);
            BufferedReader in = new BufferedReader(
                new InputStreamReader(socket.getInputStream())
            );
            
            // Thread để nhận tin nhắn
            new Thread(() -> {
                try {
                    String message;
                    while ((message = in.readLine()) != null) {
                        System.out.println(message);
                    }
                } catch (Exception e) {
                    e.printStackTrace();
                }
            }).start();
            
            // Gửi tin nhắn
            Scanner scanner = new Scanner(System.in);
            String message;
            while ((message = scanner.nextLine()) != null) {
                out.println(message);
            }
            
            socket.close();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

## Chạy ứng dụng

1. **Khởi động Server:**
```bash
javac ChatServer.java ClientHandler.java
java ChatServer
```

2. **Khởi động Client (mở nhiều terminal):**
```bash
javac ChatClient.java
java ChatClient
```

## Cải tiến có thể thêm

- Lưu lịch sử chat vào file
- Thêm tính năng private message
- Thêm tính năng room chat
- Sử dụng UDP cho tin nhắn nhanh
- Thêm giao diện GUI

## Kết luận

Xây dựng ứng dụng chat là một cách tuyệt vời để thực hành các kỹ năng mạng trong Java. Bạn có thể mở rộng ứng dụng này với nhiều tính năng thú vị!

