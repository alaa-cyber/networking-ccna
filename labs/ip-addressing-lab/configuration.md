enable
configure terminal

hostname R1

interface g0/0
ip address 15.255.255.254 255.0.0.0
no shutdown

interface g0/1
ip address 182.98.255.254 255.255.0.0
no shutdown

interface g0/2
ip address 201.191.20.254 255.255.255.0
no shutdown

end
write memory
