<b>Transport Layer</b>

<p style="color: #D3D3D3">
	Sources:
	[1] Computer Networking: A Top Down Approach
	[2] 
</p>

1- _Services_<br/>
<ul>
	<li>A transport-layer protocol provides for logical communication between application processes running on different hosts.
	</li>
	<li>transport-layer services are implemented in end systems and not routers.</li>
	<li>transport-layer packet = <b>segment</b> and network-layer packet = <b>datagram</b></li>
	<li>process-to-process data delivery and error checking (both UDP and TCP provide this)</li>
</ul>
2-  <i> transport-layer protocols </i><br/>
<ul>
	<li>UDP
		<ul>
	    <li>unreliable</li>
	    <li>connectionless
	    </li>
	    <li>can send at any rate it pleases, for as long as it pleases.</li>
	    <li>process-to-process data delivery
	    </li>
	    <li>error checking
	    </li>
	    </ul>
	</li>
	<li>TCP
		<ul>
	    <li>reliable</li>
	    <li>connection-oriented
	    </li>
	    <li>flow control</li>
	    <li>sequence numbers
	    </li>
	    <li>acknowledgments</li>
	    <li>timers
	    </li>
	    <li>congestion control</li>
	    <li>process-to-process data delivery
	    </li>
	    <li>error checking
	    </li>
	    </ul>
	</li>
</ul>
3- <i> network-layer protocol </i><br/>
<ul>
	<li>IP
		<ul>
	    <li>logical communication between hosts</li>
	    <li>best-effort delivery service (no guarantee of delivery, in-order delivery or data integrity)
	    </li>
	    </ul>
	</li>
</ul>
4- <i> Multiplexing and Demultiplexing </i><br/>
<ul>
	<li><b>sockets</b>, doors through which data passes from the network to the process and through which data passes from the process to the network.
	</li>
	<li> Each transport-layer segment has a set of fields in the segment. This job of delivering the data in a transport-layer segment to the correct socket is called <b>demultiplexing</b>. </li>
	<li>The job of gathering data chunks at the source host from different sockets, encapsulating each data chunk with header information (that will later be used in demultiplexing) to create segments, and passing the segments to the network layer is called <b>multiplexing</b>. multiplexing requires: 
		<ul>
	    <li>(1) that sockets have unique identifiers</li>
	    <li>(2) that each segment have special fields that indicate the socket to which the segment is to be delivered, these fields are:
	    	<ul style="list-style-type:square">
		    <li>source port number field</li>
		    <li>destination port number field
		    </li>
		    </ul>
	    </li>
	    </ul>
	</li>
</ul>
5- <i> UDP </i><br/>
<ul>
	<li> what it does: 
		<ul style="list-style-type:disc">
	    <li>multiplexing/demultiplexing</li>
	    <li>error checking</li>
	    </ul>
	</li>
	<li> Why  
		<ul style="list-style-type:disc">
	    <li>multiplexing/demultiplexing</li>
	    <li>error checking</li>
	    </ul>
	</li>
</ul>







**- <i> Some Things to Remember </i><br/>
<ol type="1">
  <li>Each port number is a 16-bit number, ranging from 0 to 65535.</li>
  <li>The port numbers ranging from 0 to 1023 are called well-known port num- bers and are restricted, which means that they are reserved for use by well-known application protocols such as HTTP (which uses port number 80) and FTP (which uses port number 21).</li>
  <li>a TCP socket is identified by a four-tuple: (source IP address, source port number, destination IP address, destination port number).</li>
  <li>A connection-establishment request is nothing more than a TCP segment with desti- nation port number 12000 and a special connection-establishment bit set in the TCP header</li>
  <li>If the client and server are using persistent HTTP, then throughout the duration of the persistent connection the client and server exchange HTTP messages via the same server socket. However, if the client and server use non-persistent HTTP, then a new TCP connection is created and closed for every request/response, and hence a new socket is created and later closed for every request/response. </li>
</ol>
:)



