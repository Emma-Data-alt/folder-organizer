import os
import shutil

# 🔧 Set the folder path you want to organize
folder_path = 'C:/Users/emmap/Desktop/Folder_organizer'  # 👈 change this if needed

# 🗂️ Dictionary for common file type categories
file_types = {
    'Images': ['.jpg', '.jpeg', '.png', '.gif'],
    'Documents': ['.pdf', '.docx', '.txt'],
    'Audio': ['.mp3', '.wav'],
    'Videos': ['.mp4', '.mov'],
    'Archives': ['.zip', '.rar'],
    'Scripts': ['.py', '.js', '.ipynb'],
    'Other': []
}

# 🚀 Go through each file in the folder
for filename in os.listdir(folder_path):
    file_path = os.path.join(folder_path, filename)
    if os.path.isfile(file_path):
        ext = os.path.splitext(filename)[1].lower()
        moved = False

        for folder, extensions in file_types.items():
            if ext in extensions:
                target_dir = os.path.join(folder_path, folder)
                os.makedirs(target_dir, exist_ok=True)
                shutil.move(file_path, os.path.join(target_dir, filename))
                moved = True
                break

        if not moved:
            other_dir = os.path.join(folder_path, 'Other')
            os.makedirs(other_dir, exist_ok=True)
            shutil.move(file_path, os.path.join(other_dir, filename))

print("✨ Folder organized successfully!")

