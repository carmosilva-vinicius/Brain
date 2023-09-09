File permissions determine the ways different users can interact with a file or directory. When listing a file with the `ls -l` [[CLI]] [[Linux]] command, the output includes permission information. The permissions are broken into three sets of three characters [pluralsight.com](https://www.pluralsight.com/guides/linux-permissions):

- User: The first set is for the user who owns the file. If your current account is the user owner of the file, then the first set of the three permissions will apply and the other permissions have no effect [dev.to](https://dev.to/larymak/understanding-permissions-on-linux-1h2e).
- Group: The second set of permissions applies to the user group that owns the file.
- Others: The final set of permissions is generally referred to as "others". "Others" permissions are applied when the account interacting with the file is neither the user owner nor in the group that owns the files [redhat.com](https://www.redhat.com/sysadmin/linux-file-permissions-explained).

d | rwx| rwx | rwx | + | 
-- | -- | -- |-- | --
The file type, technically not part of its permissions. See `info ls -n "What information is listed"` for an explanation of the possible values. | The permissions that the owner has over the file, explained below. | The permissions that the group has over the file, explained below. | The permissions that all the other users have over the file, explained below. | A single character that specifies whether an alternate access method applies to the file. When this character is a space, there is no alternate access method. A `.` character indicates a file with a security context, but no other alternate access method. A file with any other combination of alternate access methods is marked with a `+` character, for example in the case of [Access Control Lists](https://wiki.archlinux.org/title/Access_Control_Lists "Access Control Lists").

[AUR Source](https://wiki.archlinux.org/title/File_permissions_and_attributes)
