---
title: FTK
parent: Tools
has_children: true
nav_order: 1
---

# FTK
Drive acquisition is one the first steps a Forensic Analyst will have to carry out at the beginning of case. These acquistions are often carried out remotely by VPN or by the the client (or client IT department) where the computer is located. Acquiring such images from a drive has been made easy using AccesData Forensic Toolkit (FTK) Imager. The software is free and can be downloaded [here](https://accessdata.com/product-download/forensic-toolkit-ftk-version-7.1.0)! 

Once downloaded, install the software. Launch by doubleclicking the FTK icon or running `FTK Imager.exe` from the command line.

Let's plug in an external USB drive to write to and image the host, a Windows 10 machine.

Here is the main GUI for FTK. Select `File` from the menu and `Create a Disk Image` and then chose the source of your image

![image](/assets/images/ftk/ftk1.jpg "FTK Imager")

We are imaging a physical drive so selct that option

![image](/assets/images/ftk/ftk2.jpg "FTK Imager, select Physical Drive")

Choose the drive to be imaged

![image](/assets/images/ftk/ftk3.jpg "FTK Imager, chose drive")

Now we need to select the destination (our external USB), to save the image too. We also want to carry out verification on the image to ensure that the copy we have on the USB is identical to the host machine. The image will calculate the MD5 and SHA1 hash values for the host drive ad FTK Image.

![image](/assets/images/ftk/ftk4.jpg "FTK Imager")

Next we need to selct the image format type that we will be saving. E01 is a common forensic image file format and is almost a standard. In addition, the E01 file format provides metadata about the image as well as compressing the data meaning you will be handler a smaller file after imaging. 

![image](/assets/images/ftk/ftk5.jpg "FTK Imager")

Select the image destination. The external USB dive is `D:`.

![image](/assets/images/ftk/ftk6.jpg "Select image destination")

Now image!

![image](/assets/images/ftk/ftk7.jpg "Image!")

After imaging the software will jump into the verification process

![image](/assets/images/ftk/ftk8.jpg "Image verification")

FTK Imager also creates a log of the acquisition process and places it in the same directory as the image, image-name.txt. This file lists the evidence information, details of the drive, check sums, and times the image acquisition started and finished:

![image](/assets/images/ftk/ftk9.jpg "Image verification")

Once the drive is imaged we are presented with the display that both the MD5 and SHA1 hashes indicate that the drive we just imaged and the image itself match.

![image](/assets/images/ftk/ftk10.jpg "Image verification display")

And that's that. Next up, memory dump using FTK Imager
