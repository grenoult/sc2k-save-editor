```
           ____  _                                            _ _ _             
  ___  ___|___ \| | __     ___  __ ___   _____        ___  __| (_) |_ ___  _ __ 
 / __|/ __| __) | |/ /____/ __|/ _` \ \ / / _ \_____ / _ \/ _` | | __/ _ \| '__|
 \__ \ (__ / __/|   <_____\__ \ (_| |\ V /  __/_____|  __/ (_| | | || (_) | |   
 |___/\___|_____|_|\_\    |___/\__,_| \_/ \___|      \___|\__,_|_|\__\___/|_|   
```

# sc2k-save-editor

Demo: https://sc2k-save-editor.pages.dev/

`*.sc2` file editor to update Sim City 2000 saved games. Simply upload your file, modify it and download the modified version.

## How it works?

### Reading the file
- With `FileReader` we can read "uploaded" files directly in browser. This is pretty amazing because it means we don't need a backend so we can modify files on the spot.
- Once the file is uploaded, it's read with `Uint8Array` function, the result will be an array of 8 bits unsigned integers representing the file.
- These integers are converted to a base 16 value to get a hexadecimal representation on the file.
- This hexadecimal value is stored in hidden HTML input so that we can keep it for saving later on.

### Modification
- Once file is read, we transform content and put it in HTML Form Input fields.
  - for example for the money, we get value between positions 158 and 166 (8 bytes), convert from hex to decimal. It's stored as a 8 bit unsigned value, so it goes from -2,147,483,648 to 2,147,483,647.
- Values can be modified by the user.

### Saving
* Once user submits the form, the file is rebuilt using the file stored in hidden input with the values changed in the form.
* File is modified as a blob, then a fake link is created (and removed) to download the file.

## Credits

This couldn't have been done without the extensive documentation:
 - https://github.com/dfloer/SC2k-docs/blob/master/sc2%20file%20spec.md