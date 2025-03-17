# Ungit on IBMi

> A practical guide to install ungit on IBMi

- [Ungit on IBMi](#ungit-on-ibmi)
  - [Pre-requisite](#pre-requisite)
      - [What is *bash* shell?](#what-is-bash-shell)
    - [Open Source Package Management](#open-source-package-management)
    - [Git](#git)
    - [Nodejs](#nodejs)
  - [Install Ungit](#install-ungit)
  - [Configure Ungit](#configure-ungit)
      - [Set Path Variable for Ungit](#set-path-variable-for-ungit)
      - [Setup config file](#setup-config-file)
  - [Start Ungit](#start-ungit)


## Pre-requisite
It is important to setup a working open source environment as most of the software we are going to use are open source. 
We will be using *bash* shell that is supported by *code-for-i* to install and run ungit.

#### What is *bash* shell?
We all knew QSH in IBMi. If QSH is like RPG III, then *bash* is like modern RPGLE. It is user friendly, supports color text and offers much more convenience. 

Login to your server using VS Code. Once connected, click on the bottom right bell notification icon and select, `change shell to bash` 

![bash](https://raw.githubusercontent.com/ravisankar-PIO/devopsonibmi/advanced/images/bash.png)

Disconnect from your IBMi and then connect again for the changes to take effect.

Finally, open the terminal by entering `ctrl+shift+j`. 

If all worked good, then you should be seeing the below screen
```
Terminal started, thanks for using Code for IBM i. Current directory is /home/RAVI.
-bash-5.2$ 
```

<br>
### Open Source Package Management
In your bash terminal, check whether yum is installed by entering,
```shell
/QOpenSys/pkgs/bin/yum version
```
If not installed, then I would suggest you to install open source package management system first by using [this](https://www.seidengroup.com/php-documentation/how-to-set-up-the-ibm-i-open-source-environment/) link.

After yum is installed, set the `$PATH` variable to include the location of those open source package binaries. 

```shell
cd && touch .profile
```

- Open the file `.profile` using VS Code's IFS Browser. If you don't see the file, then click on the refresh icon on the top right side of the IFS browser panel.
    
- Copy paste the below content on the `.profile` file.


```bash
export PATH=/QOpenSys/pkgs/bin:$PATH
```
Finally, enter `ctrl+shift+j` again to reopen a new terminal with path variable included in it. 

<br>
### Git 
Check whether Git is installed by entering,
```sh
git -v
```
If not installed, then install it by using,
```sh
yum install git
```

<br>
### Nodejs
Check whether Nodejs is installed by entering,
```sh
node -v
```
If not installed, then follow these steps to install:
- The below command will give you the available Nodejs packages. Browse through it and select any version that is greater than 14. 
  ```sh
  yum list available
  ```
- Then install using,
  ```sh
  yum install nodejs22.ppc64
  ```

<br>
## Install Ungit
Once Nodejs is installed, you can use the `npm` (Node Package Management) to install Ungit using,
```sh
yum install -g ungit
```
Note: The `-g` flag means ungit is installed at global level. 

<br>
## Configure Ungit
Since we have installed ungit at global level, the binaries are stored at the location `/QOpenSys/pkgs/lib/nodejs22/lib/node_modules/ungit/bin/`. Note that my Nodejs version is 22, but if you installed a different version then your path would be different.

### Set Path Variable for Ungit
We need to include this path in the `.profile` file just like we did before.


- Open the file `.profile` using VS Code's IFS Browser. If you don't see the file, then click on the refresh icon on the top right side of the IFS browser panel.
    
- Copy paste the below content on the `.profile` file.


```bash
export PATH=/QOpenSys/pkgs/bin:$PATH
export PATH=/QOpenSys/pkgs/lib/nodejs22/lib/node_modules/ungit/bin:$PATH
```
Finally, enter `ctrl+shift+j` again to reopen a new terminal with path variable included in it. 

### Setup config file
It is important to create a config file which will be used by ungit during runtime. 
```shell
cd && touch .ungitrc
```

- Open the file `.ungitrc` using VS Code's IFS Browser. If you don't see the file, then click on the refresh icon on the top right side of the IFS browser panel.
    
- Copy paste the below content on the `.ungit` file.


```json
{
  "port": 8448,
  "bugtracking": false,
  "authentication": false,
  "ungitBindIp": "0.0.0.0"
}
```

## Start Ungit

```sh
ungit --ungitBindIp=0.0.0.0
```
That's it! Your ungit is installed on IBMi!
