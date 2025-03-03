# LUKS-password from the command line

A LUKS-password for a block device can be set with the command line. This code create a template of all LUKS in your system.

```
for i in a b c d e f g h i j k l m n o p q r s t u v w x y z ; do
    sudo cryptsetup luksDump /dev/sd$i 2>/dev/null | grep -E '^UUID' | awk '{print $2}' | xargs -r -I '{}' -- echo "echo -n 'Your VERy secret LuKsPassw0rd.' | secret-tool store --label='{}' gvfs-luks-uuid '{}' # /dev/sd$i" || true
done
```

The template now looks like:

```
echo -n 'Your VERy secret LuKsPassw0rd.' | secret-tool store --label='a6ed5dec-ed6a-11ef-87f0-078a2d847fa1' gvfs-luks-uuid 'a6ed5dec-ed6a-11ef-87f0-078a2d847fa1' # /dev/sda
echo -n 'Your VERy secret LuKsPassw0rd.' | secret-tool store --label='405b9dac-d671-11ee-8f67-e35b9e93cabd' gvfs-luks-uuid '405b9dac-d671-11ee-8f67-e35b9e93cabd' # /dev/sdb
```

You can execute your selected command lines as the user that should have the password in his/hers keyring.

Make sure you empty the command history for all users.
