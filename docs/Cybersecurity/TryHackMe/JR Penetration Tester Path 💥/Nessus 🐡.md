# Introduction
![](./img/Pasted%20image%2020230903121450.png)

Nessus vulnerability scanner is exactly what you think is its! A vulnerability scanner!

It uses techniques similar to Nmap to find and report vulnerabilities, which are then, presented in a nice GUI for us to look at.

Nessus is different from other scanners as it doesn't make assumptions when scanning, like assuming the web application is running on port 80 for instance.

Nessus offers a free and paid service, in which some features are left out from the free to make you more inclined to buy the paid service. 

Their pricing is similar to Burp Suite, so unless you got some spare change, we will be just be using their free version.

You can check out their pricing options here: [https://www.tenable.com/products/nessus](https://www.tenable.com/products/nessus)

# Installation
![](./img/Pasted%20image%2020230903121637.png)

Check the [Official Installation Guide](https://docs.tenable.com/nessus/Content/GettingStarted.htm)

## Step 1

![](./img/Pasted%20image%2020230903122110.png)

Goto [https://www.tenable.com/products/nessus/nessus-essentials](https://www.tenable.com/products/nessus/nessus-essentials) and register an account.

**You will need to do this for an activation code.**

## Step 2

![](./img/Pasted%20image%2020230903122137.png)

We will then download the Nessus-#.##.#-debian6_**amd64.**deb file

Save it to your **/Downloads/** folder

## Step 3

In the terminal we will navigate to that folder and run the following command:  

`sudo dpkg -i **package_file.deb**`

Remember to replace package_file.deb with the file name you downloaded.

![](./img/Pasted%20image%2020230903122229.png)

## Step 4

We will now start the Nessus Service with the command:  

`**sudo /bin/systemctl start nessusd.service**`

![](./img/Pasted%20image%2020230903122428.png)

## Step 5

Open up Firefox and goto the following URL:  

[https://localhost:8834/](http://localhost:8834/) 

You may be prompted with a security risk alert.

Click **Advanced...** -> **Accept the Risk and Continue**

![](./img/Pasted%20image%2020230903122501.png)

## Step 6

Next, we will set up the scanner.  

Select the option **Nessus Essentials**

![](./img/Pasted%20image%2020230903122817.png)

Clicking the **Skip** button will bring us to a page, which we will input that code we got in the email from Nessus.

![](./img/Pasted%20image%2020230903122835.png)

## Step 7

Fill out the **Username** and **Password** fields. Make sure to use a strong password!

![](./img/Pasted%20image%2020230903124158.png)

## Step 8

Nessus will now install the **plugins** required for it to function.

![](./img/Pasted%20image%2020230903124224.png)

This will take some time, which will depend on your internet connection and the hardware attached to your VM.

If the progress bar appears to be **not moving**, it means you do not have **enough space** on the VM to install.

## Step 9

**Log in** with the account credentials you made earlier.

![](./img/Pasted%20image%2020230903124300.png)

## Step 10

You have now successfully installed **Nessus**!

![](./img/Pasted%20image%2020230903124330.png)

# Navigation and Scans

![](./img/Pasted%20image%2020230903124356.png)

