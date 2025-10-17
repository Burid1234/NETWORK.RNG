import os
ip_list_file = 'ips.txt'
print("--เริ่มการทำงานแล้วนะครับ--")
with open(ip_list_file , 'r') as file: #จะเปิดไฟล์
    for ip in file:
        ip = ip.strip()
        print(f"กำลังตรวจสอบ: {ip}")

print("--การตรวจสอบเสร็จสิ้นแล้วครับ--")
