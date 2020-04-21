# Lab 2.1: Install Puppet Bolt

In this lab you will learn how to:

* Install the open source Bolt utility on Windows machines.
* Execute a simple command to validate that Bolt is working.

## Steps

### Installing Bolt onto a **Windows** target machine

#### Connect to the Windows target machine with RDP

**_You can get the details of which student machines you can use as target machines in the welcome page, located at <https://classXXXX.classroom.puppet.com> (replace XXXX with your class’s numbers)._**

* If you are connecting to the Windows target machine from a **Windows** host machine, use Remote Desktop Connection.

* If you are connecting to the Windows target machine from a **macOS** host machine, use Microsoft Remote Desktop 10.

Connect with the following information:

* **hostname:** *XXXXwinY.classroom.puppet.com* (replace XXXX and Y with the correct numbers)
* **username:** *Administrator*
* **password:** *\<PASSWORD FROM THE WELCOME PAGE>*

#### Install Bolt on the Windows target machine

**_You will install Bolt on Windows using a third-party package manager,_** **chocolatey** **_._**

On the target machine, start a PowerShell session and run:

```choco install puppet-bolt```

#### Validate the installation

Close any open PowerShell windows. **This is critical** in order for PowerShell to pick up the changes you just made with chocolatey.

Note that your version might be slightly different.

```plaintext
   PS C:\Users\Administrator> bolt --version
   2.6.0
```

Open a new PowerShell window and run:

```bolt --version```

#### Run Bolt

```bolt help```

or simply:

```bolt```

This provides a page of helpful information for running Bolt. We will come back to Bolt after setting up the rest of the lab.

Next Step

======

[Linux Lab 2.1 Install Puppet Bolt](../../Linux/lab-02.1-Install-Puppet-Bolt)

---

|  [Previous Lab](../lab-01.1-Puppet-product-overview)  |  [Next Lab](../lab-02.2-Running-Bolt-Commands)  |
