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
}
<!---
MNGRUOP/MNGRUOP is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
