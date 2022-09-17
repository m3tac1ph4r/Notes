# Open System Interconnections(OSI) Model :

It is a network architecture model based on the ISO standards. It is called the OSI model as it deals with connecting the systems that are open for communication with other systems. _The OSI model has seven layers_.

### Seven Layers of OSI Model :

**1. Application Layer :**

- Application layer enables the user to access the network.
- It is the topmost layer of the OSI model.
- Application layer protocol are file transfer protocol, simple mail transfer protocol, etc.
- The most widely used application layer protocol is HTTP. A user sends the request for the web page using HTTP.

**HTTP**
![[http_desc.png]]
_Non persistent_ means we have to do the task again if connection lost. For ex: If you login in bank and do some task. Then close the tab, and if you again opened the website then you have to relogin.
But in case of _Persisitent_ if connection is lost then also it will be saved. For example if you login in the GMAIL and close the connection. But if you opened GMAIL another day you don't have to login.

![[ftp_desc.png]]

![[smtp_pop_desc.png]]

**2. Presentation Layer :**

- The presentation layer is also known as a Translation Layer as it tranlates the data from one format to another format.
- At the sender side, this layer translates the data format used by the application layer to the common format and at reciever side, this layer translates the common format into a format used by the application layer.
- **Functions of Presentation Layer :**
  - Character code translation
  - Data conversion
  - Data compression
  - Data encryption

**3. Session layer :**

- The main responsibility of the session layer is beginning, maintaining and ending the communication between the devices.
- Session layer also reports the error coming from the upper layers.
- Session layer establishes and maintains the session between two users.

**4. Transport Layer :**

- It delivers the message through the network and provides error checking so that no error occur during the transfer of data.
- It provides two kinds of services :
  - **Connection-oriented transmission :** In this transmission, the receiver sends the acknowledgement to the sender after the packet has been received. Ex : TCP
  - **Connectionless transmission :** In this transmission, the receiver does not send the acknowledgement to the sender. Ex : UDP
- Protocol Used : TCP and UDP

**5. Network Layer :**

- Network layer converts the logical address into the physical address.
- The routing concept means it determines the best route for the packet to travel from source to the destination.

- **Function of network layer :**
  - **Routing :** The network layer determines the best route from source to destination. This function is known as routing.
  - **Logical Addressing :** The network layer defines the addressing scheme to identify each device uniquely.
  - **Packetizing :** The network layer receives the data from the upper layer and converts the data into packets. This process is known as packetizing.
  - **Fragementation :** It is a process of dividing the data into fragments.

**6. Data Link Layer :**
**1. Physical Layer :**

- It is the lowest layer of the OSI model
- It is used for the trasmission of an unstructured raw bit stream over a physical medium.
- Physical layer transmits the data either in the form of electrical/optical or mechanical form
- The Physical layer is mainly used for the physical connection between the device and such physical connection can be made by using twisted-pair cable, fibre-optic or wireless transmission media.

**2. Data Link Layer :**

- It is used for transferring the data from one node to another node.
- It receives the data from the network layer and converts the data into data frames and then attaches the physical address to these frames which are sent to the physical layer.
- It enables error free transfer of data from one node to another node.

- **Function of Data Link Layer :**
  - **Frame Synchronization :** Data-link layer converts the data into frames, and it ensures that the destination must recognize the starting and ending of each frame.
  - **Addressing :** Data-link layers attach the physical address with the data frames so that the individual machines can be easily identified.
  - **Link Management :** Data-link layer manages the initiation, maintainence and termination of the link between the source and destination for the effective exchange of data.

 **Significance of data link layer :**

- The data link layer is in charge of delivering data between two network nodes that are directly connected.
- The data link layer uses a physical address for the unique identification of each device on a local network.
- The data link layer splits packet from the network layer known as frames and adds a header(in which physical address of source and destination ) and a trailer(which contains error-checking data) at the beginnning and end of the frame.
  For example : Train. The engine will be header and the last part of train which will show the green flag will be trailer. And all other compartment where passangers are sitting will be frames.
- If many devices share the same communication link, the data link layer determines which device has control over the link.

**Summary would be :**
 The data link layer is responsible for transmission, flow control, and error control between two nodes, whereas the transport layer is responsible for inter-network flow control and error control.

**7. Physical Layer :**

- It is the lowest layer of the OSI model
- It is used for the trasmission of an unstructured raw bit stream over a physical medium.
- Physical layer transmits the data either in the form of electrical/optical or mechanical form
- The Physical layer is mainly used for the physical connection between the device and such physical connection can be made by using twisted-pair cable, fibre-optic or wireless transmission media.



