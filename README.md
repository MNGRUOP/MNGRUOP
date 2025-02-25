import java.io.DataOutputStream;
import java.io.IOException;
import java.net.Socket;

public class Sender {
    private Socket socket;
    private DataOutputStream outputStream;

    public Sender(String address, int port) throws IOException {
        socket = new Socket(address, port);
        outputStream = new DataOutputStream(socket.getOutputStream());
    }

    public void sendMessage(String message) throws IOException {
        outputStream.writeUTF(message);
        outputStream.flush();
    }

    public void close() throws IOException {
        outputStream.close();
        socket.close();
    }

    public static void main(String[] args) {
        try {
            Sender sender = new Sender("127.0.0.1", 5000);
            sender.sendMessage("Hello, this is a test message.");
            sender.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }


import java.io.DataInputStream;
import java.io.IOException;
import java.net.ServerSocket;
import java.net.Socket;

public class Receiver {
    private ServerSocket serverSocket;
    private Socket socket;
    private DataInputStream inputStream;

    public Receiver(int port) throws IOException {
        serverSocket = new ServerSocket(port);
        socket = serverSocket.accept();
        inputStream = new DataInputStream(socket.getInputStream());
    }

    public String receiveMessage() throws IOException {
        return inputStream.readUTF();
    }

    public void close() throws IOException {
        inputStream.close();
        socket.close();
        serverSocket.close();
    }

    public static void main(String[] args) {
        try {
            Receiver receiver = new Receiver(5000);
            System.out.println("Received message: " + receiver.receiveMessage());
            receiver.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }

}

<!---
MNGRUOP/MNGRUOP is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
