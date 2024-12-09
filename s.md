

 Challenge Writeup: **Gift from the Organizer - Claim if You’re Worthy**

### Challenge Overview
Crizz and Luke, two inseparable friends, left behind a treasure locked away in an encrypted disk image. Your mission is to prove your worth by unlocking the image, extracting its contents, and uncovering the hidden flag.

---

### Steps to Solve

#### **Step 1: Download the Encrypted Disk Image**
- Start by downloading the provided disk image file:
  ```bash
  wget https://drive.usercontent.google.com/download?id=1pdyOQdBZiUh6vlQZSXK-HjcCofMw6mOp -O crizz.img
  ```

---

![image](https://github.com/user-attachments/assets/1abc59d2-ee2d-4f7d-8fa8-57592de94066)


#### **Step 2: Decrypt the Disk Image**
- Use the `cryptsetup` command to decrypt the disk image. Get the Disk password from hint:`*********`:
  ```bash
  sudo cryptsetup open crizz.img crizz
  ```
- Enter the password `*********` when prompted. This unlocks the disk image, mapping it to a new device at `/dev/mapper/crizz`.

---

#### **Step 3: Check the Mapped Device**
- Verify the type of the mapped device using the `file` command:
  ```bash
  sudo file -s /dev/mapper/crizz
  ```
- Confirm that the device is ready to be mounted.

---

#### **Step 4: Mount the Decrypted Disk**
- Create a directory to mount the disk:
  ```bash
  sudo mkdir /mnt/crizz
  ```
- Mount the decrypted disk to access its contents:
  ```bash
  sudo mount /dev/mapper/crizz /mnt/crizz
  ```

---

#### **Step 5: Analyze the Mounted Files**
- Navigate to the mounted directory:
  ```bash
  cd /mnt/crizz
  ```
- List the files inside. You should see:
  ```
  key.jpg
  lost+found
  ```
- Copy the `key.jpg` file to your home directory for further analysis:
  ```bash
  cp key.jpg ~/key.jpg
  ```

---

#### **Step 6: Extract Hidden Data from `key.jpg`**
- The challenge mentions the crizz and luke are frds so i guess the  password is `crizzXluke`. Use the `steghide` tool to extract hidden data from the JPEG file:
  ```bash
  steghide extract -sf ~/key.jpg
  ```
- Enter the password `crizzXluke` when prompted. After successful extraction, you will find a new file named `flag.txt` in your current directory.

---

#### **Step 7: Reveal the Flag**
- Open the `flag.txt` file to view the final flag:
  ```bash
  cat flag.txt
  ```
- The flag will be displayed as:
  ```
  crizz_rul3s_th3_gr1d
  ```

---

### Summary of Passwords
1. **Disk image password**: `*********`
2. **`key.jpg` steganographic password**: `crizzXluke`

---

### Tools Used
- **`cryptsetup`**: To decrypt and unlock the disk image.
- **`file`**: To verify the type of the mapped device.
- **`mount`**: To mount the decrypted disk image.
- **`steghide`**: To extract hidden data from the JPEG file.

---

### Final Flag
```
root@localhost{crizz_rul3s_th3_gr1d}



```

![image](https://github.com/user-attachments/assets/122178f3-10c0-4f91-a026-f9a8d5d5ba2c)

---

