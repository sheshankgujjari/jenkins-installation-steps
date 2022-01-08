### PreRequisites

1. Create a new target server or use existing server (LInux or Ubuntu)

2. Generate SSH key ```ssh-keygen -t rsa -b 4096 -m PEM```

3. Press enter for all default values

4. Enter passphrase (empty for no passphrase): 
Enter same passphrase again: 
Your identification has been saved in /root/.ssh/id_rsa.
Your public key has been saved in /root/.ssh/id_rsa.pub.

5. Copy the private key from ```/root/.ssh/id_rsa```


### Using Publish Over SSH plugin

1. Add publish over ssh plugin from Jenkins --> Manage Plugins section Using "Publish over SSH" Plugin Ref: https://plugins.jenkins.io/publish-over-ssh/

2. Restart Jenkins after plugin has been installed

3. Visit: Jenkins > Manage Jenkins > Configure System > Publish over SSH

4. If the private key is encrypted, then you will need to enter the passphrase for the key into the "Passphrase" field, otherwise leave it alone.

5. Leave the "Path to key" field empty as this will be ignored anyway when you use a pasted key (next step)

6. Copy and paste the contents of the private key which you copied earlier into the "Key" field

7. Under "SSH Servers", "Add" a new server configuration for your target server. Name of the server, Hostname and username

### Using stored Global credentials

1. Using Stored Global Credentials
Visit: Jenkins > Manage Jenkins > Manage Credentials > System > Global credentials (unrestricted) > Add Credentials

2. Kind: "SSH Username with private key"

3. Scope: "Global"

4. ID: [CREAT A UNIQUE ID FOR THIS KEY]

5. Description: [optionally, enter a decription]

6. Username: [USERNAME JENKINS WILL USE TO CONNECT TO REMOTE SERVER]

7. Private Key: [select "Enter directly"]

8. Key: [paste the contents of the private key (id_rsa per the above article)]

9. Passphrase: [enter the passphrase for the key, or leave it blank if the key is not encrypted]


### Using SSH agent plugin

1. Add ssh agent plugin from Jenkins --> Manage Plugins section 
