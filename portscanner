import socket
from threading import Thread

def port_scan(target, port):
    s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    s.settimeout(1)  # Set socket timeout to 1 second
    result = s.connect_ex((target, port))
    if result == 0:
        print("Port: " + str(port) + " Open")
    s.close()

def scan_range(target, start_port, end_port):
    for port in range(start_port, end_port + 1):
        port_scan(target, port)

print("Please enter an IP Address to scan.")
target = input("> ")

print("*" * 40)
print("* Scanning: " + target + " *")
print("*" * 40)

# Define the number of threads
num_threads = 10  # You can adjust this number based on your system's capabilities

# Calculate the ports range for each thread
ports_per_thread = 1024 // num_threads
start_port = 1
end_port = ports_per_thread

# Create and start threads
threads = []
for _ in range(num_threads):
    thread = Thread(target=scan_range, args=(target, start_port, end_port))
    threads.append(thread)
    thread.start()
    
    # Update port range for the next thread
    start_port = end_port + 1
    end_port = min(end_port + ports_per_thread, 1024)

# Wait for all threads to finish
for thread in threads:
    thread.join()
