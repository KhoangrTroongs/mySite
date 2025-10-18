---
title: "Thực hành Java: Xây dựng trò chơi Caro"
date: 2025-10-03
draft: false
description: "Hướng dẫn xây dựng trò chơi Caro từ đầu, bao gồm khởi tạo bàn cờ, xử lý nước đi và kiểm tra thắng/thua."
image: "/images/blogs/caro-game-new.svg"
tags: ["Java", "Game", "Practice"]
---

## Giới thiệu về trò chơi Caro

Caro là một trò chơi cổ điển nơi hai người chơi lần lượt đặt các ký hiệu (X và O) trên một bàn cờ. Người chơi nào đặt được 5 ký hiệu liên tiếp (ngang, dọc hoặc chéo) sẽ thắng.

## Cấu trúc chương trình

### 1. Khởi tạo bàn cờ

```java
public class CaroGame {
    private char[][] board;
    private int size = 15;
    
    public CaroGame() {
        board = new char[size][size];
        initBoard();
    }
    
    private void initBoard() {
        for (int i = 0; i < size; i++) {
            for (int j = 0; j < size; j++) {
                board[i][j] = '.';
            }
        }
    }
}
```

### 2. Hiển thị bàn cờ

```java
public void displayBoard() {
    for (int i = 0; i < size; i++) {
        for (int j = 0; j < size; j++) {
            System.out.print(board[i][j] + " ");
        }
        System.out.println();
    }
}
```

### 3. Xử lý nước đi

```java
public boolean makeMove(int row, int col, char player) {
    if (row < 0 || row >= size || col < 0 || col >= size) {
        return false;
    }
    if (board[row][col] != '.') {
        return false;
    }
    board[row][col] = player;
    return true;
}
```

### 4. Kiểm tra thắng

```java
public boolean checkWin(int row, int col, char player) {
    // Kiểm tra ngang
    if (checkDirection(row, col, player, 0, 1)) return true;
    // Kiểm tra dọc
    if (checkDirection(row, col, player, 1, 0)) return true;
    // Kiểm tra chéo
    if (checkDirection(row, col, player, 1, 1)) return true;
    if (checkDirection(row, col, player, 1, -1)) return true;
    return false;
}

private boolean checkDirection(int row, int col, char player, int dRow, int dCol) {
    int count = 1;
    // Kiểm tra một hướng
    for (int i = 1; i < 5; i++) {
        int newRow = row + i * dRow;
        int newCol = col + i * dCol;
        if (newRow < 0 || newRow >= size || newCol < 0 || newCol >= size) break;
        if (board[newRow][newCol] == player) count++;
        else break;
    }
    // Kiểm tra hướng ngược lại
    for (int i = 1; i < 5; i++) {
        int newRow = row - i * dRow;
        int newCol = col - i * dCol;
        if (newRow < 0 || newRow >= size || newCol < 0 || newCol >= size) break;
        if (board[newRow][newCol] == player) count++;
        else break;
    }
    return count >= 5;
}
```

## Vòng lặp chính

```java
public void play() {
    char currentPlayer = 'X';
    while (true) {
        displayBoard();
        System.out.println("Lượt của người chơi: " + currentPlayer);
        // Nhập nước đi từ người dùng
        // ...
        if (checkWin(row, col, currentPlayer)) {
            System.out.println("Người chơi " + currentPlayer + " thắng!");
            break;
        }
        currentPlayer = (currentPlayer == 'X') ? 'O' : 'X';
    }
}
```

## Kết luận

Xây dựng trò chơi Caro là một cách tuyệt vời để thực hành các kỹ năng Java cơ bản như mảng 2D, vòng lặp và logic kiểm tra!

