# SCT_PY_02
IMAGE ENCRYPTION TOOL 
from PIL import Image

# usage
def encrypt_image(image_path, operation="swap", shift=10):
    """Encrypts an image using the specified operation.

    Args:
        image_path: Path to the image file.
        operation: Encryption operation (swap, add, subtract, multiply, divide).
        shift: Shift value for mathematical operations.
    """
    img = Image.open(image_path)
    width, height = img.size
    pixels = img.load()

    for x in range(width):
        for y in range(height):
            r, g, b = pixels[x, y]

            if operation == "swap":
                # Swap pixel values with neighboring pixels
                if x > 0:
                    r, g, b = pixels[x - 1, y]
                if y > 0:
                    r, g, b = pixels[x, y - 1]

            elif operation == "add":
                r = (r + shift) % 256
                g = (g + shift) % 256
                b = (b + shift) % 256

                # Implement other operations like subtract, multiply, divide

            pixels[x, y] = (r, g, b)

    img.save("encrypted_image.jpg")


# usage
def decrypt_image(image_path, operation="swap", shift=10):
    """Decrypts an encrypted image.

    Args:
        image_path: Path to the encrypted image file.
        operation: Decryption operation (swap, add, subtract, multiply, divide).
        shift: Shift value for mathematical operations.
    """
    # Decryption is essentially the reverse of encryption
    # For example, to decrypt a swapped image, swap pixels again
    # For mathematical operations, use the inverse operation (subtract, divide, etc.)
    # Implement decryption logic based on the chosen operation


if __name__ == "__main__":
    image_path = "your_image.jpg"
    operation = "swap"  # Change to "add", "subtract", "multiply", or "divide" as needed
    shift = 10

    encrypt_image(image_path, operation, shift)
    decrypt_image("encrypted_image.jpg", operation, shift)
