# 🖥️ **Week 2: Linux System Administration & Automation**  
**Welcome to Week 2 of the 90 Days of DevOps - 2025 Edition!**  

This week, we dive deep into **Linux system administration and automation**, covering essential topics such as:  
✅ **User & Group Management**  
✅ **File & Directory Permissions**  
✅ **Log Analysis & Processing**  
✅ **Volume Management & Disk Usage**  
✅ **Process Monitoring & Control**  
✅ **Shell Scripting for Automation**  

By mastering these topics, you'll build a solid foundation in **Linux administration**, an essential skill for every **DevOps engineer**.  

---

## 🚀 **Project: DevOps Linux Server Monitoring & Automation**  
Imagine you’re managing a **Linux-based production server** and need to ensure **user management, logs, processes, and storage are well-maintained**.  

You'll perform **real-world system administration tasks**, including:  
🔹 **User creation & permission management**  
🔹 **Analyzing & filtering system logs**  
🔹 **Managing storage volumes**  
🔹 **Automating backups using shell scripts**  

---

## 📌 **Tasks & Commands**  

### 🔹 **1️⃣ User & Group Management**  
📖 Learn about **Linux users, groups, and permissions** (`/etc/passwd`, `/etc/group`).  

[Notes](https://github.com/Sai-kiran-7272/12-Weeks-of-DevOps/blob/main/Week%202%3A%20Linux%20Challenge/NOTES/User%20%26%20Group%20Management.md)

🛠 **Task:**  
- Create a user **devops_user** and add them to a group **devops_team**  
  ```bash
  sudo useradd -m -s /bin/bash devops_user
  sudo groupadd devops_team
  sudo usermod -aG devops_team devops_user
  ```
- Set a password and grant **sudo access**  
  ```bash
  sudo passwd devops_user
  sudo usermod -aG sudo devops_user
  ```
- Restrict **SSH login** for certain users in `/etc/ssh/sshd_config`  
  ```bash
  echo "DenyUsers test_user" | sudo tee -a /etc/ssh/sshd_config
  sudo systemctl restart sshd
  
  ```

---

### 🔹 **2️⃣ File & Directory Permissions**  
📖 Understand **ownership & permission levels** (`chmod`, `chown`, `ls -l`). 

[Notes](https://github.com/Sai-kiran-7272/12-Weeks-of-DevOps/blob/main/Week%202%3A%20Linux%20Challenge/NOTES/File%20%26%20Directory%20Permission.md)

🛠 **Task:**  
- Create a **workspace** directory and a file  
  ```bash
  mkdir /devops_workspace
  touch /devops_workspace/project_notes.txt
  ```
- Set permissions:  
  ✅ **Owner** can edit, **Group** can read, **Others** have no access  
  ```bash
  chmod 640 /devops_workspace/project_notes.txt
  ```
- Verify using:  
  ```bash
  ls -l /devops_workspace/project_notes.txt
  ```

---

### 🔹 **3️⃣ Log File Analysis with AWK, Grep & Sed**  
📖 Learn **log file processing** using **grep, awk, and sed**. 

[Notes](https://github.com/Sai-kiran-7272/12-Weeks-of-DevOps/blob/main/Week%202%3A%20Linux%20Challenge/NOTES/Log%20File%20Analysis.md) | [Log File](https://github.com/Sai-kiran-7272/12-Weeks-of-DevOps/blob/main/Week%202%3A%20Linux%20Challenge/My_Linux.log)

🛠 **Task:**  
- Download the sample log file:  
  ```bash
  wget https://raw.githubusercontent.com/loghub/My_Linux.log -O My_Linux.log
  ```
- Extract insights using:  
  - **Find all occurrences of "error"**  
    ```bash
    grep -i "error" My_Linux.log
    ```
  - **Extract timestamps and log levels using awk**  
    ```bash
    awk '{print $1, $2, $3}' My_Linux.log
    ```
  - **Replace all IP addresses with `[REDACTED]` for security**  
    ```bash
    sed -E 's/[0-9]+\.[0-9]+\.[0-9]+\.[0-9]+/[REDACTED]/g' My_Linux.log
    ```
  - **Find the most frequent log entries**  
    ```bash
    awk '{print $3}' My_Linux.log | sort | uniq -c | sort -nr | head -10
    ```

---

### 🔹 **4️⃣ Volume Management & Disk Usage**  
📖 Learn **disk partitions, mounting, and storage management**.  

[Notes](https://github.com/Sai-kiran-7272/12-Weeks-of-DevOps/blob/main/Week%202%3A%20Linux%20Challenge/NOTES/Volume%20Management%20%26%20Disk%20Usage.md)

🛠 **Task:**  
- Create a new directory:  
  ```bash
  mkdir /mnt/devops_data
  ```
- Mount a new volume (loop device for local practice):  
  ```bash
  sudo mount /dev/sdb1 /mnt/devops_data
  ```
- Verify disk usage:  
  ```bash
  df -h | grep devops_data
  ```
- Check mounted volumes:  
  ```bash
  mount | grep devops_data
  ```

---

### 🔹 **5️⃣ Process Management & Monitoring**  
📖 Learn **how to monitor and control running processes**.  

🛠 **Task:**  
- Start a background process:  
  ```bash
  ping google.com > ping_test.log &
  ```
- Monitor processes using:  
  ```bash
  ps aux | grep ping
  top
  htop
  ```
- Kill a process:  
  ```bash
  kill -9 <PID>
  ```

---

### 🔹 **6️⃣ Automate Backups with Shell Scripting**  
📖 Learn **automation with shell scripts & cron jobs**.  

🛠 **Task:**  
- Write a backup script:  
  ```bash
  #!/bin/bash
  tar -czf /backups/backup_$(date +%F).tar.gz /devops_workspace
  echo -e "\e[32mBackup successful!\e[0m"
  ```
- Make it executable:  
  ```bash
  chmod +x backup.sh
  ```
- Schedule with cron:  
  ```bash
  crontab -e
  ```
  Add the following line to run the script daily at midnight:  
  ```bash
  0 0 * * * /path/to/backup.sh
  ```

---

## 🎯 **Bonus Tasks (Optional 🚀)**  
💡 **Enhance your Linux skills with these extra challenges:**  
✅ Find the **top 5 most common log messages** in `Linux_2k.log`  
   ```bash
   awk '{print $3}' Linux_2k.log | sort | uniq -c | sort -nr | head -5
   ```
✅ List all files **modified in the last 7 days**  
   ```bash
   find /path/to/directory -type f -mtime -7
   ```
✅ Write a script to extract only **ERROR and WARNING** logs  
   ```bash
   grep -E "ERROR|WARNING" Linux_2k.log > filtered_logs.txt
   ```

---

## 📢 **How to Submit Your Work**  
📌 **Step 1:** Write a **LinkedIn post** summarizing your **Week 2 experience**.  
📌 **Step 2:** Include **screenshots or logs** showcasing your completed tasks.  
📌 **Step 3:** Use **hashtags**: `#90DaysOfDevOps #LinuxAdmin #DevOps`  
📌 **Step 4:** Share any **blog posts, GitHub repos, or articles** you create.  

---

## 📚 **Resources to Get Started**  
🔹 [Linux Command Cheat Sheet](https://www.geeksforgeeks.org/linux-commands/)  

---

## 📝 **Example LinkedIn Submission Post**  
> **Week 2 of #90DaysOfDevOps2025 done!** 🏆  
> ✅ Managed users & SSH access  
> ✅ Set up permissions & volumes  
> ✅ Analyzed logs using AWK & grep  
> ✅ Automated backups with a shell script  
>  
> Check out my blog here: **[Your Blog/GitHub Link]**  
>  
> #Linux #SysAdmin #DevOps #Learn2gether&Grow2gether  

---

💡 **Let’s keep growing together!** 🚀  
Tag me in your posts and use **#Learn2gether&Grow2gether** to connect with the DevOps community.  

---
