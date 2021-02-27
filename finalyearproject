# Define options
set val(chan)    Channel/WirelessChannel     ;# channel type
set val(prop)    Propagation/TwoRayGround    ;# radio-propagation model
set val(netif)   Phy/WirelessPhy             ;# network interface type
set val(mac)     Mac/802_11                  ;# MAC type
set val(ifq)     Queue/DropTail/PriQueue     ;# interface queue type
set val(ll)      LL                          ;# link layer type
set val(ant)     Antenna/OmniAntenna         ;# antenna model
set val(ifqlen)  50                          ;# max packet in ifq
set val(rp)      DSDV                        ;# routing protocol
set val(x)       500                          ;# X dimension of topography
set val(y)       500                         ;# Y dimension of topography 
set val(stop)    20                          ;# time of simulation end



#Creating simulation:
set ns [new Simulator]

#Creating nam and trace file:
set tracefd [open trail.tr w]
set namtrace [open trail.nam w]   

$ns trace-all $tracefd
$ns namtrace-all-wireless $namtrace $val(x) $val(y)



# set up topography object
set topo [new Topography]
$topo load_flatgrid $val(x) $val(y)
set god_ [create-god 15]

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
         






# Creating node objects..         
for {set i 0} {$i < 15 } { incr i } {
     set node($i) [$ns node]
     set udp($i) [new Agent/UDP]
     $ns attach-agent $node($i) $udp($i)
         
}
# Node representing color
for {set i 0} {$i < 15  } { incr i } {
     $node($i) color red
     $ns at 0.0 "$node($i) color red"
}



  
for {set i 0} {$i < 15 } { incr i } {
     set xx [expr {int(rand()*$val(x))}]
     set yy [expr {int(rand()*$val(y))}]

     $node($i) set X_ $xx
     $node($i) set Y_ $yy
   
     set nodeXpos($i) $xx
     set nodeYpos($i) $yy 
     set nodeZpos($i) 0.0                           
}


    
# Define node initial position in nam
for {set i 0} {$i < 15} { incr i } {
    $ns initial_node_pos $node($i) 30
}



for {set i 0} {$i < 15} { incr i} {
    for {set j 0} {$j < 15} { incr j} {
      set xpos($i) [expr {$nodeXpos($i) - $nodeXpos($j)}]
      set ypos($i) [expr {$nodeYpos($i) - $nodeYpos($j)}]
      set dis($i$j) [expr {abs($xpos($i)) + abs($ypos($i))}]
}
}
  



for {set i 0} {$i < 15} {incr i} {
   for {set j 0} {$j < 15} {incr j} {
        set sum($i$j) 0
}
}


for {set i 0} {$i < 15} {incr i} {
     set k 0
      while {$k < 15} {
         for {set j 0} {$j < 15} {incr j} {
              if ([expr {$dis($i$j) <= $dis($k$j)}]) {
                  set sum($i$k) [expr {$sum($i$k) + $dis($i$j)}]
}            else {
                  set sum($i$k) [expr {$sum($i$k) + $dis($k$j)}]
              
}
};
 incr k
};
};


for {set i 0} {$i < 15} {incr i} {
   for {set j 1} {[expr ($i+$j)] < 15} {incr j} {
        puts "$sum($i[expr ($i+$j)])\n"
}
}


set min $sum(01)


for {set i 0} {$i < 15} {incr i} {
   for {set j 1} {[expr ($i+$j)] < 15} {incr j} {
        if ([expr {$sum($i[expr ($i+$j)]) <= $min}]) {
                  set min $sum($i[expr ($i+$j)])
                  set k $i
                  set l [expr ($i+$j)]
}
}
}
puts "minimum cost = $min"

for {set i 0} {$i < 15} {incr i} {
     if ([expr {$dis($k$i) <= $dis($l$i)}]) {
            $node($i) color orange
            set null($i) [new Agent/Null]
            $ns attach-agent $node($k) $null($i)
            $ns at 0.4 "$node($i) color orange"
}  else {
             $node($i) color blue
             set null($i) [new Agent/Null]
             $ns attach-agent $node($l) $null($i)
             $ns at 0.4 "$node($i) color blue"
}
} 

   

   $ns at 0.4 "$node($k) label \"CH\""
   $ns at 0.4 "$node($l) label \"CH\""
  

for {set i 0} {$i < 15} {incr i} {
    $ns connect $udp($i) $null($i)
    set cbr($i) [new Application/Traffic/CBR]
    $cbr($i) attach-agent $udp($i)
}

for {set i 1} {$i < 15} {incr i} {
     if {([expr {$i != $k}]) && ([expr {$i != $l}])} {
          $ns at $i "$cbr($i) start"
          $ns at [expr ($i + 0.5)] "$cbr($i) stop"
          
}
}

  

#stop procedure..
proc stop {} {
    global ns tracefd namtrace
    $ns flush-trace
    close $tracefd
    close $namtrace
    exec nam trail.nam &
    
}

$ns at $val(stop) "stop"

$ns run




