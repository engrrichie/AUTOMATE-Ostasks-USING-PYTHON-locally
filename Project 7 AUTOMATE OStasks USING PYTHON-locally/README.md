# Project-7: AUTOMATE USING PYTHON -locally

[*Project Source*](https://www.udemy.com/course/decodingdevops/learn/lecture/26465838#questions)

![](Images/image.png)

- Using python to automate operating systems task especially Linux

## TASKS
 * Add Users
 *  Add Groups
 *  Add Users to group
 *  Assign user & group ownership to directory
 *  Test if user or directory exists, if not create it

 
 ## Step-1: VM Setup

- Navigate the directory that has python vagrant file on your local system and run the below commands
```sh
cd /c/vagrant-vms/Python/
cat Vagrantfile
vagrant up
```

- NOTE: Bringing VMs can take long time sometimes. If VM setup stops in the middle, run vagrant up command again.

![](Images/Vagrant%20up.png)

- Validate the VMs one by one with command `vagrant ssh` <name_of_VM_given_in_Vagrantfile> and switch to root user.

```sh
vagrant ssh scriptbox
sudo -i
```

## Step-2: Create file path

- Create a directory for pyscripts  and Ostasks using the below commands
```sh
mkdir/opt/pyscripts
cd /opt/pyscripts/
mkdir ostasks
```
- Check for directory using vim check-file.py, then insert the below scripts.
```sh
vim check-file.py

#!/usr/bin/python3
import os
path = '/tmp/testfile.txt'
if os.path. isdir(path):
    print("It is a directory")
elif os.path. isfile(path):
    print("It is a file.")
else:
    print("file or dir does not exists.")
```
![](Images/Path%20exist.png)

- Make the script executable and execute it using the below commands

```sh
chmod +x check-file.py
./check-file.py
```
![](Images/file%20does%20not%20exist.png)

- Create a file using the below command
```sh
touch /tmp/testfile.txt
./check-file.py
```
![](Images/file%20created.png)

## Step-3: Create Users and Group Directories

- Create users directories and check conditions whether they exist or not using the below command and scripts.

```sh
vim ostasks.py

#!/usr/bin/python3

userlist = ["alpha", "beta", "gamma"]

print("Adding users to system")
print("###################################################################################")

# Loop to add user from userlist
for user in userlist:
    exitcode = os.system("id {}".format(user) )
    if exitcode !=0:
        print"User {} does not exist. Adding it. ".format(user)
        print "###############################################"
        print
        os.system(("useradd {}".format(user))
    else:
        print("User already exist, skipping it. ")
        print("##########################################")
        print()
```

- Make the script executable and execute it using the below commands
```sh
chmod +x ostasks.py
./ostasks.py
```
![](Images/creating%20user.png)

![](Images/user%20created.png)

- Create group directories and check conditions whether they exist or not using the below command and scripts.

```sh
vim ostasks.py
```

```sh
#!/usr/bin/python3

userlist = ["alpha", "beta", "gamma"]

print("Adding users to system")
print("###################################################################################")

# Loop to add user from userlist
for user in userlist:
    exitcode = os.system("id {}".format(user) )
    if exitcode !=0:
        print"User {} does not exist. Adding it. ".format(user)
        print "###############################################"
        print
        os.system(("useradd {}".format(user))
    else:
        print("User already exist, skipping it. ")
        print("##########################################")
        print()

# Condition to check if group exists or not. add if not exist.
exitcode = os.system("grep science /etc/group")
if exitcode != 0:
    print("Group science does not exist. Adding it.")
    print("#############################################")
    print()
    os.system("groupadd science")
else:
    print("Group already exist, skippinig it.")
    print("##############################################")
    print()
```
![](Images/Group%20created.png)

## Step-4: Add all Users to Group

- Add all users to the Group `science`
- Create group directories and check conditions whether they exist or not using the below command and scripts.

```sh
vim ostasks.py
```
```sh
#!/usr/bin/python3

userlist = ["alpha", "beta", "gamma"]

print("Adding users to system")
print("###################################################################################")

# Loop to add user from userlist
for user in userlist:
    exitcode = os.system("id {}".format(user) )
    if exitcode !=0:
        print"User {} does not exist. Adding it. ".format(user)
        print "###############################################"
        print
        os.system(("useradd {}".format(user))
    else:
        print("User already exist, skipping it. ")
        print("##########################################")
        print()

# Condition to check if group exists or not. add if not exist.
exitcode = os.system("grep science /etc/group")
if exitcode != 0:
    print("Group science does not exist. Adding it.")
    print("#############################################")
    print()
    os.system("groupadd science")
else:
    print("Group already exist, skippinig it.")
    print("##############################################")
    print()

for user in userlist:
    print("Adding user {} in the science group".format(user))
    print("###################################################")
    print()
    os.system("usermod -G science {}".format(user))
```

![](Images/Adding%20user%20to%20the%20group.png)

## Step-5: Create a directory from the python script
- Create directory from the python script and assign ownership to both users and group.

```sh
vim ostasks.py
```
```sh
#!/usr/bin/python3

userlist = ["alpha", "beta", "gamma"]

print("Adding users to system")
print("###################################################################################")

# Loop to add user from userlist
for user in userlist:
    exitcode = os.system("id {}".format(user) )
    if exitcode !=0:
        print"User {} does not exist. Adding it. ".format(user)
        print "###############################################"
        print
        os.system(("useradd {}".format(user))
    else:
        print("User already exist, skipping it. ")
        print("##########################################")
        print()

# Condition to check if group exists or not. add if not exist.
exitcode = os.system("grep science /etc/group")
if exitcode != 0:
    print("Group science does not exist. Adding it.")
    print("#############################################")
    print()
    os.system("groupadd science")
else:
    print("Group already exist, skippinig it.")
    print("##############################################")
    print()

for user in userlist:
    print("Adding user {} in the science group".format(user))
    print("###################################################")
    print()
    os.system("usermod -G science {}".format(user))

print("Adding directory")
print("#####################################")
print()

if os.path. isdir("/opt/science_dir"):
    print("Directory already exist, skipping it")
else:
    os.mkdir("/opt/science_dir")

print("Assigning permission and ownership to the directory.")
print("#######################################################")
print()
os.system("chown :science/opt/science_dir")

os.system("chmod 770 /opt/science_dir")
```

- Check if the directory is owned by the group using the below command
```sh
ls -ld /opt/science_dir
```
![](Images/Owned%20by%20the%20group.png)

## Step-6: Clean up


