---
title: "Giao thức UDP trong Java"
date: 2025-10-08
draft: false
description: "Tìm hiểu về giao thức UDP, sự khác biệt với TCP, và cách sử dụng UDP trong Java."
image: "/images/blogs/udp-protocol.svg"
tags: ["Java", "UDP", "Network Protocol"]
---

## UDP là gì?

UDP (User Datagram Protocol) là một giao thức truyền thông không đáng tin cậy nhưng nhanh. Nó không đảm bảo dữ liệu được gửi đầy đủ hoặc đúng thứ tự, nhưng nó rất nhanh.

## So sánh TCP và UDP

| Tiêu chí | TCP | UDP |
|---------|-----|-----|
| Đáng tin cậy | Có | Không |
| Tốc độ | Chậm | Nhanh |
| Kết nối | Có | Không |
| Handshake | Có (3 bước) | Không |
| Sử dụng | Email, Web, FTP | Video, Game, DNS |

## Đặc điểm của UDP

- **Nhanh:** Không cần thiết lập kết nối
- **Không đáng tin cậy:** Có thể mất dữ liệu
- **Không có thứ tự:** Dữ liệu có thể đến không theo thứ tự
- **Overhead thấp:** Ít thông tin header

## Ví dụ UDP Server trong Java

```java
import java.net.DatagramSocket;
import java.net.DatagramPacket;
import java.net.InetAddress;

public class UDPServer {
    public static void main(String[] args) {
        try {
            DatagramSocket socket = new DatagramSocket(5000);
            System.out.println("UDP Server đang lắng nghe trên port 5000");
            
            byte[] receiveData = new byte[1024];
            DatagramPacket receivePacket = new DatagramPacket(receiveData, receiveData.length);
            
            socket.receive(receivePacket);
            String message = new String(receivePacket.getData(), 0, receivePacket.getLength());
            System.out.println("Nhận: " + message);
            
            InetAddress clientAddress = receivePacket.getAddress();
            int clientPort = receivePacket.getPort();
            
            String response = "Server nhận được: " + message;
            byte[] sendData = response.getBytes();
            DatagramPacket sendPacket = new DatagramPacket(
                sendData, sendData.length, clientAddress, clientPort
            );
            socket.send(sendPacket);
            
            socket.close();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

## Ví dụ UDP Client trong Java

```java
import java.net.DatagramSocket;
import java.net.DatagramPacket;
import java.net.InetAddress;

public class UDPClient {
    public static void main(String[] args) {
        try {
            DatagramSocket socket = new DatagramSocket();
            
            String message = "Xin chào Server!";
            byte[] sendData = message.getBytes();
            
            InetAddress serverAddress = InetAddress.getByName("localhost");
            DatagramPacket sendPacket = new DatagramPacket(
                sendData, sendData.length, serverAddress, 5000
            );
            socket.send(sendPacket);
            System.out.println("Gửi: " + message);
            
            byte[] receiveData = new byte[1024];
            DatagramPacket receivePacket = new DatagramPacket(receiveData, receiveData.length);
            socket.receive(receivePacket);
            
            String response = new String(receivePacket.getData(), 0, receivePacket.getLength());
            System.out.println("Server: " + response);
            
            socket.close();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

## Khi nào sử dụng UDP?

- **Video Streaming:** Tốc độ quan trọng hơn độ tin cậy
- **Online Games:** Cần phản ứng nhanh
- **DNS:** Truy vấn nhanh
- **VoIP:** Cuộc gọi thời gian thực
- **IoT:** Thiết bị có tài nguyên hạn chế

## Kết luận

UDP là lựa chọn tốt khi tốc độ quan trọng hơn độ tin cậy. Hiểu biết về UDP sẽ giúp bạn xây dựng các ứng dụng thời gian thực!

