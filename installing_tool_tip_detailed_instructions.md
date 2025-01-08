# Installing the toolbar extensions on Remarkable Paper Pro (RPP)

Last updated on: 2025/01/08 15:00:00 UTC

> **_NOTE:_**  The next part guides you through more or less the complete installation procedure
> using Terminal in either a Macbook or Ubuntu/Linux systems. Skip to the next section, if you
> prefer using apps instead of doing things through terminal.


## Developer mode
In order to hack yoour RPP, you need to have `Developer Mode` activated. Follow the instructions on
the [reMarkable website](https://support.remarkable.com/s/article/Developer-mode) to enter in the
developer mode.

> [!WARNING]  
>  Once you activate `Developer Mode`, your RPP will do a factory reset.

Once you have enabled `Developer Mode`, you will need to connect your RPP to your computer using a
USB-C cable. For detailed information on how to do it, check the [following
link](https://www.simplykyra.com/blog/learn-how-to-access-your-remarkable-paper-pro-through-the-command-line/#steps-for-ssh-capabilities).

Note down the IP address of your RPP. You will need it to SSH into your device in later steps.

## Downloading the prerequisites
You will need to download the following files to your computer. For this guide, we will assume that
you have downloaded the files to your `Downloads` directory.

- Download `xovi`: Download the `xovi` package from
  [here](https://raw.githubusercontent.com/asivery/rmpp-xovi-extensions/refs/heads/master/scripts/install_allmerged.sh)
  and save it to your `Downloads` directory.

- Download the extensions from `xovi`
  [here](https://github.com/asivery/rmpp-xovi-extensions/releases/tag/29122024-v5).
  You will see three compressed files there. Download the file named `extensions.zip` and save it
  to your `Downloads` directory.

- Download the `xovi-toolbar-extensions` from [here]([https](https://github.com/fouzR/xovi-toolbar-extensions).
  Once you are on the page, click on the green `Code` button and select `Download ZIP`. Save the
  downloaded file to your `Downloads` directory.

  Congrats, you have downloaded all the necessary files to your computer. Extract all the `zip`
  files to their respective directories. You will need to upload some of these files to your RPP in
  the next steps.

## Uploading the files to your RPP
In this section, you will upload the required files to your RPP. We will be using terminal to
achieve this task. If you prefer using apps, you can use `FileZilla` (see this
[section](#using-filezilla-to-upload-the-files)) to upload the files to your RPP.


### Upload the `xovi` installer
Navigate to the `Downloads` directory and upload the `install_allmerged.sh` file to the `/tmp`
directory on your RPP by running the following command:
```bash
  scp ~/Downloads/install_allmerged.sh root@xxx.xx.x.XXX:/tmp
```

### SSH into your RPP
Run the following command in your terminal to SSH into your RPP:
```bash
  ssh root@xxx.xx.x.XXX
```
Replace the `xxx.xx.x.XXX` with the IP address displayed on the copyright page.


#### Making the appropriate folders
Run the following commands to create the necessary folders:
```bash
  mkdir -p /home/root/xovi
  mkdir -p /home/root/xovi/extensions.d
  mkdir -p /home/root/xovi/exthome/qt-resource-rebuilder
```

### Installing `xovi`
Run the following command to install `xovi`:
```bash
  chmod a+x /tmp/install_allmerged.sh && /tmp/install_allmerged.sh
```

Exit the RPP by pressing `Ctrl + D` on your keyboard. You will be back in your computer's terminal
from where you will need to upload the necessary files to your RPP in proper folders.

### Upload the extensions
Navigate to the `Downloads` directory and located and upload the `qt-resource-rebuilder.so` file to
the `/home/root/xovi/extensions.d` directory on your RPP. `qt-resource-rebuilder.so` should be
located in the `extensions` directory of the extracted `extensions.zip` file.
```bash
  scp ~/Downloads/qt-resource-rebuilder.so root@xxx.xx.x.XXX:/home/root/xovi/extensions.d
```

### Upload the toolbar extensions
Navigate to the `Downloads` directory and upload the `Edit.qmd` and `simplified-3.17.qmd` (or the
most appropriate file corresponding to your reMarkable's OS version) files to the
`/home/root/xovi/exthome/qt-resource-rebuilder` directory on your RPP. These files should be located
in the `xovi-toolbar-extensions` directory that you downloaded earlier.
```bash
  scp ~/Downloads/Edit.qmd root@xxx.xx.x.XXX:/home/root/xovi/exthome/qt-resource-rebuilder
  scp ~/Downloads/simplified-3.17.qmd root@xxx.xx.x.XXX:/home/root/xovi/exthome/qt-resource-rebuilder
```

### Rebuilding the hashtable
SSH back into your RPP and run the following commands:
```bash
  ssh root@xxx.xx.x.XXX
```

Run the following commands to rebuild the hashtable:
```bash
  rm -f /home/root/xovi/exthome/qt-resource-rebuilder/hashtab

  systemctl stop xochitl

  killall xochitl

  QMLDIFF_HASHTAB_CREATE=/home/root/xovi/exthome/qt-resource-rebuilder/hashtab xovi/debug
```
Once you run the above commands, your RPP will refresh and ask you to enter your passcode (if you
have that option turned on). After entering the passcode, your RPP will restart.

### Restarting xovi
After your RPP restarts, press `Ctrl + C` on your keyboard to exit the terminal. SSH back into your
RPP and run the following command to rebuild the hashtable:
```bash
  xovi/rebuild_hashtable
```
  
Finally, restart `xovi` by running the following command:
```bash
  xovi/start
```

You should see a new button above the pages icon. Tap the `Quick tools` toggle and start using it! Hit the `Reset floatbar` to center it on top.

## Using FileZilla to upload the files
If you prefer using apps to upload the files to your RPP, you can use `FileZilla` to do so. Follow
the instructions below to upload the files to your RPP using `FileZilla`.

- Download all the necessary files to your computer. Extract the `zip` files to their respective
  directories (see this [section]( #Downloading-the-prerequisites)).

- Download `FileZilla` from [here](https://filezilla-project.org/) and install it on your computer.

- Open `FileZilla` and enter the IP address of your RPP in the `Host` field. Enter `root` in the
  `Username` field and the password displayed on the copyright page in the `Password` field. Enter
  `22` in the `Port` field and click on `Quickconnect`.

- Once youre reMarkable is connected, you will see the file structure of your RPP on the right side
  of the `FileZilla` window. In order to create a new directory, right-click on the right side and
  select `Create directory`. To upload files, simply drag and drop the files from your computer to
  the appropriate directory on your RPP.

- Once connected, navigate to the `/tmp` directory and upload the `install_allmerged.sh` file to the
  `/tmp` directory on your RPP.

- Navigate to the `/home/root` directory and create the following directories:
  - `xovi`
  - `xovi/extensions.d`
  - `xovi/exthome/qt-resource-rebuilder`

- Navigate to the `/home/root/xovi/extensions.d` directory and upload the `qt-resource-rebuilder.so`
  file to the directory.

- Navigate to the `/home/root/xovi/exthome/qt-resource-rebuilder` directory and upload the `Edit.qmd`
  and `simplified-3.17.qmd` files to the directory. After this point, we have to use the terminal to
  install the toolbar extensions.

- SSH into your RPP and run the following commands in the provided order to install the toolbar
  extensions:

```bash
  chmod a+x /tmp/install_allmerged.sh && /tmp/install_allmerged.sh
  
  rm -f /home/root/xovi/exthome/qt-resource-rebuilder/hashtab
  
  systemctl stop xochitl
  
  killall xochitl
  
  QMLDIFF_HASHTAB_CREATE=/home/root/xovi/exthome/qt-resource-rebuilder/hashtab xovi/debug
```

- After your RPP restarts, press `Ctrl + C` on your keyboard to exit the terminal. SSH back into
  your RPP and run the following command to rebuild the hashtable:
```bash
  xovi/rebuild_hashtable
```

- Finally, restart `xovi` by running the following command:
```bash
  xovi/start
```

You should see a new button above the pages icon. Tap the `Quick tools` toggle and start using it! Hit the `Reset floatbar` to center it on top.