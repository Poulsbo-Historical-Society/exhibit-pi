# Exhibit Pi
Setting up a Raspberry Pi for PHS Exhibit

1) Image a Raspberry Pi OS Lite install onto your SD card
2) Install dependencies
   ```bash
   apt install vlc emacs git pulseaudio
   ```
3) Add a deploy key
   ```bash
   ssh-keygen -t rsa -b 4096
   ```
   3b) add ssh key to repo's "Deploy keys" setting
   
3) Clone this repository
   ```bash
   git clone git@github.com:Poulsbo-Historical-Society/exhibit-pi.git
   cd exhibit-pi
   ```
4) Link the pulseaudio config into place
   ```bash
   ln -s pulse.client.conf /etc/pulse/client.conf
   ```
5) Make the autoplay directory & put something inside it
   ```bash
   mkdir /autoplay
   chmod 777 /autoplay

   # 5b) scp video files into /autoplay, or copy them via usb
   ```
6) Link the service files, start, and enable them
   ```bash
   ln -s /home/pi/pulseaudio.service /etc/systemd/system/.
   ln -s /home/pi/vlc-autoplay.service /etc/systemd/system/.
   systemctl enable /etc/systemd/system/pulseaudio.service
   systemctl enable /etc/systemd/system/vlc-autoplay.service
   systemctl start pulseaudio
   systemctl start vlc-autoplay
   ```
