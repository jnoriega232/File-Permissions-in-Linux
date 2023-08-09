# File Permissions in Linux

## Project Description
The research team in the fictional organization I'm describing is in the process of revising the file permissions for specific files and directories located within the  ```projects``` directory. The existing permissions do not accurately align with the intended level of authorization. Ensuring that these permissions are reviewed and adjusted appropriately is crucial for maintaining the security of their system. To achieve this objective, I undertook the following actions:

## Check File and Directory Details
The provided code exemplifies my utilization of Linux commands to ascertain the current permissions configured for a particular directory within the file system.

<p align="center">
<img src="https://i.imgur.com/LgGnWj5.png" height="70%" width="70%" alt="Azure Free Account"/>

In the screenshot, the initial line showcases the command I input, while subsequent lines exhibit the resulting output. The code comprehensively enumerates the items within the ```projects``` directory. I employed the ```ls``` command with the ```-la``` option to reveal an elaborate list of file contents, encompassing hidden files. The output of my execution discloses the presence of a directory named ```drafts```, a concealed file labeled ```.project_x.txt```, and four additional project files. The initial 10-character string in the first column symbolizes the permissions designated for each individual file or directory.

## Describe the Permissions String
The 10-character sequence can be dissected to discern the individuals with authorized access to the file and their respective permissions. The characters have the following interpretations:

- 1st Character: A ```d``` or hyphen (```-```) signifies the file type. ```d``` indicates a directory, while (```-```) indicates a regular file.

- 2nd-4th Characters: These characters denote the user's read (```r```), write (```w```), and execute (```x```) permissions. A hyphen (```-```) signifies the absence of the corresponding permission.

- 5th-7th Characters: These characters denote the group's read (```r```), write (```w```), and execute (```x```) permissions. A hyphen (```-```) signifies the absence of the respective permission.

- 8th-10th Characters: These characters denote the "other" category's read (```r```), write (```w```), and execute (```x```) permissions. This category encompasses all users aside from the user and the group. A hyphen (```-```) indicates the lack of the specified permission.

As an illustration, let's take the file permissions of ```project_t.txt``` as an instance: ```-rw-rw-r--```. With a hyphen (```-```) as the first character, it's evident that ```project_t.txt``` is a file rather than a directory. The presence of ```r``` in the second, fifth, and eighth positions signifies that the user, group, and others possess read permissions. The third and sixth positions bear ```w```, indicating that exclusively the user and group hold write permissions. Notably, no entity has execute permissions for ```project_t.txt```.

## Change File Permissions
The organization concluded that no write access should be granted to "other" for any of their files. To align with this directive, I revisited the file permissions I had previously retrieved. Upon analysis, I identified that write access for "other" needs to be revoked from ```project_k.txt```.

The subsequent code exemplifies my utilization of Linux commands to accomplish this task:

<p align="center">
<img src="https://i.imgur.com/hq5GtTH.png" height="70%" width="70%" alt="Azure Free Account"/>

The initial pair of lines within the screenshot showcases the commands I input, while the subsequent lines present the outcome of the second command. Utilizing the ```chmod``` command, permissions on files and directories are modified. The first argument dictates the permissions to be altered, and the second argument designates the file or directory. In this instance, I eliminated write permissions for "other" on the ```project_k.txt``` file. Following this adjustment, I employed ```ls -la``` to assess the modifications I implemented.

## Change File Permissions on a Hidden File
The research team within my organization has recently archived project_x.txt. Their intention is to restrict write access to this project for all individuals, while ensuring that only the user and the group retain read access.

The subsequent code exemplifies my utilization of Linux commands to modify the permissions:

<p align="center">
<img src="https://i.imgur.com/XutGSOe.png" height="70%" width="70%" alt="Azure Free Account"/>

The initial pair of lines within the screenshot presents the commands I input, while the subsequent lines depict the results of the second command. Recognizing that ```.project_x.txt``` is a concealed file due to its initial period (```.```), I proceeded to make modifications. Specifically, I withdrew write permissions from both the user and the group, simultaneously introducing read permissions for the group. Achieving this involved the utilization of ```u-w``` to remove write permissions from the user, followed by ```g-w``` to eliminate write permissions from the group, and ```g+r``` to append read permissions to the group.

## Change Directory Permissions
Within my organization, the directive is to restrict access to the drafts directory and its contents exclusively to the researcher2 user. As such, the aim is to ensure that execute permissions are granted solely to researcher2, with no other individuals having such privileges.

Below is an example showcasing my use of Linux commands to modify permissions:

<p align="center">
<img src="https://i.imgur.com/TzQORxo.png" height="70%" width="70%" alt="Azure Free Account"/>

The initial pair of lines within the screenshot reveals the commands I input, while the subsequent lines exhibit the outcome of the second command. Building upon my earlier observation that the group possessed execute permissions, I employed the chmod command to eliminate them. Notably, the researcher2 user was already endowed with execute permissions, obviating the need for their addition.

## Summary
I undertook several permission changes to align with my organization's desired level of authorization for files and directories within the projects directory. To initiate this process, I utilized the "ls -la" command to inspect the directory's existing permissions. This examination served as the foundation for my subsequent actions. Subsequently, I employed the "chmod" command on multiple occasions to systematically modify permissions across files and directories.
