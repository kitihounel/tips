# Get wi-fi password

- Open a command prompt window.
- Run the following command to list all wireless network profiles saved on the computer.

  ```sh
  netsh wlan show profile
  ```

- Now to get detailled information about a network and its password, run:

  ```sh
  netsh wlan show profile name="<Network SSID>" key=clear
  ```

## Notes

- In the article where we find this tip, it is said to open the command prompt in admin mode.
  But we tried with a simple user account, and we were able to get what we were looking for.

## Source

- [GeeksForGeeks](https://www.geeksforgeeks.org/how-to-find-wi-fi-password-using-cmd)
