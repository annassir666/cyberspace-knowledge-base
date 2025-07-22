#networks #OSI #models

![[osi1.png]]


Explanation of each step:

Mnemonic to know from 1 to 7: **P**lease **D**o **N**ot **T**hrow **S**pinach **P**izza **A**way

1. Physical: data in bits, electrical signals, and radio such as wifi radio bands 4,5,6 GHz
    
2. Data Link: How different nodes/devices exchange information in the same network segment. Examples of layer 2 include Ethernet, i.e., 802.3, and WiFi, i.e., 802.11. Ethernet and WiFi addresses are six bytes. Their address is called a MAC address
    
3. Network: Sending data between different network segments. In more technical terms, the network layer handles logical addressing and routing, i.e., finding a path to transfer the network packets between the diverse networks. In the data link layer, we discussed a company office with ten computers connected to each other. With multiple offices across different locations, the network layer is responsible for connecting these offices.
    
4. Transport: enables end-to-end communication between running applications on different hosts. Examples of layer 4 are Transmission Control Protocol (TCP) and User Datagram Protocol (UDP).
    
5. Session: responsible for establishing, maintaining, and synchronising communication between applications running on different hosts. Establishing a session means initiating communication between applications and negotiating the necessary parameters for the session. Data synchronisation ensures that data is transmitted in the correct order and provides mechanisms for recovery in case of transmission failures. Examples of the session layer are Network File System (NFS) and Remote Procedure Call (RPC).
    
6. Presentation: ensures the data is delivered in a form the application layer can understand. handles data encoding, compression, and encryption. An example of encoding is character encoding, such as ASCII or Unicode.
    
7. Application: provides network services directly to end-user applications. Your web browser would use the HTTP protocol to request a file, submit a form, or upload a file. Examples of Layer 7 protocols are HTTP, FTP, DNS, POP3, SMTP, and IMAP.

![[Screenshot 2024-12-05 at 15.24.50.png]]