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
