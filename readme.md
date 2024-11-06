# portable WSL2

## build WSL2 kernel

~~~
sudo apt install git bc build-essential flex bison libssl-dev libelf-dev dwarves pkg-config cpio -y
git clone --depth 1 https://github.com/microsoft/WSL2-Linux-Kernel.git
cd WSL2-Linux-Kernel
cp Microsoft/config-wsl .config
make
~~~

## Use custom kernel

~~~
cp arch/x86/boot/bzImage /mnt/<Disk-Litera>/<Folder-To-Kernel>/bzImage
cat <<EOT >> /mnt/c/Users/<User-Name>/.wslconfig
[wsl2]
kernel=<Disk-Litera>:\\<Folder-To-Kernel>\\bzImage
EOT
~~~

## Move Distro

As *.tar archive:

~~~
wsl.exe --export <DistroName> <Tar-FileName>
wsl.exe --import <DistroName> <Folder-To-Install> <Tar-FileName>
~~~

..or *.vhdx image:

~~~
wsl.exe --export <DistroName> <ImageName> --vhd
wsl.exe --import <DistroName> <Folder-To-Install> <ImageName> --vhd
~~~

After import, the system boots with the root. To boot under a specific user, use the command:

~~~
wsl.exe -d <DistroName> -u <UserName>
~~~
