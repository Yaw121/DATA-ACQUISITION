## PREPARING A TARGET DRIVE FOR ACQUISITION IN LINUX ##


## Objective
This repository documents a lab focused on data acquisition techniques using Linux tools. The lab is designed to provide hands-on experience in preparing target drives and acquiring data securely and efficiently, ensuring data integrity for forensic purposes.


## Key Activities
1. **Preparing a Target Drive for Acquisition in Linux**
   - Use Linux utilities to prepare a target drive for data acquisition.
   - Format and mount the drive to ensure it is ready for forensic imaging.

2. **Acquiring Data with `dd` in Linux**
   - Utilize the `dd` command to create a forensic image of the target drive.
   - Verify the integrity of the acquired image using hash values (e.g., MD5, SHA-256).

3. **Reporting and Documentation**
   - Document each step in the data acquisition process.
   - Generate a report summarizing the methods, tools, and results.

## Tools and Technologies Used
- **Linux Command Line:** For executing data acquisition tasks.
- **dd Utility:** Tool for creating bit-by-bit forensic images.
- **Hashing Tools:** Tools like `md5sum` and `sha256sum` for verifying data integrity.
- **Target Drive:** Storage media for forensic imaging and analysis.

## Skills Acquired
- Proficiency in preparing storage drives for forensic data acquisition.
- Expertise in using `dd` to create forensic images.
- Knowledge of hashing techniques to verify the integrity of acquired data.
- Experience in documenting forensic acquisition processes.



## STEPS ##
<details>
<summary><b>Task 1 - Prepare Linux File System</b></summary>

First, I prepared a Windows FAT32 file system by logging into Linux and Opening the terminal.

1. To use a graphical user interface application for preparing disk storage, type: gparted in the termainl and press Enter.
![image](https://github.com/user-attachments/assets/e79737c8-3aa3-4bb4-bf6b-ba27cae91408)


2. The /dev/sda - GParted window is open. Information about the partitioning details of selected device /dev/sda is displayed in the middle pane.
![image](https://github.com/user-attachments/assets/02779150-ca65-4d9a-a181-1a801d876ab1)

 
3. On the far right corner, access the drop-down list and change it to /dev/sdb.
 ![image](https://github.com/user-attachments/assets/c06a4d8c-8226-44d9-969b-5d61a709bcf5)


4. The selection switches to /dev/sdb, which I’ll be using to prepare a volume compatible with another system, such as FAT32.To proceed, right-click on /dev/sdb1 and choose Unmount from the context menu to ensure the partition is not in use before making any changes.
  ![image](https://github.com/user-attachments/assets/90157e19-5b04-442b-bba6-0dba3ad94d37)


5. Right-click on /dev/sdb1 and choose Delete to remove the existing partition. This step clears the partition, allowing you to create a new one with the desired file system.
   ![image](https://github.com/user-attachments/assets/cd053592-023a-40d8-ad1f-cf5f05c8da15)


6. Once the partition is deleted, the space will appear as unallocated. Right-click on the unallocated space and select New to create a new partition with your desired settings.
   ![image](https://github.com/user-attachments/assets/8c92110e-9151-4945-852f-bde9024f3289)


7. In the Create New Partition dialog box, locate the New size (MiB) field. Enter 4096 to set the size of the new partition to 4,096 MiB (approximately 4 GB). This step defines the partition size.
   On the File system spin box, select fat32. On the Label text box, type: Windows, Click Add
   ![image](https://github.com/user-attachments/assets/e6243076-624b-4226-810d-e38558a016f8)


8. The new partition, New Partition #1, is now added. To apply and save the changes made to the file system, click the green checkmark or tick icon at the top of the GParted window. This step finalizes the partitioning process
  ![image](https://github.com/user-attachments/assets/2d5314e5-f90c-4cdd-badd-ceef08f651bc)


9. Click Apply when asked if you want to apply pending operations.
   ![image](https://github.com/user-attachments/assets/30978309-bb80-48ec-becf-7d4614ccc5b2)


10. Please wait while changes are being committed. Click Close when notified that the operations were successfully completed.
     ![image](https://github.com/user-attachments/assets/2010d844-504c-4a09-a780-3f8a44dcdf56)


11. The new primary partition in /dev/sdb1 is now added. Close the /dev/sdb - GParted window.
    ![image](https://github.com/user-attachments/assets/b08c0036-81e3-440c-a209-91dbafcae38a)


</details>


<details>

<summary><b>Task 2 - Mounting a disk volume</b></summary>

To mount the partition that was created earlier, perform the following steps;

## STEPS ##

1. To identify the name of your device file, open a terminal and run the following command: fdisk -l
   This will list all the available disks and partitions on your system, helping you locate the device file name (e.g., /dev/sdb) for the newly created partition.
 ![image](https://github.com/user-attachments/assets/76ad9fa8-34f1-4294-9fa5-7c16e60af9fe)
  

2. In the output of the fdisk -l command, look for the section labeled /dev/sdb.
Pay attention to the details displayed for this partition, such as Start, End, Blocks, Id, and System. These fields provide important information about the partition's size, type, and layout, which can help verify its configuration.
   ![image](https://github.com/user-attachments/assets/3b681550-cdd5-4443-ae80-bb661cd2a09e)


3. To create a directory where you will mount the device, type: mkdir /mnt/sdb1 AND press Enter
   ![image](https://github.com/user-attachments/assets/527605df-d3d0-4d69-b3e2-d9ce8845ae59)


4. After creating the mnt directory, the next step is to edit the /etc/fstab file to configure the partition to mount automatically at boot. At the prompt, type: leafpad
   This will open the fstab file in the Leafpad text editor, where you can add the necessary entry for your partition. Make sure to save your changes before closing the editor. 
   ![image](https://github.com/user-attachments/assets/15069723-bd35-476c-bbed-7ad2287c84e7)


5. When the Leafpad application opens, click on File in the top menu, then select Open. This will allow you to browse and open the /etc/fstab file if it hasn't opened automatically.
   ![image](https://github.com/user-attachments/assets/a3dfe641-0571-4d24-b6db-22be5ae54ffa)

  

6. In the Open dialog box, follow these steps:
   Click File System in the left pane to access the root directory.
   In the right pane, double-click on the etc folder to open it.
   Once inside the etc folder, scroll down to find the file named fstab.
   Select fstab and click Open to edit the file.

## NB: Please be aware that the fstab file is not located in the folder fstab.d and instead found at the bottom of the etc folder ##
![image](https://github.com/user-attachments/assets/53e8761c-600f-4362-b10b-7edce0e297ba)

7. When fstab file opens, go to the end of the file and type the following entries: /dev/sdb1  /mnt/sdb1  vfat  defaults  0  0. Press the TAB key to provide a space between the entries.
   This entry sets up the new partition /dev/sdb1 to be mounted at /mnt/sdb1 using the vfat file system. The options "defaults 0 0" specify the standard mount options and exclude the partition from the backup routine and file system check. Make sure to save your changes before closing the editor
![image](https://github.com/user-attachments/assets/0b553752-57da-4c14-91ef-ea4f998294b0)

8. Click File and select Save. Close Leafpad text editor window.


9. Back on the terminal window, to clear the screen, type: clear. Press Enter. On the next prompt, type: gparted
Press Enter.
![image](https://github.com/user-attachments/assets/40d9c3a9-e291-44d9-9fd8-69686e3d3737)



10. When GParted opens, look for the drop-down list in the top-right corner of the window.
Change the selection to /dev/sdb to view and manage the partitions on that specific disk.
![image](https://github.com/user-attachments/assets/ee707058-1562-46ab-9d54-d33414acaf28)


11. In the middle details pane, you'll see that the /dev/sdb1 partition is assigned the mount point /mnt/sdb1. This indicates that the drive is ready to be mounted and used, such as for receiving an image of a suspect drive.
    To mount it now:

Right-click on /dev/sdb1.
Select Mount on > /mnt/sdb1/ from the context menu.
This step ensures the partition is accessible and ready for use.
![image](https://github.com/user-attachments/assets/1d2a1839-7129-43c7-89e5-959fc025d660)


12. Please wait for the partition to finish mounting.

After a few seconds, you’ll notice a key icon appears next to FAT32, indicating that the partition is successfully mounted and is now in use.
Once confirmed, close the GParted window to return to the Terminal.
![image](https://github.com/user-attachments/assets/911662d9-c3da-4afa-baa5-67990b2ddb53)
  
</details>


## ACQUIRING DATA WITH dd IN LINUX ##

































  
</details>






































