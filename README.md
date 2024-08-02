# File permissions in Linux

## Objective

The File Permission Lab project aimed to changed multiple permissions to match the level of authorization an organization wanted for files and directories in the projects directory. 

### Skills Learned

- Knowledge of file and directory structures, including permissions, ownership, and group attributes.
- Grasping the importance of file permissions in maintaining system security and preventing unauthorized access.
- Ability to diagnose and rectify permission-related issues, such as troubleshooting access denied errors.
- Careful analysis of file permissions to identify potential security risks.
- Understanding the implications of different permission combinations.
- Ability to clearly document changes made to file permissions for future reference.

### Tools Used

- Linux command line.
- ls: To view file and directory information, including permissions.
- chmod: To change file permissions.
- chown: To change file ownership.
- id: To view user and group information.
  
## Steps

The following code demonstrates how I used Linux commands to determine the existing permissions set for a specific directory in the file system.
![Screenshot 2024-08-02 114122](https://github.com/user-attachments/assets/40c98b30-5625-4e9b-9b92-749fc77351c9)

*Ref 1: File System*

The first line of the screenshot displays the command I entered, and the other lines display the output. The code lists all contents of the project's directory. I used the ls command with the -la option to display a detailed listing of the file contents that also returned hidden files. The output of my command indicates that there is one directory named drafts, one hidden file named .project_x.txt, and five other project files. The 10-character string in the first column represents the permissions set on each file or directory.

## Describe the permissions string

The 10-character string can be deconstructed to determine who is authorized to access the file and their specific permissions. The characters and what they represent are as follows:

1st character: This character is either a d or hyphen (-) and indicates the file type. If it’s a d, it’s a directory. If it’s a hyphen (-), it’s a regular file.

2nd-4th characters: These characters indicate the read (r), write (w), and execute (x) permissions for the user. When one of these characters is a hyphen (-) instead, it indicates that this permission is not granted to the user.

5th-7th characters: These characters indicate the read (r), write (w), and execute (x) permissions for the group. When one of these characters is a hyphen (-) instead, it indicates that this permission is not granted for the group.

8th-10th characters: These characters indicate the read (r), write (w), and execute (x) permissions for other. This owner type consists of all other users on the system apart from the user and the group. When one of these characters is a hyphen (-) instead, that indicates that this permission is not granted for other.

For example, the file permissions for project_t.txt are -rw-rw-r--. Since the first character is a hyphen (-), this indicates that project_t.txt is a file, not a directory. The second, fifth, and eighth characters are all r, which indicates that user, group, and other all have read permissions. The third and sixth characters are w, which indicates that only the user and group have write permissions. No one has execute permissions for project_t.txt.

## Change file permissions

The organization determined that other shouldn't have write access to any of their files. To comply with this, I referred to the file permissions that I previously returned. I determined project_k.txt must have the write access removed for other.

The following code demonstrates how I used Linux commands to do this:

![Screenshot 2024-08-02 115028](https://github.com/user-attachments/assets/2c943a2d-fbbc-48b6-adef-584b02965af4)

*Ref 2: File System*

The first two lines of the screenshot display the commands I entered, and the other lines display the output of the second command. The chmod command changes the permissions on files and directories. The first argument indicates what permissions should be changed, and the second argument specifies the file or directory. In this example, I removed write permissions from other for the project_k.txt file. After this, I used ls -la to review the updates I made.

## Change file permissions on a hidden file

The research team at the organization recently archived project_x.txt. They do not want anyone to have write access to this project, but the user and group should have read access. 

The following code demonstrates how I used Linux commands to change the permissions:

![Screenshot 2024-08-02 115433](https://github.com/user-attachments/assets/2915efa4-8e42-467c-b0c4-3336bf524a02)

*Ref 3: File System*

The first two lines of the screenshot display the commands I entered, and the other lines display the output of the second command. I know .project_x.txt is a hidden file because it starts with a period (.). In this example, I removed write permissions from the user and group, and added read permissions to the group. I removed write permissions from the user with u-w. Then, I removed write permissions from the group with g-w, and added read permissions to the group with g+r. 

## Change directory permissions

The organization only wants the researcher2 user to have access to the drafts directory and its contents. This means that no one other than researcher2 should have execute permissions.

The following code demonstrates how I used Linux commands to change the permissions:

![Screenshot 2024-08-02 115831](https://github.com/user-attachments/assets/c4883f48-fd8e-49ca-b497-6a46bd137df5)

*Ref 4: File System*

The output here displays the permission listing for several files and directories. Line 1 indicates the current directory (projects), and line 2 indicates the parent directory (home). Line 3 indicates a regular file titled .project_x.txt. Line 4 is the directory (drafts) with restricted permissions. Here you can see that only researcher2 has execute permissions.  It was previously determined that the group had execute permissions, so I used the chmod command to remove them. The researcher2 user already had execute permissions, so they did not need to be added.
