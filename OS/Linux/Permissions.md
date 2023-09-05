d | rwx| rwx | rwx | + | 
-- | -- | -- |-- | --
The file type, technically not part of its permissions. See `info ls -n "What information is listed"` for an explanation of the possible values. | The permissions that the owner has over the file, explained below. | The permissions that the group has over the file, explained below. | The permissions that all the other users have over the file, explained below. | A single character that specifies whether an alternate access method applies to the file. When this character is a space, there is no alternate access method. A `.` character indicates a file with a security context, but no other alternate access method. A file with any other combination of alternate access methods is marked with a `+` character, for example in the case of [Access Control Lists](https://wiki.archlinux.org/title/Access_Control_Lists "Access Control Lists").

[AUR Source](https://wiki.archlinux.org/title/File_permissions_and_attributes)
