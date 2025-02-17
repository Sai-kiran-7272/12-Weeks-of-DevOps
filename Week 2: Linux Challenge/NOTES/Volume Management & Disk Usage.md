# **📌 In-Depth Guide to Volume Management & Disk Usage in Linux**  

## **🔍 Why is Volume Management Important in DevOps?**  

In Linux, storage management is crucial for system stability and efficiency. As a DevOps engineer, you will often deal with:  

✅ **Disk partitions** – Dividing storage into sections.  
✅ **Mounting volumes** – Attaching storage devices to directories.  
✅ **Monitoring disk usage** – Checking available space and usage.  

Let’s break down each command and understand its function in detail. 🚀  

---

## **📌 Step 1: Creating a Directory for Mounting**  

### **Command:**  
```bash
mkdir /mnt/devops_data
```  

### **Explanation:**  
- `mkdir` → Creates a new **directory** (folder) in Linux.  
- `/mnt/devops_data` → This is the directory we will use to **mount** our storage.  

### **Why is This Important?**  
- **Mounting links a storage device to a directory.**  
- `/mnt` is commonly used for **temporary storage mounts** (e.g., external drives).  

### **Bonus: Check If the Directory Already Exists Before Creating It**  
```bash
[ ! -d /mnt/devops_data ] && mkdir /mnt/devops_data
```  
- `! -d` → Checks if the directory **does NOT exist**.  
- `&&` → Runs the next command (`mkdir`) **only if the condition is true**.  

---

## **📌 Step 2: Mounting a New Volume**  

### **Command:**  
```bash
sudo mount /dev/sdb1 /mnt/devops_data
```  

### **Explanation:**  
- `sudo` → Runs the command **with admin (root) privileges**, as mounting requires higher permissions.  
- `mount` → **Attaches** a storage device to a directory.  
- `/dev/sdb1` → Represents the **storage partition** we want to mount.  
- `/mnt/devops_data` → The **mount point** (directory where the storage will be accessible).  

### **Understanding `/dev/sdb1`**  
- Linux **identifies storage devices** as `/dev/sdX`:  
  - `/dev/sda` → First disk  
  - `/dev/sdb` → Second disk  
- `1` in `/dev/sdb1` means **the first partition** on the second disk.  

### **Bonus: How to Mount an ISO File as a Virtual Disk?**  
```bash
sudo mount -o loop ubuntu.iso /mnt/devops_data
```  
- `-o` → Specifies **mount options**.  
- `loop` → Treats the **ISO file as a virtual disk**.  

---

## **📌 Step 3: Checking Disk Space Usage**  

### **Command:**  
```bash
df -h | grep devops_data
```  

### **Explanation:**  
- `df` → Displays **disk space usage** for all mounted file systems.  
- `-h` → Outputs results in **human-readable format** (MB, GB instead of bytes).  
- `| grep devops_data` → Filters output to **only show the mounted volume**.  

### **Understanding `df -h` Output:**  
```
Filesystem      Size  Used Avail Use% Mounted on
/dev/sdb1      100G   20G   80G  20%  /mnt/devops_data
```  
- **Size** → Total storage space of the volume (**100GB**).  
- **Used** → Space already occupied (**20GB**).  
- **Avail** → Free space left (**80GB**).  
- **Mounted on** → Directory where the volume is attached (**/mnt/devops_data**).  

### **Breakdown of `df` Options:**  
| Option | Description |
|--------|------------|
| `-h` | Displays output in **human-readable format** (MB, GB, TB). |
| `-T` | Shows **file system type** (e.g., ext4, xfs, ntfs). |
| `-i` | Displays information about **inodes** instead of storage. |

### **Bonus: Check Disk Usage of a Specific Directory**  
```bash
du -sh /mnt/devops_data
```  
- `du` → Stands for **Disk Usage**, used to check folder sizes.  
- `-s` → Shows only the **summary** (total size).  
- `-h` → Formats output in **human-readable format**.  

---

## **📌 Step 4: Checking Mounted Volumes**  

### **Command:**  
```bash
mount | grep devops_data
```  

### **Explanation:**  
- `mount` → Displays **all mounted storage devices** and their mount points.  
- `| grep devops_data` → Filters output to show only the **specific mounted volume**.  

### **Example Output:**  
```
/dev/sdb1 on /mnt/devops_data type ext4 (rw,relatime,data=ordered)
```  
- `/dev/sdb1` → The **storage partition that is mounted**.  
- `/mnt/devops_data` → The **directory where it is mounted**.  
- `type ext4` → The **filesystem format** (EXT4 is a common Linux filesystem).  
- `(rw,relatime,data=ordered)` → **Mount options**:  
  - `rw` → **Read & Write access**.  
  - `relatime` → Optimized **timestamp updates**.  
  - `data=ordered` → Ensures **data is written in a safe order**.  

### **Bonus: List All Mounted File Systems in a Clear Format**  
```bash
lsblk -f
```  
- `lsblk` → Lists all **storage devices and partitions**.  
- `-f` → Displays **file system type and mount points**.  

---

## **📌 Summary of Commands and Their Purpose**  

| **Command** | **Purpose** |
|------------|------------|
| `mkdir /mnt/devops_data` | Creates a directory for mounting the volume. |
| `sudo mount /dev/sdb1 /mnt/devops_data` | Mounts a storage device to a directory. |
| `df -h | grep devops_data` | Checks disk space usage of the mounted volume. |
| `mount | grep devops_data` | Displays information about the mounted volume. |
| `du -sh /mnt/devops_data` | Shows the total size of files in the directory. |
| `lsblk -f` | Lists all storage devices and their mount points. |

---

## **📌 Additional Volume Management Commands for Practice**  

### **Unmount a Volume**  
To detach the mounted volume:  
```bash
sudo umount /mnt/devops_data
```  
- `umount` → Unmounts the storage device from the directory.  

### **Check Available Disk Partitions**  
To view all disk partitions, use:  
```bash
lsblk
```
- `lsblk` → Lists **all storage devices and their partitions**.  

### **Check Free Space on All Disks**  
```bash
df -h
```  
- `df -h` → Shows **available and used storage on all mounted devices**.  

---

## **📌 Key Takeaways**  

✅ **Mounting allows Linux to access storage devices and partitions.**  
✅ **Checking disk usage helps prevent low storage issues.**  
✅ **Monitoring mounted volumes is crucial for troubleshooting storage problems.**  

🚀 **Next Steps:** Try mounting different types of storage, including USB drives, network storage (NFS), or cloud-based volumes!  

Got questions? Let’s discuss! 😊 Happy learning! 🎯
