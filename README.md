
from PIL import Image
import numpy as np

def encrypt_image(input_path, output_path, key):
    # Open the image
    image = Image.open(input_path)
    # Convert image to numpy array
    image_array = np.array(image)
    
    # Encrypt the image by adding the key
    encrypted_array = (image_array + key) % 256
    encrypted_image = Image.fromarray(encrypted_array.astype('uint8'))
    
    # Save the encrypted image
    encrypted_image.save(output_path)
    print(f"Image encrypted and saved to {output_path}")

def decrypt_image(input_path, output_path, key):
    # Open the encrypted image
    encrypted_image = Image.open(input_path)
    # Convert image to numpy array
    encrypted_array = np.array(encrypted_image)
    
    # Decrypt the image by subtracting the key
    decrypted_array = (encrypted_array - key) % 256
    decrypted_image = Image.fromarray(decrypted_array.astype('uint8'))
    
    # Save the decrypted image
    decrypted_image.save(output_path)
    print(f"Image decrypted and saved to {output_path}")

# Example usage
encryption_key = 50
encrypt_image('original_image.png', 'encrypted_image.png', encryption_key)
decrypt_image('encrypted_image.png', 'decrypted_image.png', encryption_key)
