import os
import platform
from datetime import datetime

ip_list_file = 'ips.txt'
log_file = 'ping_log.txt'

#ฟังชั่นการเขียน log ของเรานะ
def write_log(message):
    with open(log_file,'a') as file:
        file.write(message + '\n')
        
print("--เริ่มการตรวจสอบสถานะนะครับ;)--")

current_time = datetime.now().strftime("%Y-%m-%d %H:%M:%S")
log_header = f"\n--- ตรวจสอบเมื่อเวลา: {current_time} ---"
print(log_header)
write_log(log_header)

with open(ip_list_file , 'r') as file: 
    for ip in file:
        ip = ip.strip()
        
        param = '-n 1' if  platform.system().lower() == 'windows' else '-c 1'
        command =f"ping {param} {ip}"
        response = os.system(command + " > NUL")

        if response == 0:
            status = f"{ip} is UP"
        else:
            status = f"{ip} is DOWN"
        print(status)
        write_log(status)


print("-- การตรวจสอบเสร็จสิ้นแล้วครับ ผลลัพท์ถูกบันทึกไว้แล้วน้า --")

// after RUN CODE
bank@MacBook-Air-M2 MINI_PROJECT % /usr/local/bin/python3 /Users/bank/Desktop/MINI_PROJECT/ping_tool.py
--เริ่มการตรวจสอบสถานะนะครับ;)--

--- ตรวจสอบเมื่อเวลา: 2025-10-17 14:09:43 ---
8.8.8.8 is UP
192.168.1.1 is DOWN
google.com is UP
10.0.0.99 is DOWN
-- การตรวจสอบเสร็จสิ้นแล้วครับ ผลลัพท์ถูกบันทึกไว้แล้วน้า --
