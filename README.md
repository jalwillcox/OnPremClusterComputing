# On-Prem Cluster Computing
Jon Willcox (willcox@broadinstitute.org)

03/26/2024

These are some instructions to get set up for on-prem cluster computing in the Ellinor Lab at The Broad Institute. 

## Step 1: Getting access to /medpop/afib

Submit request [here](https://broad.service-now.com/sp?id=sc_category&sys_id=1680a9bd4fb662005c1423d18110c7b7&catalog_id=e0d08b13c3330100c8b837659bba8fb4)

Patrick will have to give the ok, but that’s usually quick.

Once you have access, you can log on with the command below if you are on-site or connected to the Broad [VPN](https://intranet.broadinstitute.org/bits/service-catalog/accounts-access/vpn-access-two-factor-authentication).

```
# Replace 'userid' with your user ID
ssh userid@login.broadinstitute.org
```

## Step 2: Set up key pair

This will let you login to the cluster from your laptop without using a password.

BITS instructions are [here](https://broad.service-now.com/sp?id=kb_article&sys_id=04e9f76c1b0404142cac84ccdd4bcbc1)

## Step 3: Set up to transfer files

If you have a Broad-issued computer, you can map a network drive to your computer

BITS instructions are [here](https://intranet.broadinstitute.org/bits/service-catalog/compute-resources/map-network-drive)

Ellinor Lab servers:
| directory | server |
| ------- | ------ |
| `/medpop/afib` | smb://helium/medpop_afib |
| `/medpop/bayercvd` | smb://hydrogen/medpop_bayercvd |

For non-Broad-issued computers BITS instructions are [here](https://broad.service-now.com/sp?id=kb_article&sys_id=56234f1047aba99011484438946d4320)

## Step 4 (optional): Customize bash configuration

The following lines set a few defaults that may be useful:

```
# Include a path with some useful scripts 
PATH=$PATH:/medpop/afib/willcox/bin

# automatically load UGER on openening session
use UGER

# Reset LESS default
LESS=-c

        # the following lines should go within the if-statment,
        #   e.g. just before the line 'fi'

        # load a few commonly used dotkits
        use .google-cloud-sdk
        use .anaconda3-2022.10
        use GCC-5.2
        use R-4.1


```

These can be added to the file `~/.my.bashrc` using an editor such as `vim` or `nano`, or if you'd prefer, you can copy a template using the following lines:

```
# save your current ~/.my.bashrc as ~/.my.bashrc.backup
mv ~/.my.bashrc ~/.my.bashrc.backup

# copy the template over to ~/.my.bashrc
cp /medpop/afib/willcox/resources/.my.bashrc ~/.my.bashrc
```

## Step 5: Make yourself a working directory

For example, if you will mainly be working in `/medpop/afib`, you can use the command:

```
# Replace userid with your user ID
mkdir /medpop/afib/userid
```

This will be a location for you to store data and perform operations.

## Useful resources and commands

- [Here](https://ryanstutorials.net/linuxtutorial/) is a useful tutorial to learn basics for operating in a linux/command-line environment.
- [Here](https://ryanstutorials.net/bash-scripting-tutorial/) is a useful tutorial for learning the basics of Bash.

Because space on-prem is limited, it is helpful to keep tabs on your disk usage:

```
# This command will display some basic information about availible space on your filesystem
# Replace '/medpop/afib' with the filesystem you would like to check
df -h /medpop/afib

# This command will display the disk usage for your working directory
# Replace userid with your user ID
du -sh /medpop/afib/userid
```



