import os
import random
import string
import tempfile

def generate_random_data(size):
    """Generate random bytes for overwriting."""
    return os.urandom(size)

def wipe_free_space(overwrite_passes=3):
    """Overwrite free space on the current drive to make recovery harder."""
    temp_dir = tempfile.gettempdir()
    filename = os.path.join(temp_dir, "wipe_temp_file.bin")

    print("[*] Wiping free space. This may take a while...")

    try:
        with open(filename, 'wb') as f:
            # Fill up disk space with random data
            block_size = 1024 * 1024  # 1MB blocks
            while True:
                f.write(generate_random_data(block_size))
    except OSError:
        # Disk is full
        pass

    for pass_num in range(overwrite_passes):
        print(f"[*] Overwrite pass {pass_num + 1}/{overwrite_passes}")
        with open(filename, 'r+b') as f:
            f.seek(0)
            while True:
                try:
                    f.write(generate_random_data(block_size))
                except:
                    break

    os.remove(filename)
    print("[*] Free space overwritten and temporary file deleted.")

if __name__ == "__main__":
    wipe_free_space()
