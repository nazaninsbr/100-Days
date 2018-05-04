<b>Transport Layer</b>


1- _Services_<br/>
<ul>
	<li>A transport-layer protocol provides for logical communication between application processes running on different hosts.
	</li>
	<li>transport-layer services are implemented in end systems and not routers.</li>
	<li>transport-layer packet = <b>segment</b> and network-layer packet = <b>datagram</b></li>
	<li>process-to-process data delivery and error checking (both UDP and TCP provide this)</li>
</ul>
2-  _ transport-layer protocols _<br/>
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
3- _ network-layer protocol _<br/>
<ul>
	<li>IP
		<ul>
	    <li>logical communication between hosts</li>
	    <li>best-effort delivery service (no guarantee of delivery, in-order delivery or data integrity)
	    </li>
	    </ul>
	</li>
</ul>
