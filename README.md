# python-port-scanner
import socket

# Function to scan a port
def scan_port(target, port):
    sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    sock.settimeout(1)

    result = sock.connect_ex((target, port))

    if result == 0:
        return "OPEN"
    else:
        return "CLOSED"

# Ask user for target
target = input("Enter IP address or website: ")

# Ask user for ports
ports = input("Enter ports separated by commas: ")

# Convert ports into a list
port_list = ports.split(",")

# Open result file
file = open("results.txt", "w")

print("\nScanning target:", target)
print("-" * 30)

# Loop through ports
for port in port_list:
    port = int(port)

    status = scan_port(target, port)

    output = f"Port {port}: {status}"

    print(output)

    # Save to file
    file.write(output + "\n")

file.close()

print("\nResults saved to results.txt")
