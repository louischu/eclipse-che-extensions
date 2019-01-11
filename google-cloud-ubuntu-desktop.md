sudo apt-get update
sudo apt-get install ubuntu-desktop -y
sudo apt-get install gnome-panel gnome-settings-daemon metacity nautilus gnome-terminal vnc4server -y
vncserver //for set password
cp ~/.vnc/xstartup ~/.vnc/xstartup.bak
vim ~/.vnc/xstartup
content:
xsetroot -solid grey
vncconfig -iconic &


gnome-panel &
gnom-settings-daemon &
metacity &
nautilus &
gnome terminal &