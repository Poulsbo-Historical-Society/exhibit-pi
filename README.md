# Exhibit Pi
Setting up a Raspberry Pi for PHS Exhibit

1) Image a Raspberry Pi OS Lite install onto your SD card
      - naming scheme is phs-exhib-<display>.lan, username=phs
2) Install dependencies
   ```bash
   apt update && apt upgrade && apt install emacs git pulseaudio
   ```
3) Clone this repository
   ```bash
   git clone https://github.com/Poulsbo-Historical-Society/exhibit-pi.git
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
6) Link the service files, start, and enable them
   ```bash
   ln -s /home/phs/exhibit-pi/pulseaudio.service /etc/systemd/system/.
   systemctl enable /etc/systemd/system/pulseaudio.service
   systemctl start pulseaudio
   ```
