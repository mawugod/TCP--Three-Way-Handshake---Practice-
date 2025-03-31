# TCP Three-Way Handshake In Practice

## Tools:
**Netcat(nc)** – It’s a utility for reading/writing data across network connections. This acts as both server and client in this demonstration
**Tcpdump** - It’s a packet capture tool for monitoring network traffic.

## Visual Representation:
![image](https://github.com/user-attachments/assets/e4131118-cabb-461c-98c4-ddcd19a06b0f)  

## Set Up:
**Environment** : This was demonstrated using a single Ubuntu VM acting as both server and client.
Below, you can see the ‘’nc’ is used as a server listening on the 0.0.0.0 address.

## Graphics
**Server** :  
![image](https://github.com/user-attachments/assets/96c3eca9-a6b8-445e-9f7c-9e3a40f59e13)  


**Client** :  
![image](https://github.com/user-attachments/assets/ba6536be-f0cd-4dfb-be34-93af4ba0ba41)  

**Network Capture** :  
![image](https://github.com/user-attachments/assets/a971fe67-0115-408c-bf8c-8d5b0315ce5a)  

## Procedure

1.	The server first opens a connection to listen to a client intending to communicate.
  a.	Command: nc –ivp 5050 
    i.	–i: Listen mode
    ii.	–v: Verbose output
    iii.	–p 5050: Indicating the specific port 

  b.	Hit the Enter key

2. In a separate terminal, the network capture tool ‘tcpdump’ is set ready to capture traffic with the command:
    a.	sudo tcpdump –i lo 
      i.	 ‘-i’ argument is to enable an interface to be set up
      ii.	‘lo’ is the loopback interface being set up.
  b.	Hit the Enter key
  
**NB:** Ephemeral port: which is a temporary and dynamic port numbers assigned by the client’s OS and used by its applications to communicate with the server in this case was ‘60118’ as identified from the server.  
![image](https://github.com/user-attachments/assets/f54a1264-c931-4afe-8ef3-4a1fff47db72)  

3.	In another terminal, client connects to the server with the command:
    a.	tcpdump 127.0.0.1 5050
    b.	Hit the Enter key

Switch to Server terminal; you will realize that whatever you have entered appears at there.  
If you should type at the server terminal and switch back to the client, you will still see what was being typed.  
In all there is a communication taking place.  
Let’s see how the ‘tcpdump’ tool captured the conversation and how the implementaion of the three-way handshake took place.  

## Three-Way Handshake Analysis

1. The client sends a SYN (S) flag with a sequence number (3136640809) as indicated in the image below.
   ![image](https://github.com/user-attachments/assets/9c6d2516-09d5-4713-adda-a95dcf13ac63)  

2. The Server then responds with a SYN/ACK (S.) where the ACK is an increment by one of the initial sequence number:  
Acknowledgment number = client’s sequence number + 1 (3136640810); now a new server sequence number.
![image](https://github.com/user-attachments/assets/88d3bbdd-e8c8-47b8-b241-1988f0ad0368)  

3. The Client sends an acknowledgement (ACK) confirming the connection.  
As the result, a reliable TCP connection is established. 
It continuous with the PUSH (P) flag indicating urgent data transmission, and being acknowledged ack (.) => [P.].  
![image](https://github.com/user-attachments/assets/621b5c47-3f37-4b69-a66a-fde9d2dce7c5)  

 
Connection termination: The FIN (F) flag indicates the connection has been terminated and it is followed by ACK (.).  
![image](https://github.com/user-attachments/assets/33528a53-1696-4458-9e3d-a79edd45e7b7)


