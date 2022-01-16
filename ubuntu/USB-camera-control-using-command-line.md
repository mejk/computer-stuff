# Webcam tools:

This provides a CLI-based method to control your webcam.

Install video for Linux control:

```
sudo apt update
sudo apt install v4l-utils
```
To check the connected video devices:

```
v4l2-ctl --list-devices
```
The output looks something like this:

```
$  v4l2-ctl --list-devices
fakecam (platform:v4l2loopback-000):
        /dev/video20

Video Capture 4 (usb-0000:00:14.0-7.2.1):
        /dev/video2
        /dev/video3
        /dev/video4
        /dev/video5

Video Capture 5 (usb-0000:00:14.0-8):
        /dev/video0
        /dev/video1

```
In this case the first one is the connected USB camera and the second one is the built-in camera.

To see the controls:

```
v4l2-ctl -d /dev/video0 --list-ctrls
```

For the two devices above, this gives:

```
                     brightness 0x00980900 (int)    : min=0 max=255 step=1 default=128 value=128
                       contrast 0x00980901 (int)    : min=0 max=255 step=1 default=32 val(base) 
                     brightness 0x00980900 (int)    : min=0 max=255 step=1 default=128 value=128
                       contrast 0x00980901 (int)    : min=0 max=255 step=1 default=128 value=128
                     saturation 0x00980902 (int)    : min=0 max=255 step=1 default=128 value=128
 white_balance_temperature_auto 0x0098090c (bool)   : default=1 value=1
                           gain 0x00980913 (int)    : min=0 max=255 step=1 default=0 value=128
           power_line_frequency 0x00980918 (menu)   : min=0 max=2 default=2 value=2
      white_balance_temperature 0x0098091a (int)    : min=2000 max=7500 step=10 default=4000 value=3330 flags=inactive
                      sharpness 0x0098091b (int)    : min=0 max=255 step=1 default=128 value=128
         backlight_compensation 0x0098091c (int)    : min=0 max=1 step=1 default=1 value=1
                  exposure_auto 0x009a0901 (menu)   : min=0 max=3 default=3 value=3
              exposure_absolute 0x009a0902 (int)    : min=3 max=2047 step=1 default=250 value=250 flags=inactive
         exposure_auto_priority 0x009a0903 (bool)   : default=0 value=1
                   pan_absolute 0x009a0908 (int)    : min=-36000 max=36000 step=3600 default=0 value=0
                  tilt_absolute 0x009a0909 (int)    : min=-36000 max=36000 step=3600 default=0 value=0
                 focus_absolute 0x009a090a (int)    : min=0 max=255 step=5 default=0 value=40 flags=inactive
                     focus_auto 0x009a090c (bool)   : default=1 value=1
                  zoom_absolute 0x009a090d (int)    : min=100 max=500 step=1 default=100 value=200

```

and

```
                    brightness 0x00980900 (int)    : min=0 max=255 step=1 default=128 value=128
                       contrast 0x00980901 (int)    : min=0 max=255 step=1 default=32 value=32
                     saturation 0x00980902 (int)    : min=0 max=100 step=1 default=64 value=64
                            hue 0x00980903 (int)    : min=-180 max=180 step=1 default=0 value=0
 white_balance_temperature_auto 0x0098090c (bool)   : default=1 value=1
                          gamma 0x00980910 (int)    : min=90 max=150 step=1 default=120 value=120
           power_line_frequency 0x00980918 (menu)   : min=0 max=2 default=1 value=1
      white_balance_temperature 0x0098091a (int)    : min=2800 max=6500 step=1 default=4000 value=4000 flags=inactive
                      sharpness 0x0098091b (int)    : min=0 max=7 step=1 default=2 value=2
         backlight_compensation 0x0098091c (int)    : min=0 max=2 step=1 default=1 value=1
                  exposure_auto 0x009a0901 (menu)   : min=0 max=3 default=3 value=3
              exposure_absolute 0x009a0902 (int)    : min=4 max=1250 step=1 default=156 value=156 flags=inactive
         exposure_auto_priority 0x009a0903 (bool)   : default=0 value=1

```

Any of these can be set using ` v4l2-ctl --set-ctrl`.

For example, set the zoom in the camera in device '/dev/video4':

```
 v4l2-ctl -d /dev/video4 --set-ctrl=zoom_absolute=200
```
