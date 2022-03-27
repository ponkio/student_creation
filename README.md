# Student creation

## Descritpion

A basic ansible playbook to bootstrap a linux server with a plethora of users and groups conviently organized for a classroom environment. As well as disable ssh password authentication. 

## Dependencies

In order to run this playbook you will need to install the following packages:

```
python3
pip
pipenv
```

After the packages are installed verify you have ssh access as a user with passwordless sudo permissions to the server you are targeting. 

_It is HIGHLY recommended you setup key authentication to the target server with `ssh-copy-id` prior to running this_


## Setup and installation

First clone the repo and setup the virtual environment.

```
git clone https://github.com/ponkio/student_creation 
cd student_creation/
pipenv shell
pip install .
```

## Configuration

Configuration is stored in `vars.yml` here is an example a more complex configuration:

```
classes:
    instructors:
        - name: "Administrator"
          username: admin
    class_123:
        - name: "John Doe"
          username: JD12345
    class_456
        - name: "Jane Doe"
          username: JD67890
        - name: "Not JohnDoe"
          username: NJ95684
```

If the instructors class exists then ansible will automatically modify `/etc/sudoers` to allow for users in the instructors group to execute commands with sudo. 

A group will be created for each item in under `classes:` in the above example 3 groups would be created with 1 group having sudo access. 

In each class or group is a list of users. Each user will be created and assigned the group they are under. The default password for each user is the username. Each user will also be generated an SSH private key to authenticate with. This private key is downloaded and stored (relative to where you ran the script) `keys/`. 

## Running the script

Run the `ansible-playbook` command and modify the `-i` parameter to your target server (_the `,` is very important_). And `-u` with the user that has key authentication setup with the target server(s). You can find more details on ways to connect to target servers [here](https://docs.ansible.com/ansible/latest/user_guide/connection_details.html). 

```
ansible-playbook -i 1.2.3.4, main.yml -u ponkio
```

Afterwards you should now have ssh keys in `keys/` in the same structure as your configuration file. 

_Note: You are able to use an inventory file to target multiple servers. See [ansible docs](https://docs.ansible.com/ansible/latest/network/getting_started/first_inventory.html) for details_
=======
# Rose Students

## Pre-requisites
In order to run this playbook you will need the following installed: 

```
python >= 3.6 
pip
ansible
pipenv
```
TEST DUMMY API key: 7fd1a60b01f91b314f59955a4e4d4e80d8edf11d
