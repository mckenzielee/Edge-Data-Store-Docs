---
uid: disasterRecovery
---

#
# Edge Data Store

_Disaster Recovery Process Guidelines_

_(Windows and Linux Systems)_

#

# Intro

This topic provides procedures for creating a backup of Edge Data Store stream data and configuration files, moving them to a new system, and then restoring the back up files onto the new system. Procedures are provided for Windows and Linux systems.
 
Prequisite:  Read the Credentials topic prior to beginning this topic.  This guide does not include backing up or restoring of any credentials. All credentials are encrypted for security purposes, so they cannot be copied or transferred. After the new system has had the storage and configuration files copied over, and the service has started, you will need to re-enter the credentials for the system using API calls. After updating, restart the Edge Data Store service. The new edge device will be running as the previous device, and will contain all the data up to the point the previous device went down.


# Windows Recovery

**Create a backup**

Prerequisite: Administrative access on the device to successfully restore on Windows system

1. Verify that Edge Data Store service has stopped, if your device is still able to boot. This can be done through the Windows Service Manager or Task Manager Services tab.
2. Locate the storage and configuration files.

	**Note:** Windows storage and configuration files should be in the following locations:
			\(***1**) C:\ProgramData\OSIsoft\EdgeDataStore\Configuration
			\(***1**) C:\ProgramData\OSIsoft\EdgeDataStore\Storage
			The ProgramData folder is typically hidden, so if it is not visible, go to the **View** tab in **Windows Explorer** and check **Hidden**.

3. Create a zip or tar file containing the storage and configuration directories, and move it to a USB or other safe location. File transfer can be done with WinSCP, SFTP, or external device.

**Move the files to the new hardware***

Once the new hardware has replaced the previous system and has been installed with Edge Data Store, the new system will have a default configuration. 

1. Stop the Edge Data Store service using the Windows Service Manager or Task Manager service tab.
2. Once that service has stopped, navigate to the C:\ProgramData\OSIsoft\EdgeDataStore directory and extract your zip or tar file in that directory again using WinSCP, SFTP, or external device.

**Restore data files**

1. Delete the default storage and configuration folders from the new device.
2. Copy or unzip the backup storage and configuration files into the C:\ProgramData\OSIsoft\EdgeDataStore directory.

	**Note:** The C: drive may not be your systems default drive letter. Refer to My Computer, This PC, or simply open a command prompt to verify your systems drive letter.

3. Use the Windows Service Manager or Task Manager to restart the Edge Data Store service.


# Linux Recovery

**Create a backup**

Prerequisite: Root access on the Linux device

1. If your device is still able to boot, verify that Edge Data Store service has stopped, using the following command: 

   ```
   _sudo systemctl stop osisoft.edgedatastore_
   ```
	**Note:** Using the _cp_ command may result in a change in file ownership to the current user. 

2. Locate the storage and configuration files.

	**Note:** Linux storage and configuration files should be in the following locations:
			/usr/share/OSIsoft/EdgeDataStore/Configuration
			/usr/share/OSIsoft/EdgeDataStore /Storage

3. Create a zip or tar file containing the storage and configuration directories, and move it to a USB or other safe location. File transfer can be done with WinSCP, SFTP, or external device.

**Move the files to the new hardware***

Once the new hardware has replaced the previous system and has been installed with Edge Data Store, the new system will have a default configuration. 

1. Stop the Edge Data Store service using the following command:

   ```
   _sudo systemctl stop osisoft.edgedatastore_
   ```

2. Once that service has stopped, navigate to the /usr/share/OSIsoft/EdgeDataStore directory and extract your zip or tar file in that directory again using WinSCP, SFTP, or external device.

**Restore data files**

1. Delete the default storage and configuration folders from the /usr/share/OSIsoft/EdgeDataStore directory.
2. Copy or unzip the backup storage and configuration files into the EdgeDataStore directory.
3. Update the ownership of the 2 directories to _edgedatastore_ for the user and group, if they do not match _edgedatastore_. 
4. Start the Edge Data Store service with the following command:

   ```
   _sudo systemctl start osisoft.edgedatastore_
   ```

5. Verify that Edge Data Store is running with the following command:

   ```
   _sudo systemctl status osisoft.edgedatastore_
   ```

	**Note:** Default directory permissions are set to 755, and each subsequent file is 644. If you do not use tar it is possible to have permission issues with the recovery files. Tar matches via string name rather than the account 		  ID/UID, and it also preserves permissions on files when zipping them.
