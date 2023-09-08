import psutil
import time
import datetime
import socket
# Function to get current system information
def get_system_info():
    timestamp = datetime.datetime.now().strftime("%Y-%m-%d %H:%M:%S")
    cpu_usage = psutil.cpu_percent()
    logical_cpus = psutil.cpu_count(logical=True)
    used_memory = psutil.virtual_memory().percent
    used_disk_space = psutil.disk_usage('/').percent
    current_host_ip = socket.gethostbyname(socket.gethostname())

    return (timestamp, cpu_usage, logical_cpus, used_memory, used_disk_space,current_host_ip)

# Function to write system information to a log file
def write_to_logfile(filename, data):
    with open(filename, 'a') as file:
        file.write(','.join(map(str, data)) + '\n')

# Function to create a notification log file
def create_notification_log(filename):
    with open(filename, 'w') as file:
        file.write("The System is running a low memory.\n")

if __name__ == "__main__":
    

    current_date = datetime.datetime.now().strftime("%Y-%m-%d")
    log_filename = f"{current_date}-pub.log"
    notification_filename = f"{current_date}-notification.log"

    while True:
        system_info = get_system_info()
        write_to_logfile(log_filename, system_info)

    
        if system_info[3] > 80: # 80==> memory_threshold
            
            create_notification_log(notification_filename)
            print(f"Low memory notification: {notification_filename} created.")

        time.sleep(5)     # 5 ==> monitoring_interval

