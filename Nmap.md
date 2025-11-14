# Nmap Commands

## 1. Basic Scan
This is the most basic `nmap` scan to detect open ports on a target.

`nmap <target_ip>`

## 2. Scan Multiple IPs or a Range of IPs

`nmap 192.168.1.1 192.168.1.2`

`nmap 192.168.1.1-50`

## 3. Scan Multiple Port(s)

`nmap -p 22,80,443 <target_ip>`

## 4.Scan all 65535 ports of the target
`nmap -p- <target_ip>`

## 5. Service Version Detection

`nmap -sV <target_ip>`

## 6. Operating System Detection
`nmap -O <target_ip>`















