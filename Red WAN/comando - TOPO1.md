# R1

## configurando ip address
```
configure terminal
int f0/0
ip address 10.8.0.1 255.255.255.248
no shutdown
exit
int f2/0
ip address 10.8.0.17 255.255.255.248
no shutdown
exit
```

## configurando rip
```
configure terminal
router rip
version 2
network 10.8.0.0
network 10.8.0.16
end
```

## configurando GLBP Activo R1
```
int f0/0
glbp 1 ip 10.8.0.46
glbp 1 preempt
glbp 1 priority 150
glbp 1 load-balancing round-robin
```


# R2

## configurando ip address
```
configure terminal
int f0/0
ip address 10.8.0.9 255.255.255.248
no shutdown
exit
int f2/0
ip address 10.8.0.25 255.255.255.248
no shutdown
exit
```

## configurando rip
```
configure terminal
router rip
version 2
network 10.8.0.8
network 10.8.0.24
end
```

## configurando GLBP pasivo R2
```
int f0/0
glbp 1 ip 10.8.0.46
glbp 1 load-balancing round-robin
```

# R3

## configurando ip address
```
configure terminal
int f0/0
ip address 10.8.0.2 255.255.255.248
no shutdown
exit
int f2/0
ip address 10.8.0.33 255.255.255.248
no shutdown
exit
```


## configurando rip
```
configure terminal
router rip
version 2
network 10.8.0.0
network 10.8.0.32
end
```

## configurando HSRP pasivo R3
```
int f0/0
standby 1 ip 10.8.0.46
```


# R4

## configurando ip address
```
configure terminal
int f0/0
ip address 10.8.0.10 255.255.255.248
no shutdown
exit
int f2/0
ip address 10.8.0.41 255.255.255.248
no shutdown
exit
```

## configurando rip
```
configure terminal
router rip
version 2
network 10.8.0.8
network 10.8.0.40
end
```

## configurando HSRP Activo R4
```
int f0/0
standby 1 ip 10.8.0.46
standby 1 priority 150
standby 1 preempt
```




configure terminal
router rip
version 2
network 10.8.0.0
network 10.8.0.8
network 10.8.0.16
network 10.8.0.24
network 10.8.0.32
network 10.8.0.40
end


