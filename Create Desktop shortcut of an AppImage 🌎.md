## Steps to create Desktop shortcut and Integration of an AppImage

Of course, even a new user easily can start an application packed in the AppImage format but the problem is, he or she has to access the local folder where the file is residing, every time to run the same.

### 1. Download AppImage

The first thing we should have is the AppImage of the software that we want to run because we cannot install it like any other Linux package using the package manager. For example, here we are downloading popular **NextCloud** client software that is available in AppImage format. You can go for any other program such as **Inkscape**.

### 2. Make the AppImage Executable

Once the file is in your system, first we have to make it executable because by default the file doesn’t have permission to execute itself.

Switch to Downloads, as whatever we download using the browser goes to this folder.

cd Downloads

To check your AppImage is there or not:

ls

Make the file executable:

chmod u+x _your-filename.AppImage_

**Note**: Change **_your-filename.AppImage_** with the Actual software file name you have downloaded.

### 3. Download the icon

Now, whatever AppImage you have, also download the icon of that Software you want to use in the icon or png format. You can simply search for that in Google. For example, I want to create a desktop shortcut of NextCloud client, then in the search engine -I will type: `nextcloud icon png`

### 4. Move both icon and AppImage to /opt

Although it is not necessary, still to make sure we won’t delete our downloaded files accidentally, we move them to **/opt** directory from Downloads.

sudo mv **filename.AppImage** /opt/

sudo mv **your-icon-name.png** /opt/

### 5. Create Desktop shortcut and Application Launcher

Once both AppImage of software and its icon move to `/opt` directory, create a desktop shortcut to easily run it from anywhere.

Hence, we have to create the shortcut manually. Here we are creating the NextCloud AppImage shortcut:

sudo dnf install nano -y

Create Desktop Launcher Shortcut. Replace “**NextCloud**” with whatever name you want to give your shortcut.

sudo nano /usr/share/applications/**NextCloud**.desktop

**Note**: Replace `Nextcloud`,  `nextcloud.AppImage` and `nextcloud-icon.png` in the file.

**Add the following lines:**

[Desktop Entry]
Name=**Nextcloud**
Exec=/opt/**nextcloud.AppImage**
Icon=/opt/**nextcloud-icon.png**
comment=cloud
Type=Application
Terminal=false
Encoding=UTF-8
Categories=Utility;

Save the file- **Ctrl+O** hit the **Enter** key, and then exit **Ctrl+X.**

Now, you can start your AppImage directly from the Applications Launcher. Moreover, if the Desktop icons are enabled on your system then you can create the shortcut on the Desktop as well. Just use:

sudo cp -r /usr/share/applications/**NextCloud**.desktop ~/Desktop/

After that go to the **desktop**, right-click on that, select **properties**, and in the **permissions** tab select _Allow this file to run as a program._

**Ending Notes:**

In this way, we can easily integrate our program’s AppImage on any Linux system. You can see our article related to this – [Install NextCloud Client on Linux](https://www.how2shout.com/linux/install-nextcloud-client-on-almalinux-or-rocky-linux-8/)