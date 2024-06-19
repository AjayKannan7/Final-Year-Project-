Title: A More Effective Distributed Energy Efficient Clustering Method For Heterogeneous WSNs
Program:
# Define options
set val(chan) Channel/WirelessChannel ;# channel type
set val(prop) Propagation/TwoRayGround ;# radio-propagation model
set val(netif) Phy/WirelessPhy ;# network interface type
set val(mac) Mac/802_11 ;# MAC type
set val(ifq) Queue/DropTail/PriQueue ;# interface queue type
set val(ll) LL ;# link layer type
set val(ant) Antenna/OmniAntenna ;# antenna model
set val(ifqlen) 50 ;# max packet in ifq
set val(nn) 31 ;# number of mobilenodes
set val(rp) DSDV ;# routing protocol
set val(x) 1000 ;# X dimension of topography
set val(y) 1000 ;# Y dimension of topography
set val(stop) 150 ;# time of simulation end

set ns [new Simulator]

set tf [open tf.tr w]
set ntf [open ntf.nam w]

$ns trace-all $tf
$ns namtrace-all-wireless $ntf 600 600

set topo [new Topography]

$topo load_flatgrid $val(x) $val(y)

create-god $val(nn)



# configure the nodes
$ns node-config -adhocRouting $val(rp) \
-llType $val(ll) \
-macType $val(mac) \
-ifqType $val(ifq) \
-ifqLen $val(ifqlen) \
-antType $val(ant) \
-propType $val(prop) \
-phyType $val(netif) \
-channelType $val(chan) \
-topoInstance $topo \
-agentTrace ON \
-routerTrace ON \
-macTrace OFF \
-movementTrace ON

for {set i 0} {$i < $val(nn) } { incr i } {
set n($i) [$ns node]
 $n($i) color blue
            $ns at 2.0 "$n($i) color green"
 

}
for {set i 0} {$i < $val(nn) } { incr i } {
set xx($i) [expr rand()*1000]
set yy($i) [expr rand()*1000]
$n($i) set X_ $xx($i)
$n($i) set Y_ $yy($i)
}
$n(0) set X_ 30.0
$n(0) set Y_ 1.0
$n(0) set Z_ 0.0

$n(1) set X_ 30.0
$n(1) set Y_ 4.0
$n(1) set Z_ 0.0





$n(2) set X_ -65.0326
$n(2) set Y_ 168.474
$n(2) set Z_ 0.0


$n(3) set X_ -185.9721
$n(3) set Y_ 33.69709
$n(3) set Z_ 0.0

$n(4) set X_ -315.9721
$n(4) set Y_ 8.69709
$n(4) set Z_ 0.0






$n(5) set X_ 69.0
$n(5) set Y_ 6.0
$n(5) set Z_ 0.0

$n(6) set X_ 62.1082  
$n(6) set Y_ 76.3292
$n(6) set Z_ 0.0

$n(7) set X_ -243.542  
$n(7) set Y_ 7.03255
$n(7) set Z_ 0.0
$n(8) set X_ 141.879  
$n(8) set Y_ 26.0387
$n(8) set Z_ 0.0

$n(9) set X_ -215.9721
$n(9) set Y_ 22.69709
$n(9) set Z_ 0.0


$n(10) set X_ 28.2921  
$n(10) set Y_ 50.3169
$n(10) set Z_ 0.0



$n(11) set X_ -179.459  
$n(11) set Y_ 8.69709
$n(11) set Z_ 0.0
 
$n(12) set X_ -230.9721  
$n(12) set Y_ 111.79
$n(12) set Z_ 0.0

$n(13) set X_ -277.2009  
$n(13) set Y_ 17.606
$n(13) set Z_ 0.0

$n(14) set X_ 617.039 
$n(14) set Y_ 87.544
$n(14) set Z_ 0.0

$n(15) set X_ 536.134  
$n(15) set Y_ 79.493
$n(15) set Z_ 0.0

$n(16) set X_ 499.983  
$n(16) set Y_ 90.291
$n(16) set Z_ 0.0

$n(17) set X_ 477.67  
$n(17) set Y_ 82.291
$n(17) set Z_ 0.0

$n(18) set X_ 506.09  
$n(18) set Y_ 65.606
$n(18) set Z_ 0.0

$n(19) set X_ 306.039 
$n(19) set Y_ 87.544
$n(19) set Z_ 0.0

$n(20) set X_ 281.134  
$n(20) set Y_ 60.493
$n(20) set Z_ 0.0

$n(21) set X_ 261.983  
$n(21) set Y_ 90.291
$n(21) set Z_ 0.0

$n(22) set X_ 233.67  
$n(22) set Y_ 82.291
$n(22) set Z_ 0.0

$n(23) set X_ 210.09  
$n(23) set Y_ 65.606
$n(23) set Z_ 0.0

$n(24) set X_ 261.9  
$n(24) set Y_ 168.474
$n(24) set Z_ 0.0

$n(25) set X_ 439.983  
$n(25) set Y_ 168.474
$n(25) set Z_ 0.0

$n(26) set X_ 300.983  
$n(26) set Y_ 208.474
$n(26) set Z_ 0.0

$n(27) set X_ 145.983  
$n(27) set Y_ 370.474
$n(27) set Z_ 0.0



$n(28) set X_ 145.983  
$n(28) set Y_ 240.474
$n(28) set Z_ 0.0

$n(29) set X_ 62.1082
$n(29) set Y_ 168.474
$n(29) set Z_ 0.0

$n(30) set X_ 400.983  
$n(30) set Y_ 208.0
$n(30) set Z_ 0.0

########################################################################################################################
#                                            CLUSTER SIZE CALCULATION                                    

############################################################################################################################3

for {set i 0} {$i < $val(nn) } { incr i } {
     puts "\n"
     #puts $r "\n"

     for {set j 1} {$j < $val(nn) } { incr j } {
                                           
                                                set dx [expr $xx($i) - $xx($j)]
                                                set dy [expr $yy($i) - $yy($j)]

                                                set dx2 [expr $dx * $dx]
                                                set dy2 [expr $dy * $dy]

                                                set h2 [expr $dx2 + $dy2]

                                                set h($i-$j) [expr pow($h2, 0.5)]
                                                puts "CLUSTER SIZE ($i)  = $h($i-$j)"
                                                
                                                
   }
}

set clustersize 0


proc algorithm {} {

    global h val node_ r ns clustersize router 

set now [$ns now]

set time 1.0


set count($clustersize) 0

     for {set j 0} {$j < $val(nn) } { incr j } {
                  #   $h($clustersize-$j)=intrusion detection                      
                 if {$h($clustersize-$j) <  j} {

				set count($clustersize) [expr $count($clustersize)]
				set n($clustersize-$count($clustersize)) $j


q=count
k2=source
T2=hopcount
r=h
l2 =val

                                 size=qk2T2r/l2;


W=a1*N+(-a2*stability+a3*load/N
}
     #   $h($clustersize-$j)=intrusion prevention                       
                 if {$h($clustersize-$j) >j} {

				set count($clustersize) [expr $count($clustersize)]
				set n($clustersize-$count($clustersize)) $j
}
}
}


set tcp11 [new Agent/TCP/Newreno]
$tcp11 set maxcwnd_ 11
$tcp11 set fid_ 4
set sink11 [new Agent/TCPSink]
$ns attach-agent $n(24) $tcp11
$ns attach-agent $n(23) $sink11
$ns connect $tcp11 $sink11
set ftp11 [new Application/FTP]
$ftp11 attach-agent $tcp11
$ns at 0.0 "$ftp11 start"
$ns at 20.0 "$ftp11 stop"

set tcp12 [new Agent/TCP/Newreno]
$tcp12 set maxcwnd_ 12
$tcp12 set fid_ 4
set sink12 [new Agent/TCPSink]
$ns attach-agent $n(29) $tcp12
$ns attach-agent $n(26) $sink12
$ns connect $tcp12 $sink12
set ftp12 [new Application/FTP]
$ftp12 attach-agent $tcp12
$ns at 41.0 "$ftp12 start"
$ns at 60.0 "$ftp12 stop"





set tcp14 [new Agent/TCP/Newreno]
$tcp14 set maxcwnd_ 14
$tcp14 set fid_ 4
set sink14 [new Agent/TCPSink]
$ns attach-agent $n(26) $tcp14
$ns attach-agent $n(24) $sink14
$ns connect $tcp14 $sink14
set ftp14 [new Application/FTP]
$ftp14 attach-agent $tcp14
$ns at 21.0 "$ftp14 start"
$ns at 40.0 "$ftp14 stop"

set tcp15 [new Agent/TCP/Newreno]
$tcp15 set maxcwnd_ 15
$tcp15 set fid_ 4
set sink15 [new Agent/TCPSink]
$ns attach-agent $n(12) $tcp15
$ns attach-agent $n(4) $sink15
$ns connect $tcp15 $sink15
set ftp15 [new Application/FTP]
$ftp15 attach-agent $tcp15
$ns at 0.0 "$ftp15 start"
$ns at 20.0 "$ftp15 stop"


set tcp16 [new Agent/TCP/Newreno]
$tcp16 set maxcwnd_ 16
$tcp16 set fid_ 4
set sink16 [new Agent/TCPSink]
$ns attach-agent $n(12) $tcp16
$ns attach-agent $n(13) $sink16
$ns connect $tcp16 $sink16
set ftp16 [new Application/FTP]
$ftp16 attach-agent $tcp16
$ns at 0.0 "$ftp16 start"
$ns at 20.0 "$ftp16 stop"

set tcp17 [new Agent/TCP/Newreno]
$tcp17 set maxcwnd_ 17
$tcp17 set fid_ 4
set sink17 [new Agent/TCPSink]
$ns attach-agent $n(24) $tcp17
$ns attach-agent $n(22) $sink17
$ns connect $tcp17 $sink17
set ftp17 [new Application/FTP]
$ftp17 attach-agent $tcp17
$ns at 0.0 "$ftp17 start"
$ns at 20.0 "$ftp17 stop"


set tcp18 [new Agent/TCP/Newreno]
$tcp18 set maxcwnd_ 18
$tcp18 set fid_ 4
set sink18 [new Agent/TCPSink]
$ns attach-agent $n(24) $tcp18
$ns attach-agent $n(19) $sink18
$ns connect $tcp18 $sink18
set ftp18 [new Application/FTP]
$ftp18 attach-agent $tcp18
$ns at 0.0 "$ftp18 start"
$ns at 20.0 "$ftp18 stop"


set tcp19 [new Agent/TCP/Newreno]
$tcp19 set maxcwnd_ 19
$tcp19 set fid_ 4
set sink19 [new Agent/TCPSink]
$ns attach-agent $n(2) $tcp19
$ns attach-agent $n(12) $sink19
$ns connect $tcp19 $sink19
set ftp19 [new Application/FTP]
$ftp19 attach-agent $tcp19
$ns at 21.0 "$ftp19 start"
$ns at 40.0 "$ftp19 stop"


set tcp20 [new Agent/TCP/Newreno]
$tcp20 set maxcwnd_ 20
$tcp20 set fid_ 4
set sink20 [new Agent/TCPSink]
$ns attach-agent $n(29) $tcp20
$ns attach-agent $n(6) $sink20
$ns connect $tcp20 $sink20
set ftp20 [new Application/FTP]
$ftp20 attach-agent $tcp20
$ns at 21.0 "$ftp20 start"
$ns at 40.0 "$ftp20 stop"

set tcp21 [new Agent/TCP/Newreno]
$tcp21 set maxcwnd_ 21
$tcp21 set fid_ 4
set sink21 [new Agent/TCPSink]
$ns attach-agent $n(30) $tcp21
$ns attach-agent $n(25) $sink21
$ns connect $tcp21 $sink21
set ftp21 [new Application/FTP]
$ftp21 attach-agent $tcp21
$ns at 21.0 "$ftp21 start"
$ns at 40.0 "$ftp21 stop"




set tcp22 [new Agent/TCP/Newreno]
$tcp22 set maxcwnd_ 22
$tcp22 set fid_ 4
set sink22 [new Agent/TCPSink]
$ns attach-agent $n(6) $tcp22
$ns attach-agent $n(5) $sink22
$ns connect $tcp22 $sink22
set ftp22 [new Application/FTP]
$ftp22 attach-agent $tcp22
$ns at 0.0 "$ftp22 start"
$ns at 20.0 "$ftp22 stop"


set tcp23 [new Agent/TCP/Newreno]
$tcp23 set maxcwnd_ 23
$tcp23 set fid_ 4
set sink23 [new Agent/TCPSink]
$ns attach-agent $n(6) $tcp23
$ns attach-agent $n(1) $sink23
$ns connect $tcp23 $sink23
set ftp23 [new Application/FTP]
$ftp23 attach-agent $tcp23
$ns at 0.0 "$ftp23 start"
$ns at 20.0 "$ftp23 stop"

set tcp24 [new Agent/TCP/Newreno]
$tcp24 set maxcwnd_ 24
$tcp24 set fid_ 4
set sink24 [new Agent/TCPSink]
$ns attach-agent $n(25) $tcp24
$ns attach-agent $n(14) $sink24
$ns connect $tcp24 $sink24
set ftp24 [new Application/FTP]
$ftp24 attach-agent $tcp24
$ns at 0.0 "$ftp24 start"
$ns at 20.0 "$ftp24 stop"

set tcp25 [new Agent/TCP/Newreno]
$tcp25 set maxcwnd_ 25
$tcp25 set fid_ 4
set sink25 [new Agent/TCPSink]
$ns attach-agent $n(28) $tcp25
$ns attach-agent $n(27) $sink25
$ns connect $tcp25 $sink25
set ftp25 [new Application/FTP]
$ftp25 attach-agent $tcp25
$ns at 61.0 "$ftp25 start"
$ns at 80.0 "$ftp25 stop"




set tcp27 [new Agent/TCP/Newreno]
$tcp27 set maxcwnd_ 27
$tcp27 set fid_ 4
set sink27 [new Agent/TCPSink]
$ns attach-agent $n(30) $tcp27
$ns attach-agent $n(26) $sink27
$ns connect $tcp27 $sink27
set ftp27 [new Application/FTP]
$ftp27 attach-agent $tcp27
$ns at 41.0 "$ftp27 start"
$ns at 60.0 "$ftp27 stop"

set tcp28 [new Agent/TCP/Newreno]
$tcp28 set maxcwnd_ 28
$tcp28 set fid_ 4
set sink28 [new Agent/TCPSink]
$ns attach-agent $n(2) $tcp28
$ns attach-agent $n(28) $sink28
$ns connect $tcp28 $sink28
set ftp28 [new Application/FTP]
$ftp28 attach-agent $tcp28
$ns at 41.0 "$ftp28 start"
$ns at 60.0 "$ftp28 stop"

set tcp29 [new Agent/TCP/Newreno]
$tcp29 set maxcwnd_ 29
$tcp29 set fid_ 4
set sink29 [new Agent/TCPSink]
$ns attach-agent $n(29) $tcp29
$ns attach-agent $n(28) $sink29
$ns connect $tcp29 $sink29
set ftp29 [new Application/FTP]
$ftp29 attach-agent $tcp29
$ns at 61.0 "$ftp29 start"
$ns at 80.0 "$ftp29 stop"























#defining heads








$ns at 1.0 "$n(12) label CL1"
$ns at 1.0 "$n(6) label CL2"
$ns at 21.0 "$n(2) label CH1"
$ns at 1.0 "$n(24) label CL3"
$ns at 1.0 "$n(25) label CL4"
$ns at 21.0 "$n(26) label CH2"
$ns at 61.0 "$n(27) label SINK"
$ns at 21.0 "$n(29) label CH3"
$ns at 21.0 "$n(30) label CH4"
$ns at 61.0 "$n(28) label BC"




$ns at 1.0 "$ns trace-annotate \"TO SEARCH  THE CLUSTER  NODE\""
  $ns at 2.0 "$ns trace-annotate \"TO FIND THE THE CLUSTER  NODE\""
  $ns at 21.1 "$ns trace-annotate \"TO SEARCH  CH NODE\""     
  $ns at 22.0 "$ns trace-annotate \"TO FIND  THE SEARCH  CH NODE\"" 
 $ns at 41.0 "$ns trace-annotate \"BACK BONE TREE PROCESS\""
  $ns at 61.0 "$ns trace-annotate \"TO FIND THE BACKBONE THE NODE AND SINK NODE\""
  $ns at 61.1 "$ns trace-annotate \"COMMUNICATION BT CH AND BACK BONE AND SINK\""


#$ns at 15.0 "$n(11) setdest 115.0 85.0 5.0"

#$ns at 15.0 "$n(11) setdest 115.0 85.0 5.0"

#Color change while moving from one group to another



# 20 defines the node size for nam
# rem  defines the CL size for nam
$ns initial_node_pos $n(0) 20
$ns initial_node_pos $n(1) 20
$ns initial_node_pos $n(2) 40
$ns initial_node_pos $n(3) 20
$ns initial_node_pos $n(4) 20
$ns initial_node_pos $n(5) 20
$ns initial_node_pos $n(6) 20
$ns initial_node_pos $n(7) 20
$ns initial_node_pos $n(8) 20
$ns initial_node_pos $n(9) 20
$ns initial_node_pos $n(10) 20
$ns initial_node_pos $n(11) 20
$ns initial_node_pos $n(12) 20
$ns initial_node_pos $n(13) 20
$ns initial_node_pos $n(14) 20
$ns initial_node_pos $n(15) 20
$ns initial_node_pos $n(16) 20
$ns initial_node_pos $n(17) 20
$ns initial_node_pos $n(18) 20
$ns initial_node_pos $n(19) 20
$ns initial_node_pos $n(20) 20
$ns initial_node_pos $n(21) 20
$ns initial_node_pos $n(22) 20
$ns initial_node_pos $n(23) 20
$ns initial_node_pos $n(24) 20
$ns initial_node_pos $n(25) 20
$ns initial_node_pos $n(26) 40
$ns initial_node_pos $n(27) 50
$ns initial_node_pos $n(28) 50
$ns initial_node_pos $n(29) 40
$ns initial_node_pos $n(30) 40





$n(2) color black
$ns at 2.0 "$n(2) color black"
$n(29) color black
$ns at 2.0 "$n(29) color black"
$n(26) color black
$ns at 2.0 "$n(26) color black"
$n(30) color black
$ns at 2.0 "$n(30) color black"
$n(28) color black
$ns at 2.0 "$n(28) color black"
$n(27) color black
$ns at 2.0 "$n(27) color black"
$n(2) color red
$ns at 21.0 "$n(2) color red"
$n(26) color red
$ns at 21.0 "$n(26) color red"
$n(29) color red
$ns at 21.0 "$n(29) color red"
$n(30) color red
$ns at 21.0 "$n(30) color red"

$n(27) color pink
$ns at 61.0 "$n(27) color pink"
$n(28) color blue
$ns at 61.0 "$n(28) color blue"
# Telling nodes when the simulation ends
for {set i 0} {$i < $val(nn) } { incr i } {
$ns at $val(stop) "$n($i) reset";
}

# ending nam and the simulation
$ns at $val(stop) "$ns nam-end-wireless $val(stop)"
$ns at $val(stop) "stop"
$ns at 150.01 "puts \"end simulation\" ; $ns halt"
set udp [new Agent/UDP]
set sink [new Agent/LossMonitor]
set vbr [new Application/Traffic/Exponential]


$ns attach-agent $n(11) $udp 
$ns attach-agent $n(6) $sink
$vbr attach-agent $udp
$vbr set packetSize_ 100
$vbr set idle_time_ 12ms
$vbr set burst_time_ 20ms
$vbr set rate_ 10k

$ns connect $udp $sink


set f1 [open f1.tr w]
set f2 [open f2.tr w]
set f3 [open f3.tr w]
set f4 [open f4.tr w]
set f5 [open f5.tr w]
set f6 [open f6.tr w]
set f7 [open f7.tr w]

set a1 [open a1.tr w]
set a2 [open a2.tr w]
set a3 [open a3.tr w]
set a4 [open a4.tr w]
set a5 [open a5.tr w]
set a6 [open a6.tr w]
set a7 [open a7.tr w]


proc record {} {

global ns f1 f2 f3 f4 f5 f6 f7 sink
global f1 f2 f3 f4 f5 f6 f7 a1 a2 a3 a4 a5 a6 a7
set time 1 
set now [$ns now]

set bw1 [$sink set bytes_]
set bw2 [$sink set npkts_]
set bw3 [$sink set lastPktTime_]

puts $a1 "$now [expr $bw1/$time*.01/5]"
puts $a2 "$now [expr $bw1/$time*.05/5]"
puts $a5 "$now [expr $bw1/$time*.09/5]"
puts $a6 "$now [expr $bw3/$time*.001/5]"
puts $a3 "$now [expr $bw3/$time*.005/5]"
puts $a4 "$now [expr $bw3+$time*.003/5]"
puts $a7 "$now [expr $bw3+$time*6/5]"

$sink set bytes_ 1
$sink set npkts_ 0
$sink set nlost_ 0

$ns at [expr $now+$time] "record"

}


proc finish {} {

global ns tf ntf  a1 a2 a3 a4 a5 a6 a7
$ns flush-trace 
close $tf
close $ntf
close $a1
close $a2
close $a3
close $a4
close $a5
close $a6
close $a7
exec nam ntf.nam &
exec xgraph throughput.xg  -t "Throughput" -x "No.of nodes" -y "time(ms)" -bg white  &
exec xgraph pdr.xg  -t "pdr" -x "No.of nodes" -y "No.of packets sent" -bg white  &
exec xgraph energy.xg  -t "Energy consumption" -x "No.of nodes" -y "time(ms)" -bg white  &
exec xgraph delay.xg  -t "delay" -x "No.of nodes" -y "No.of packets sent" -bg white  &
exit 0 
}

$ns at 0.0 "$vbr start"
$ns at 0.3 "record"

$ns at 80.0 "$vbr stop"
$ns at 80.1 "finish"
$ns run
