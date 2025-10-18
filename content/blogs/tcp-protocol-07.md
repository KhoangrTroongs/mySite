---
title: "Giao thức TCP trong Java"
date: 2025-10-07
draft: false
description: "Tìm hiểu về giao thức TCP, cách hoạt động, handshake 3 bước, và cách sử dụng TCP trong Java."
image: "/images/blogs/tcp-protocol-new.svg"
tags: ["Java", "TCP", "Network Protocol"]
---

## TCP là gì?

TCP (Transmission Control Protocol) là một giao thức truyền thông đáng tin cậy. Nó đảm bảo rằng dữ liệu được gửi đầy đủ, đúng thứ tự và không bị lỗi.

## Đặc điểm của TCP

- **Đáng tin cậy:** Dữ liệu được gửi đầy đủ
- **Có thứ tự:** Dữ liệu được nhận theo thứ tự gửi
- **Kiểm soát luồng:** Tránh quá tải
- **Chậm hơn UDP:** Vì phải đảm bảo độ tin cậy

## Handshake 3 bước (3-Way Handshake)

Trước khi truyền dữ liệu, TCP thực hiện handshake 3 bước:

1. **SYN:** Client gửi gói SYN đến Server
2. **SYN-ACK:** Server gửi lại gói SYN-ACK
3. **ACK:** Client gửi lại gói ACK

```
Client                          Server
  |                              |
  |-------- SYN (seq=x) -------->|
  |                              |
  |<----- SYN-ACK (seq=y) -------|
  |                              |
  |-------- ACK (seq=x+1) ------>|
  |                              |
  |<--- Kết nối được thiết lập -->|
```

## Ví dụ TCP Server trong Java

```java
import java.net.ServerSocket;
import java.net.Socket;
import java.io.*;

public class TCPServer {
    public static void main(String[] args) {
        try {
            ServerSocket serverSocket = new ServerSocket(5000);
            System.out.println("TCP Server đang lắng nghe trên port 5000");
            
            while (true) {
                Socket clientSocket = serverSocket.accept();
                System.out.println("Client kết nối: " + clientSocket.getInetAddress());
                
                // Xử lý client
                BufferedReader in = new BufferedReader(
                    new InputStreamReader(clientSocket.getInputStream())
                );
                PrintWriter out = new PrintWriter(clientSocket.getOutputStream(), true);
                
                String message = in.readLine();
                System.out.println("Nhận: " + message);
                
                out.println("Server nhận được: " + message);
                clientSocket.close();
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

## Ví dụ TCP Client trong Java

```java
import java.net.Socket;
import java.io.*;

public class TCPClient {
    public static void main(String[] args) {
        try {
            Socket socket = new Socket("localhost", 5000);
            System.out.println("Kết nối đến server thành công");
            
            PrintWriter out = new PrintWriter(socket.getOutputStream(), true);
            BufferedReader in = new BufferedReader(
                new InputStreamReader(socket.getInputStream())
            );
            
            out.println("Xin chào Server!");
            String response = in.readLine();
            System.out.println("Server: " + response);
            
            socket.close();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

## Đóng kết nối (4-Way Handshake)

Khi đóng kết nối, TCP thực hiện 4 bước:

1. **FIN:** Client gửi gói FIN
2. **ACK:** Server gửi lại ACK
3. **FIN:** Server gửi gói FIN
4. **ACK:** Client gửi lại ACK

## Khi nào sử dụng TCP?

- Email (SMTP, POP3)
- Web (HTTP, HTTPS)
- FTP (File Transfer)
- SSH (Secure Shell)
- Bất kỳ ứng dụng nào cần độ tin cậy cao

## Kết luận

TCP là giao thức quan trọng cho các ứng dụng cần độ tin cậy cao. Hiểu biết về TCP sẽ giúp bạn xây dựng các ứng dụng mạng mạnh mẽ!

