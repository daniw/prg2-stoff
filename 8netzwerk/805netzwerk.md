### Sie können einfache Java TCP- und UPD-Client/Server-Programme analysieren und implementieren

---

[Zurück](800netzwerk.md)

#### TCP Server

```java
package twice;

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.io.PrintWriter;
import java.net.ServerSocket;
import java.net.Socket;

public class TwiceServer {
	
	public static void main(String[] args) throws IOException{
	
		int port = 6789;
		ServerSocket s = new ServerSocket(port);
		boolean state = true;
		
		String inputLine;
		
		while(state) {
			System.out.println("Starting twice-Server at port " + port);
			System.out.println("Wait for client...");
			Socket client = s.accept();
			System.out.println("Connected to client!");
			
			PrintWriter outStream = new PrintWriter(client.getOutputStream());
			BufferedReader inStream = 
					new BufferedReader(
							new InputStreamReader(client.getInputStream())
					);
			
			try{
				outStream.println("What's your number?");
				outStream.flush();
				inputLine = inStream.readLine();
				
				if(inputLine.equals("END")) {
					outStream.println("terminating service...");
					System.out.println("termination by client");
					state = false;
				}
				else {
					int value = Integer.parseInt(inputLine);
					outStream.println(value*2 + " is twice your number");
				}
			}
			
			catch (Exception ex) {
				outStream.println("Error: " + ex.getMessage());
			}
			
			finally {
				outStream.flush();
				client.close();
			}
			
		}
		
		System.exit(0);
	
	}
}
```

#### TCP Client

```java
package twice;

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.io.PrintWriter;
import java.net.Socket;

public class TwiceClient {
	
	public static void main(String[] args) throws IOException{
		
		int port = 6789;
		String host = "127.0.0.1";
		
		boolean state = true;
		
		BufferedReader keyStream = new BufferedReader(new InputStreamReader(System.in));
		
		while(state){
			Socket client = new Socket(host, port);
			PrintWriter outStream = 
					new PrintWriter(client.getOutputStream());
			BufferedReader inStream = 
					new BufferedReader(
							new InputStreamReader(client.getInputStream())
					);
			
			System.out.println(inStream.readLine());
			String line = keyStream.readLine();
			
			if(line.equals("END")) {
				state = false;
				outStream.println(line);
				outStream.flush();
				client.close();
			}
			else {
				state = true;
				outStream.println(line);
				outStream.flush();
				line = inStream.readLine();
				System.out.println(line);
				client.close();
			}
			
		}
		
		System.exit(0);
	}
	
}
```

---
