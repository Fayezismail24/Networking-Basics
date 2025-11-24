### line console 0:

- **Refers to**: Configuring the console line, which is the physical or direct connection to the device (usually through a serial cable or terminal software)

- **Purpose**: This command is used to configure settings for accessing the device through the console port

- **Password**:  IT sets a password that must be entered to access the device through the console

#### Line Console 0 Password
```javascript
Switch(config)#line console 0
Switch(config-line)#password [Enter Password Here]
Switch(config-line)#login
```

<img width="813" height="665" alt="image" src="https://github.com/user-attachments/assets/aeca8acf-fdd7-4d88-97a9-dcdeaf243032" />

---------------------------------


### Privileged EXEC Access Control:
- **Refer to**: Used to set a password for accessing privileged EXEC mode (global configuration mode). It secures the level of access required for performing advanced configuration tasks on the device.
- **Purpose**: Protects access to higher privilege levels and ensures that only authorized users can execute sensitive or configuration commands
```javascript
Switch(config)#enable secret [Enter Secret Here]

```


### Encrypt all Password:
- **Refer to**: This command enables the encryption of all plaintext passwords in the configuration file. It is used to secure passwords, ensuring that they are not visible in clear text when viewing the configuration
- ```javascript
  Switch(config)# service password-encryption
  ```
   










