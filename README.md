# How-to-encrypt-any-file-using-ISH-SHELL
nano secure_storage.py
put this code:
from cryptography.fernet import Fernet
import os

# Generate a new key
def generate_key():
    key = Fernet.generate_key()
    with open("secret.key", "wb") as key_file:
        key_file.write(key)

# Load the key from the file
def load_key():
    return open("secret.key", "rb").read()

# Encrypt a file
def encrypt_file(file_name):
    key = load_key()
    fernet = Fernet(key)

    with open(file_name, "rb") as file:
        original = file.read()

    encrypted = fernet.encrypt(original)

    with open(file_name, "wb") as encrypted_file:
        encrypted_file.write(encrypted)

# Decrypt a file
def decrypt_file(file_name):
    key = load_key()
    fernet = Fernet(key)

    with open(file_name, "rb") as encrypted_file:
        encrypted = encrypted_file.read()

    decrypted = fernet.decrypt(encrypted)

    with open(file_name, "wb") as decrypted_file:
        decrypted_file.write(decrypted)

# Main menu
if __name__ == "__main__":
    if not os.path.exists("secret.key"):
        generate_key()
        print("Encryption key has been generated and saved to secret.key")

    choice = input("Choose: 1 to encrypt a file, 2 to decrypt a file: ")
    file_name = input("Enter the file name: ")

    if choice == "1":
        encrypt_file(file_name)
        print(f"The file {file_name} has been encrypted")
    elif choice == "2":
        decrypt_file(file_name)
        print(f"The file {file_name} has been decrypted")
    else:
        print("Invalid option!")


        python3 secure_storage.py
        
