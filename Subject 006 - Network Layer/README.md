# Network Layer

<p style="color: #D3D3D3">
	Sources:<br>
	[1] Computer Networking: A Top Down Approach <br>
	[2] My Prof. Slides at University of Tehran
	<hr>
</p>

## Terminology
<ul>
	<li><b>Forwarding</b> involves the transfer of a packet from an incoming link to an outgoing link within a single router.</li>
	<li><b>Routing</b> involves all of a network’s routers, whose collective interactions via routing protocols determine the paths that packets take on their trips from source to destination node.</li>
</ul>

## Summary 

1- Network Layer Services<br>
<ul>
	<li>(1) Routing (network-wide process that determines the end-to-end paths that packets take from source to destination)</li>
	<li>(2) Forwarding (router-local action of transferring a packet from an input link interface to the appropriate output link interface)</li>
	<li>The network layer must determine the route or path taken by packets as they flow from a sender to a receiver. The algorithms that calculate these paths are referred to as <b>routing algorithms</b>.</li>
	<li>Every router has a <b>forwarding table</b>. A router forwards a packet by examin- ing the value of a field in the arriving packet’s header, and then using this header value to index into the router’s forwarding table. The value stored in the forward- ing table entry for that header indicates the router’s outgoing link interface to which that packet is to be forwarded. Depending on the network-layer protocol, the header value could be the destination address of the packet or an indication of the connection to which the packet belongs.</li>
	<li>the routing algorithm determines the values that are inserted into the routers’ forwarding tables.
		<ul>
			<li>centralized (with an algorithm executing on a central site and downloading routing information to each of the routers)</li>
			<li>decentralized (with a piece of the distributed routing algorithm running in each router)</li>
		</ul>
	</li>
	<li>link-layer switches base their forwarding decision on values in the fields of the link-layer frame; switches are thus referred to as link-layer (layer 2) devices. Other packet switches, called routers, base their forwarding decision on the value in the network layer field. Routers are thus network-layer (layer 3) devices, but must also implement layer 2 protocols as well, since layer 3 devices require the services of layer 2 to implement their (layer 3) functionality. </li>
	<li>(3: maybe) connection setup (the routers along the chosen path from source to destination to handshake with each other in order to set up state before network-layer data packets within a given source-to-destination connection can begin to flow)</li>
</ul>









