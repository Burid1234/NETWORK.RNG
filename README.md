import os
import platform
from datetime import datetime
import requests

ip_list_file = 'ips.txt'
log_file = 'ping_log.txt'
Discord_WEBHOOK_Url = 'https://discord.com/api/webhooks/1428651407069675550/eWVzqrJtXJQM1lVv_GKqSTLCyLBcdsR5fEGjgA6lszCtmSqp8lPMQ_c8F4CUtVy3Qp58'

#ฟังชั่นการเขียน log ของเรานะ
def write_log(message):
    with open(log_file,'a') as file:
        file.write(message + '\n')

def send_discord_webhook(message):

    if not Discord_WEBHOOK_Url:
        print(" -- ยังไม่ได้ตั้งค่า discord นะจ๊ะ!!!")
        return
    
    data = {
         'content': message,
         'username': 'Network Monitor Bot'
     }
    try:
        response = requests.post(Discord_WEBHOOK_Url,json=data)
        if response.status_code != 204:
            print(f" --ส่งdiscordไม่สำเร็จนะจ๊ะ!!!--:{response.text}")
    except Exception as e:
        print(f"-- เกิดข้อผิดพลาดในการส่ง discordนะจ๊ะ!!:{e} --")
        
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
            notification_message =f" แจ้งเตือนด่วนนน \nพบว่า {ip} อยู่ในสถานนะDOWN!!"
            send_discord_webhook(notification_message)
        print(status)
        write_log(status)

print("-- การตรวจสอบเสร็จสิ้นแล้วครับ ผลลัพท์ถูกบันทึกไว้แล้วน้า --")

// after for run code 

-- ตรวจสอบเมื่อเวลา: 2025-10-17 16:19:28 ---
8.8.8.8 is UP
192.168.1.1 is DOWN
google.com is UP
10.0.0.99 is DOWN
-- การตรวจสอบเสร็จสิ้นแล้วครับ ผลลัพท์ถูกบันทึกไว้แล้วน้า --
