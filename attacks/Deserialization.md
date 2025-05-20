# Deserialization

Tools that can be used:

ysoserial → java (`java -jar ysoserial-all.jar CommonsCollections4 'rm -rf'`)

ysoserial.exe → c#

phpgcc → php (`./phpggc Symfony/RCE4 exec 'rm /home/carlos/morale.txt' | base64`)

---

- Update the data type label for the access token by replacing `s` with `i`.
- Edit the serialized data so that the `avatar_link` points to `/home/carlos/morale.txt`. Remember to update the length indicator. The modified attribute should look like this:
- In the source code, notice the `CustomTemplate` class contains the `__destruct()` magic method. This will invoke the `unlink()` method on the `lock_file_path` attribute, which will delete the file on this path.
- You now need to construct a valid cookie containing this malicious object and sign it correctly using the secret key you obtained earlier. You can use the following PHP script to do this. Before running the script, you just need to make the following changes: