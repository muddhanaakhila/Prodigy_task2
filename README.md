from PIL import Image
import numpy as np
import random

# Function to encrypt the image using pixel manipulation
def encrypt_image(image_path, key):
    # Open the image and convert it to RGB
    img = Image.open(image_path)  # Image path as string should work correctly
    img = img.convert('RGB')
    
    # Convert the image into a numpy array for pixel manipulation
    pixels = np.array(img)
    
    # Apply pixel manipulation (XOR operation with a key)
    encrypted_pixels = pixels ^ key
    
    # Convert the manipulated pixels back to an image
    encrypted_image = Image.fromarray(encrypted_pixels.astype(np.uint8))
    
    # Save the encrypted image
    encrypted_image.save('encrypted_image.png')
    print("Image encrypted successfully and saved as 'encrypted_image.png'")

# Function to decrypt the image using the same key
def decrypt_image(encrypted_image_path, key):
    # Open the encrypted image
    img = Image.open(encrypted_image_path)
    img = img.convert('RGB')
    
    # Convert the image into a numpy array for pixel manipulation
    pixels = np.array(img)
    
    # Apply XOR operation with the same key to decrypt
    decrypted_pixels = pixels ^ key
    
    # Convert the manipulated pixels back to an image
    decrypted_image = Image.fromarray(decrypted_pixels.astype(np.uint8))
    
    # Save the decrypted image
    decrypted_image.save('decrypted_image.png')
    print("Image decrypted successfully and saved as 'decrypted_image.png'")

# Generate a random key for encryption/decryption
def generate_key():
    # Generate a random key (using a simple value like 122, but you can make this complex)
    return random.randint(0, 255)

# Main function to run the encryption and decryption
def main():
    image_path = input("Enter the image path for encryption: ")
    
    # Handle spaces in the image path by ensuring proper formatting
    image_path = image_path.strip()  # Remove any extra spaces
    
    key = generate_key()
    print(f"Using encryption key: {key}")
    
    encrypt_image(image_path, key)
    
    encrypted_image_path = 'encrypted_image.png'
    decrypt_image(encrypted_image_path, key)

if __name__ == "__main__":
    main()
