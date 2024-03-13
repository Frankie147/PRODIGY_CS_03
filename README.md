from PIL import Image

def encrypt_image(image_path, key):
    """
    Encrypts an image using XOR operation with a given key.
    
    Parameters:
        image_path (str): Path to the input image file.
        key (int): Encryption key.
    
    Returns:
        encrypted_image (PIL.Image): Encrypted image.
    """
    # Open the input image
    img = Image.open(image_path)
    
    # Get the pixel data
    pixels = img.load()
    
    # Encrypt each pixel using XOR operation with the key
    width, height = img.size
    for x in range(width):
        for y in range(height):
            r, g, b = pixels[x, y]
            pixels[x, y] = r ^ key, g ^ key, b ^ key
    
    return img

def decrypt_image(image_path, key):
    """
    Decrypts an encrypted image using XOR operation with a given key.
    
    Parameters:
        image_path (str): Path to the encrypted image file.
        key (int): Encryption key used during encryption.
    
    Returns:
        decrypted_image (PIL.Image): Decrypted image.
    """
    # Open the encrypted image
    img = Image.open(image_path)
    
    # Get the pixel data
    pixels = img.load()
    
    # Decrypt each pixel using XOR operation with the key
    width, height = img.size
    for x in range(width):
        for y in range(height):
            r, g, b = pixels[x, y]
            pixels[x, y] = r ^ key, g ^ key, b ^ key
    
    return img

def main():
    # Image file paths
    input_image_path = "input_image.jpg"
    encrypted_image_path = "encrypted_image.jpg"
    
    # Encryption key
    key = 123
    
    # Encrypt the image
    encrypted_img = encrypt_image(input_image_path, key)
    encrypted_img.save(encrypted_image_path)
    print("Image encrypted successfully.")
    
    # Decrypt the image
    decrypted_img = decrypt_image(encrypted_image_path, key)
    decrypted_img.show()
    print("Image decrypted successfully.")

if __name__ == "__main__":
    main()
