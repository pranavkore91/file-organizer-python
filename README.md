# file-organizer-python
import os
import shutil

SOURCE_FOLDER = "Downloads"

FILE_TYPES = {
    "Images": [".jpg", ".jpeg", ".png", ".gif"],
    "Documents": [".pdf", ".docx", ".txt"],
    "Videos": [".mp4", ".mkv", ".avi"],
    "Music": [".mp3", ".wav"],
    "Archives": [".zip", ".rar", ".7z"]
}

for filename in os.listdir(SOURCE_FOLDER):
    file_path = os.path.join(SOURCE_FOLDER, filename)

    if not os.path.isfile(file_path):
        continue

    extension = os.path.splitext(filename)[1].lower()

    for folder, extensions in FILE_TYPES.items():
        if extension in extensions:
            destination = os.path.join(SOURCE_FOLDER, folder)
            os.makedirs(destination, exist_ok=True)
            shutil.move(file_path, os.path.join(destination, filename))
            print(f"Moved: {filename} → {folder}")
            break

print("Files organized successfully!")
