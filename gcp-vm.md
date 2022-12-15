Compute Engine -> VM Instances
Create an instance -> New VM instance

Name: fx-trading-host
Region: europe-west3 (Frankfurt)
Zone: europe-west3-c
Machine family: GENERAL-PURPOSE
Series: E2
Machine-type: e2-medium (2vCPU, 4 GB memory)
Do not select 'Enable display device'

Boot disk
Type: New balanced persistent disk
Size: 10 GB
Image: Debian GNU/Linux 11 (bullseye)

Enable both:
    Allow HTTP traffic
    Allow HTTPS traffic


Leave all other values as default
Click CREATE



