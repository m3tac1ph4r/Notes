# Computer Network

### Network :
A network is a set of devices that are connected with a physical media link. In a network, two or more nodes are connected by a physical link or two or more networks are connected by one or more nodes. A network is a collection of devices connected to each other to allow the sharing of data.



### Network Topology :
Network topology specifies the layout of a computer network. It shows how devices and cables are connected to each other.

**Types of Network Topology :**

**1. Star :**
* Star Topology is a network topology in which all the nodes are connected to a single device known as central device.
* Star topology requires more cable compared to other topologies. Therefore it is more robust as a failure in one cable will only disconnect a specific computer connected to this cable. 
* If  the centeral device is damaged, then the whole network fails.
* Star topology is very easy to install, manage and troubleshoot. It is commonly used in office and home networks.

![[star_topology.png]]

**2. Ring :**
* Ring topology is a network topology in which nodes are exactly connected to two or more nodes and thus, forming a single continuous path for the transmission.
* It does not need any centeral server to control the connectivity among the nodes.
* If the single node is damaged, then the whole network fails.
* Ring topology is very rarely used as it expensive, difficult to install and manage.

![[ring_topology.png]]

**3. Bus :**
* Bus topology is a network topology in which all the nodes are connected to a single cable known as a central cable or bus.
* It act as a shared communication medium i.e if any device wants to send the data to other devices then it will sent the data over the bus which in turn sends the data to all the attached devices.
* Bus topology is useful for small number of devices.
* As if the bus is damaged then the whole network fails.

![[bus_topology.png]]


**4. Mesh :**
* Mesh topology is a network topology in which all the nodes are individually connected to other nodes.
* It does not need any central switch or hub to control the connectivity among the nodes.
* Cabling cost is high as it requires bulk wiring.

![[mesh_topology.png]]


**5. Tree :**
* Tree topology is a combination of star and bus topology. It is also known as the  expanded star topology.
* Ethernet protocol is used in the tree topology.
* In this the whole network is divided into segments known as star networks which can be easily maintained. If one segment is damaged there is no effect on other segments.
* Tree topology depends on the "main bus" and if it breaks then the whole network gets damaged.

![[tree_topology.png]]

**6. Hybrid Topology :**
* A hybrid topology is a combination of different topologies to form a resulting topology.
* If star topology is connected with another star topology then it remains a star topology. If star is connected with different topology then it becomes a hybrid topology.
* It provides flexibility as it can be implemented in a different network enviroment.