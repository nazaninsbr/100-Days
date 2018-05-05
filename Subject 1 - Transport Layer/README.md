<b>Transport Layer</b>

<p style="color: #D3D3D3">
	Sources:<br>
	[1] Computer Networking: A Top Down Approach <br>
	[2] 
	<hr>
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
	<li><b>NO</b> service provides the following:
		<ul style="list-style-type:square">
		    <li>bandwidth guarantee</li>
		    <li>delay guarantee
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
	<li> What it does: 
		<ul style="list-style-type:disc">
	    <li>multiplexing/demultiplexing</li>
	    <li>error checking</li>
	    </ul>
	</li>
	<li> Characteristics
		<ul>
	    <li>packets may be lost</li>
	    <li>packets may arrive out of order</li>
	    <li>no handshaking: connectionless</li>
	    <li>each segment handled independently of others</li>
	    </ul>
	</li>
	<li> Examples of use
		<ol type="A">
	    <li>DNS</li>
	    <li>SNMP</li>
	    <li>Multimedia</li>
	    <li>Real-time apps</li>
	    </ol>
	</li>
	<li> Why would we want UDP?
		<ul style="list-style-type:square">
	    <li>no connection establishment (less delay)</li>
	    <li>simple: no connection state</li>
	    <li>small header size</li>
	    <li>no congestion control: more control on when and how much to send</li>
	    </ul>
	</li>
	<li> Segment structure
		<ul style="list-style-type:disc">
	    <li>source port</li>
	    <li>destination port</li>
	    <li>length = header + data (in bytes)</li>
	    <li>checksum (to check for errors): check out <a href="https://stackoverflow.com/questions/1480580/udp-checksum-calculation">this</a> and <a href="https://www.slashroot.in/how-is-tcp-and-udp-checksum-calculated">this</a> link for more</li>
	    <li>application data</li>
	    </ul>
	</li>
</ul>
6- <i> Reliable Data Transfer </i><br/>
<ul>
	<li> rdt (more details <a href="http://www2.ic.uff.br/~michael/kr1999/3-transport/3_040-principles_rdt.htm">here</a>)
		<ul>
			<li>rdt1.0 : the channel is reliable [so only rdt_send and rdt_recv]</li>
			<li>rdt2.0 : channel with bit error => so we add error detection and ACK and NACK [for feedback] and retransmission [these kinds of protocols are known as <b>stop and wait</b>]</li>
			<li>rdt2.1 : what if ACK and NACK are corrupt? we could have duplicate problem => add sequence numbers [0 and 1 will do]
				**** 1-bit sequence number will suffice, since it will allow the receiver to know whether the sender is resending the previously transmitted packet (the sequence number of the received packet has the same sequence number as the most recently received packet) or a new packet (the sequence number changes, moving “forward” in modulo-2 arithmetic). *****
			</li>
			<li>rdt2.2 : a NACK free protocol => sequence number must be added in ACK packet</li>
			<li>rdt3.0 : packet loss => add timeout
				<ul style="list-style-type:disc">
			    <li>d[trans] = L / R</li>
			    <li>U[sender] = (L/R)/(RTT+L/R)</li>
			    <li>so..awful performance</li>
			    </ul>
			</li>
			<li>pipeline protocols : to improve performance => range of seq. numbers + multiple in-flight packets + buffering [<a href="http://www.ccs-labs.org/teaching/rn/animations/gbn_sr/">this link</a> and <a href="https://www.slideshare.net/skyla12345/go-backn-protocol">this one</a> could be useful]
				<ul style="list-style-type:square">
			    <li><b>GBN (Go Back-N)</b>
			    	<ul>
			    		<li>N, unacknowledged packets in the pipeline.</li>
			    		<li>If we define base to be the sequence number of the oldest unacknowledged packet and nextseqnum to be the smallest unused sequence number (that is, the sequence number of the next packet to be sent), then four intervals in the range of sequence numbers can be identified. Sequence numbers in the interval [0,base-1] correspond to packets that have already been transmitted and acknowledged. The inter- val [base,nextseqnum-1] corresponds to packets that have been sent but not yet acknowledged. Sequence numbers in the interval [nextseqnum,base+N-1] can be used for packets that can be sent immediately, should data arrive from the upper layer. Finally, sequence numbers greater than or equal to base+N cannot be used until an unacknowledged packet currently in the pipeline (specifically, the packet with sequence number base) has been acknowledged.</li>
			    		<li>flow control is one reason to impose a limit on the sender.</li>
			    		<li>cumulative acknowledgment, indicat- ing that all packets with a sequence number up to and including n have been cor- rectly received at the receiver.</li>
			    		<li>a timer for the oldest transmitted but not yet acknowledged packet.</li>
			    		<li>In our GBN protocol, the receiver discards out-of-order packets. Although it may seem silly and wasteful to discard a correctly received (but out-of-order) packet, there is some justification for doing so. Recall that the receiver must deliver data in order to the upper layer. Suppose now that packet n is expected, but packet n + 1 arrives. Because data must be delivered in order, the receiver could buffer (save) packet n + 1 and then deliver this packet to the upper layer after it had later received and delivered packet n. However, if packet n is lost, both it and packet n + 1 will eventually be retransmitted as a result of the GBN retransmission rule at the sender. Thus, the receiver can simply discard packet n + 1. The advantage of this approach is the simplicity of receiver buffering—the receiver need not buffer any out-of-order packets.</li>
			    	</ul>
			    </li>
			    <li><b>Selective Repeat</b>
			    	<ul>
			    		<li>avoid unnecessary retransmissions by having the sender retransmit only those packets that it suspects were received in error.</li>
			    		<li>receiver individually acknowledge correctly received packets.</li>
			    		<li>receiver will acknowledge a correctly received packet whether or not it is in order. Out-of-order packets are buffered until any missing packets (that is, packets with lower sequence numbers) are received</li>
			    		<li>receiver reacknowledges already received packets with certain sequence numbers below the current window base, this reacknowledgment is indeed needed. if there is no ACK for packet send_base propagating from the receiver to the sender, the sender will eventually retransmit packet send_base, even though it is clear (to us) that the receiver has already received that packet. If the receiver were not to acknowledge this packet, the sender’s window would never move forward</li>
			    	</ul>
			    </li>
			    </ul>
			</li>
	    </ul>
	</li>
</ul>
7-<i> TCP </i><br/>
<ul>
	<li>
		<ul>
	    <li></li>
	    </ul>
	</li>
</ul>





12- <i> TCP Congestion Control </i><br/>
<ul>
	<li> The basics:
		<ul>
		<li>TCP must use end-to-end congestion control rather than net- work-assisted congestion control, since the IP layer provides no explicit feedback to the end systems regarding network congestion.
		</li>
		<li>Limit the rate at which it sends traffic into its connection as a function of perceived network congestion.</li>
		<li>LastByteSent – LastByteAcked 􏰅<= min{cwnd, rwnd}</li>
		<li>loss and packet transmission delays are negligible => the sender’s send rate is roughly cwnd/RTT bytes/sec.</li>
		<li>TCP uses acknowledgments to trigger (or clock) its increase in congestion window size, TCP is said to be <b>self-clocking</b>.
			<ul style="list-style-type:square">
			<li>additive increase</li>
			<li>multiplicative decrease</li>
			</ul>
		</li>
		</ul>
	</li>
	<li>TCP congestion control algorithm:
		<ul style="list-style-type:disc">
			<li>(1) Slow start [mandatory]
				<ul style="list-style-type:disc">
					<li>cwnd is typically initialized to a small value of 1 MSS</li>
					<li>cwnd begins at 1 MSS and increases by 1 MSS every time a transmitted segment is first acknowledged.</li>
					<li>doubling of the sending rate every RTT.</li>
					<li>if there is a loss event (i.e., congestion) indicated by a timeout, the TCP sender sets the value of cwnd to 1 and begins the slow start process anew. It also sets the value of a second state variable, ssthresh (shorthand for “slow start threshold”) to cwnd/2</li>
					<li>when the value of cwnd equals ssthresh, slow start ends and TCP transitions into congestion avoidance mode.</li>
					<li>if three duplicate ACKs are detected TCP performs a fast retransmit</li>
				</ul>
			</li>
			<li>(1) Congestion avoidance [mandatory]
				<ul>
					<li>increases the value of cwnd by just a single MSS every RTT</li>
					<li>method 1: increase cwnd by MSS bytes (MSS/cwnd) when- ever a new acknowledgment arrives.</li>
					<li>The value of cwnd is set to 1 MSS, and the value of ssthresh is updated to half the value of cwnd when the loss event occurred.</li>
					<li>triple duplicate ACK: TCP halves the value of cwnd (adding in 3 MSS for good measure to account for the triple duplicate ACKs received) and records the value of ssthresh to be half the value of cwnd when the triple duplicate ACKs were received. The fast-recovery state is then entered.</li>
				</ul>
			</li>
			<li>(1) Fast recovery 
				<ul>
					<li> the value of cwnd is increased by 1 MSS for every duplicate ACK received for the missing segment that caused TCP to enter the fast-recovery state.</li>
				</ul>
			</li>
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
  <li>The TCP segment has 20 bytes of header over- head in every segment, whereas UDP has only 8 bytes of overhead.</li>
  <li>TCP has a 32-bit sequence number field, where TCP sequence numbers count bytes in the byte stream rather than packets.</li>
</ol>
:)



