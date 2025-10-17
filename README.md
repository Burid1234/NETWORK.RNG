import os
import platform

ip_list_file = 'ips.txt'
print("--เริ่มการทำงานแล้วนะครับ--")

with open(ip_list_file , 'r') as file: 
    for ip in file:
        ip = ip.strip()
        
        param = '-n 1' if  platform.system().lower() == 'windows' else '-c 1'
        command =f"ping {param} {ip}"
        response = os.system(command)

        if response == 0:
            print(f"{ip} is UP")
        else:
            print(f"{ip} is DOWN")

print("--การตรวจสอบเสร็จสิ้นแล้วครับ--")

// after to RUN code python dude^^
usr/local/bin/python3 /Users/bank/Desktop/MINI_PROJECT/ping_tool.py
bank@MacBook-Air-M2 MINI_PROJECT % /usr/local/bin/python3 /Users/bank/Desktop/MINI_PROJECT/ping_tool.py
--เริ่มการทำงานแล้วนะครับ--
PING 8.8.8.8 (8.8.8.8): 56 data bytes
64 bytes from 8.8.8.8: icmp_seq=0 ttl=251 time=15.468 ms

--- 8.8.8.8 ping statistics ---
1 packets transmitted, 1 packets received, 0.0% packet loss
round-trip min/avg/max/stddev = 15.468/15.468/15.468/0.000 ms
8.8.8.8 is UP
PING 192.168.1.1 (192.168.1.1): 56 data bytes

--- 192.168.1.1 ping statistics ---
1 packets transmitted, 0 packets received, 100.0% packet loss
192.168.1.1 is DOWN
PING google.com (142.250.204.142): 56 data bytes
64 bytes from 142.250.204.142: icmp_seq=0 ttl=251 time=14.934 ms

--- google.com ping statistics ---
1 packets transmitted, 1 packets received, 0.0% packet loss
round-trip min/avg/max/stddev = 14.934/14.934/14.934/0.000 ms
google.com is UP
PING 10.0.0.99 (10.0.0.99): 56 data bytes

--- 10.0.0.99 ping statistics ---
1 packets transmitted, 0 packets received, 100.0% packet loss
10.0.0.99 is DOWN
--การตรวจสอบเสร็จสิ้นแล้วครับ--
