# Exhibit Pi
Setting up a Raspberry Pi for PHS Exhibit

1) Image a Raspberry Pi OS Lite install onto your SD card
      - naming scheme is phs-exhib-0.lan, username=phs
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
   mv /etc/pulse/client.conf /etc/pulse/client.conf.bk
   ln -s pulse.client.conf /etc/pulse/client.conf
   ```
5) Set pulse group & disable user-space pulse
   ```bash
   usermod -a -G pulse-access phs
   systemctl --global disable pulseaudio.service pulseaudio.socket
   ```
5) Make the autoplay directory & put something inside it
   ```bash
   mkdir /autoplay
   chmod 777 /autoplay

   # scp video files into /autoplay, or copy them via usb
   # if subtitles are available they should be named the same
   # as the video file with .srt extension
   
   ```
6) Link the service files, start, and enable them
   ```bash
   ln -s /home/phs/exhibit-pi/pulseaudio.service /etc/systemd/system/.
   ln -s /home/phs/exhibit-pi/vlc-autoplay.service /etc/systemd/system/.
   systemctl enable /etc/systemd/system/pulseaudio.service
   systemctl enable /etc/systemd/system/vlc-autoplay.service
   systemctl start pulseaudio
   systemctl start vlc-autoplay
   ```
