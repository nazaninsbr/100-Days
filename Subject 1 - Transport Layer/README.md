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
	<li>connection-oriented
		<ul>
	    <li>handshake</li>
	    <li>TCP protocol runs only in the end systems and not in the intermediate network elements (routers and link-layer switches), the intermediate network elements do not maintain TCP connection state.</li>
	    </ul>
	</li>
	<li>Services
		<ul>
			<li>full-duplex service</li>
			<li>point-to-point (multicasting is not possible)</li>
		</ul>
	</li>
	<li>three-way handshake []
	</li>
	<li>things to know
		<ul>
			<li>MSS [MSS limits a segments data field <b>NOT</b> the entire segment size]</li>
			<li>MTU</li>
			<li>how is MSS set?</li>
			<li>when should tcp send buffered data?</li>
			<li>TCP connection consists of buffers, vari- ables, and a socket connection to a process in one host, and another set of buffers, variables, and a socket connection to a process in another host. As mentioned ear- lier, no buffers or variables are allocated to the connection in the network elements (routers, switches, and repeaters) between the hosts.</li>
		</ul>
	</li>
	<li>TCP Segment
		<ul>
			<li>TCP header is typically 20 bytes</li>
			<li>32-bit sequence number field (used for reliable transfer)</li>
			<li>32-bit acknowledgment number field (used for reliable transfer)</li>
			<li>16-bit receive window (used for flow control)</li>
			<li>4-bit header length field (size of header length as a multiple of 32 bits)</li>
			<li>options field</li>
			<li>6-bit flag field [ACK bit, RST, SYN, and FIN, PSH bit indicates that the receiver should pass the data to the upper layer immediately. Finally, the URG bit is used to indicate that there is data in this segment that the sending-side upper-layer entity has marked as “urgent.”] </li>
			<li>16-bit urgent data pointer field (The location of the last byte of this urgent data)</li>
		</ul>
	</li>
	<li>TCP is said to provide cumulative acknowledgments</li>
	<li> the receiver keeps the out-of-order bytes and waits for the missing bytes to fill in the gaps => more efficient in terms of network bandwidth [not inforced]</li>
	<li>Round Trip Time
		<ol type="A">
			<li>Length of timeout: the timeout should be larger than the connection’s round-trip time (RTT) [or unnecessary retransmissions would be sent.] </li>
			<li>SampleRTT, for a segment is the amount of time between when the segment is sent (that is, passed to IP) and when an acknowledg- ment for the segment is received. [not calculated for each segment usually one sample RTT taken at a time](never computes a SampleRTT for a segment that has been retransmitted; it only measures SampleRTT for segments that have been transmitted once)</li>
			<li>EstimatedRTT = (1 – 􏰃A) * EstimatedRTT + 􏰃A * SampleRTT [this weighted average puts more weight on recent samples than on old samples.]</li>
			<li>variability of the RTT.DevRTT, as an estimate of how much SampleRTT typically deviates from EstimatedRTT:<br/>
			DevRTT = (1 – 􏰄B) • DevRTT + 􏰄B •| SampleRTT – EstimatedRTT |</li>
			<li>TimeoutInterval = EstimatedRTT + 4 • DevRTT [when a timeout occurs, the value of TimeoutInterval is doubled to avoid a premature timeout occurring for a subsequent segment that will soon be acknowledged.]</li>
		</ol>
	</li>
</ul>
8- <i> TCP: Reliable Data Transfer </i><br/>
<ul>
	<li>the data stream that a process reads out of its TCP receive buffer is uncorrupted, without gaps, without duplication, and in sequence; that is, the byte stream is exactly the same byte stream that was sent by the end system on the other side of the connection</li>
	<li>retransmission: timeout | duplicate ack</li>
	<li>TCP sender FSM</li>
	<li>Doubling the Timeout Interval and going back to the formula after new ACK</li>
	<li>TCP does not use negative acknowledgments, the receiver cannot send an explicit negative acknowledgment back to the sender</li>
	<li><b>Fast Retransmit</b>
		<ul>
			<li>One of the problems with timeout-triggered retransmissions is that the timeout period can be relatively long</li>
			<li>A duplicate ACK is an ACK that reacknowledges a segment for which the sender has already received an earlier acknowledgment.</li>
			<li style="color: red;">TCP receiver’s ACK generation policy</li>
			<li>In the case that three duplicate ACKs are received, the TCP sender performs a fast retransmit, retransmitting the missing segment before that segment’s timer expires</li>
		</ul>
	</li>
</ul>
9- <i> TCP: Flow Control </i><br/>
<ul>
	<li>If the application is rela- tively slow at reading the data, the sender can very easily overflow the connection’s receive buffer by sending too much data too quickly.
	</li>
	<li>Flow control is thus a speed-matching service—matching the rate at which the sender is sending against the rate at which the receiving application is reading.</li>
	<li>TCP provides flow control by having the sender maintain a variable called the receive window. Informally, the receive window is used to give the sender an idea of how much free buffer space is available at the receiver.</li>
	<li>LastByteRcvd – LastByteRead 􏰅<= RcvBuffer</li>
	<li>rwnd = RcvBuffer – [LastByteRcvd – LastByteRead]</li>
	<li>Because the spare room changes with time, rwnd is dynamic</li>
	<li><b>Problem and Solution:</b> There is one minor technical problem with this scheme. To see this, suppose Host B’s receive buffer becomes full so that rwnd = 0. After advertising rwnd = 0 to Host A, also suppose that B has nothing to send to A. Now consider what hap- pens. As the application process at B empties the buffer, TCP does not send new seg- ments with new rwnd values to Host A; indeed, TCP sends a segment to Host A only if it has data to send or if it has an acknowledgment to send. Therefore, Host A is never informed that some space has opened up in Host B’s receive buffer—Host A is blocked and can transmit no more data! To solve this problem, the TCP specifi- cation requires Host A to continue to send segments with one data byte when B’s receive window is zero. These segments will be acknowledged by the receiver. Eventually the buffer will begin to empty and the acknowledgments will contain a nonzero rwnd value.</li>
</ul>
10- <i> TCP: Connection Management </i><br/>
<ul>
	<li>TCP connection establishment can significantly add to perceived delays
	</li>
	<li>Make Connection:
		<ol>
			<li><b>SYN Segment :</b> The client-side TCP first sends a special TCP segment to the server-side TCP. This special segment contains no application-layer data. But one of the flag bits in the segment’s header (see Figure 3.29), the SYN bit, is set to 1. client randomly chooses an initial sequence number and puts this number in the sequence number field of the initial TCP SYN segment.</li>
			<li><b>SYNACK segment :</b> TCP SYN segment arrives at the server host (assuming it does arrive!), the server extracts the TCP SYN segment from the datagram, allocates the TCP buffers and variables to the connection, and sends a connection-granted segment to the client TCP. [allocation of these buffers and variables before completing the third step of the three-way handshake makes TCP vulnerable to a denial-of-service attack known as SYN flooding.]</li>
			<li>Upon receiving the SYNACK segment, the client also allocates buffers and variables to the connection. The client host then sends the server yet another segment; this last segment acknowledges the server’s connection-granted segment. The SYN bit is set to zero, since the connection is established. This third stage of the three-way handshake may carry client-to-server data in the segment payload.</li>
		</ol>
	</li>
	<li>Close Connection:
		<ol>
			<li>FIN</li>
			<li>FIN_WAIT_1</li>
			<li>FIN_WAIT_2</li>
			<li>TIME_WAIT</li>
		</ol>
	</li>
</ul>

11- <i> Principles of Congestion Control </i><br/>
<ul>
	<li>read the 3 scenarios
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
			<li>(2) Congestion avoidance [mandatory]
				<ul>
					<li>increases the value of cwnd by just a single MSS every RTT</li>
					<li>method 1: increase cwnd by MSS bytes (MSS/cwnd) when- ever a new acknowledgment arrives.</li>
					<li>The value of cwnd is set to 1 MSS, and the value of ssthresh is updated to half the value of cwnd when the loss event occurred.</li>
					<li>triple duplicate ACK: TCP halves the value of cwnd (adding in 3 MSS for good measure to account for the triple duplicate ACKs received) and records the value of ssthresh to be half the value of cwnd when the triple duplicate ACKs were received. The fast-recovery state is then entered.</li>
				</ul>
			</li>
			<li>(3) Fast recovery 
				<ul>
					<li> the value of cwnd is increased by 1 MSS for every duplicate ACK received for the missing segment that caused TCP to enter the fast-recovery state.</li>
					<li> TCP Tahoe, unconditionally cut its congestion window to 1 MSS and entered the slow-start phase after either a timeout-indicated or triple-duplicate-ACK-indicated loss event. The newer version of TCP, TCP Reno, incorporated fast recovery.</li>
				</ul>
			</li>
		</ul>
	</li>
	<li>read pages 278 - 282 of the book</li>
</ul>


+++ <i> Some Things to Remember </i> +++<br/>
<ol type="1">
  <li>Each port number is a 16-bit number, ranging from 0 to 65535.</li>
  <li>The port numbers ranging from 0 to 1023 are called well-known port num- bers and are restricted, which means that they are reserved for use by well-known application protocols such as HTTP (which uses port number 80) and FTP (which uses port number 21).</li>
  <li>a TCP socket is identified by a four-tuple: (source IP address, source port number, destination IP address, destination port number).</li>
  <li>A connection-establishment request is nothing more than a TCP segment with desti- nation port number 12000 and a special connection-establishment bit set in the TCP header</li>
  <li>If the client and server are using persistent HTTP, then throughout the duration of the persistent connection the client and server exchange HTTP messages via the same server socket. However, if the client and server use non-persistent HTTP, then a new TCP connection is created and closed for every request/response, and hence a new socket is created and later closed for every request/response. </li>
  <li>The TCP segment has 20 bytes of header over- head in every segment, whereas UDP has only 8 bytes of overhead.</li>
  <li>TCP has a 32-bit sequence number field, where TCP sequence numbers count bytes in the byte stream rather than packets.</li>
  <li>Both Ethernet and PPP link-layer proto- cols have an MSS of 1,500 bytes.</li>
</ol>
:)



