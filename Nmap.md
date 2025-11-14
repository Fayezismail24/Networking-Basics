# Nmap Commands

## 1. Basic Scan
This is the most basic `nmap` scan to detect open ports on a target.

`nmap <target_ip>`

## 2. Scan Multiple IPs or a Range of IPs

`nmap 192.168.1.1 192.168.1.2`

`nmap 192.168.1.1-50`

## 3. Scan All Hosts on a Network

`nmap -sn [Network/Subnet]`

`nmap -sn 192.168.1.0/24`

## 4. Show all Host IP

 `nmap -sn [Network/Subnet] | grep "Nmap scan report" | cut -d " " -f 5` 



## 5. Scan Multiple Port(s)

`nmap -p 22,80,443 <target_ip>`

## 6.Scan all 65535 ports of the target
`nmap -p- <target_ip>`

## 7. Service Version Detection

`nmap -sV <target_ip>`

## 8. Operating System Detection
`nmap -O <target_ip>`















