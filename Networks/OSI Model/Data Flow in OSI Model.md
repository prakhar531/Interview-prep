# OSI Model

## Flow of Data in OSI Model

When we transfer information from one device to another, it travels through 7 layers of OSI model. First data travels down through 7 layers from the sender’s end and then climbs back 7 layers on the receiver’s end.

Let’s look at it with an Example:

Luffy sends an e-mail to his friend Zoro.

**Step 1:** Luffy interacts with e-mail application like Gmail, outlook, etc. Writes his email to send. (This happens in **Layer 7: Application layer**)

**Step 2:** Mail application prepares for data transmission like encrypting data and formatting it for transmission. (This happens in **Layer 6: Presentation Layer**)

**Step 3:** There is a connection established between the sender and receiver on the internet. (This happens in **Layer 5: Session Layer**)

**Step 4:** Email data is broken into smaller **segments**. It adds sequence number and error-checking information to maintain the reliability of the information. (This happens in **Layer 4: Transport Layer**)

**Step 5:** Addressing of **packets** is done in order to find the best route for transfer.The sender & receiver’s IP addresses are placed in the header by the network layer (This happens in **Layer 3: Network Layer**)

**Step 6:** Data packets are encapsulated into **frames**, then MAC address is added for local devices and then it checks for error using error detection. (This happens in **Layer 2: Data Link Layer**)

**Step 7:** Lastly Frames are transmitted in the form of electrical/ optical signals over a physical network medium like ethernet cable or WiFi.

After the email reaches the receiver i.e. Zoro, the process will reverse and decrypt the e-mail content. At last, the email will be shown on Zoro’s email client.

## OSI Model in a Nutshell

![alt text](<Screenshot (135).png>)
![alt text](<Screenshot (136).png>) ![alt text](<Screenshot (135)-1.png>)

## OSI vs TCP/IP Model

Some key differences between the OSI model and the TCP/IP Model are:

1. TCP/IP model consists of 4 layers but OSI model has 7 layers. Layers 5,6,7 of the OSI model are combined into the Application Layer of TCP/IP model and OSI layers 1 and 2 are combined into Network Access Layers of TCP/IP protocol.
2. The TCP/IP model is older than the OSI model, hence it is a foundational protocol that defines how should data be transferred online.
3. Compared to the OSI model, the TCP/IP model has less strict layer boundaries.
4. All layers of the TCP/IP model are needed for data transmission but in the OSI model, some applications can skip certain layers. Only layers 1,2 and 3 of the OSI model are necessary for data transmission.
