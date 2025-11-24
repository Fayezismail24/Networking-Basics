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

<img width="221" height="102" alt="image" src="https://github.com/user-attachments/assets/4145207b-979c-4d29-9343-e99d37645966" />

---------------------------------


### Privileged EXEC Access Control:
- **Refer to**: Used to set a password for accessing privileged EXEC mode (global configuration mode). It secures the level of access required for performing advanced configuration tasks on the device.
- **Purpose**: Protects access to higher privilege levels and ensures that only authorized users can execute sensitive or configuration commands
```javascript
Switch(config)#enable secret [Enter Secret Here]

```
<img width="92" height="34" alt="image" src="https://github.com/user-attachments/assets/685aea02-6e4b-4300-96d2-1f83cff6c599" />



### Encrypt all Password:
- **Refer to**: This command enables the encryption of all plaintext passwords in the configuration file. It is used to secure passwords, ensuring that they are not visible in clear text when viewing the configuration
- ```javascript
  Switch(config)# service password-encryption
  ```


  <img width="207" height="170" alt="image" src="https://github.com/user-attachments/assets/06e7ba80-e6f6-498d-8a0b-d52325b7a2bf" />
  <img width="297" height="171" alt="image" src="https://github.com/user-attachments/assets/b8a2dea8-2883-4531-b86b-cc2e28bb1765" />


  

   










