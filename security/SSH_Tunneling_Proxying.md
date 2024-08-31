
### Practical Work on SSH Tunneling and Proxying in Linux

#### 1. **Introduction**

- **Objective:** Understand how to set up and use SSH tunneling and proxying for secure communication.
- **Requirements:** Basic knowledge of Linux commands, SSH installed on both client and server machines.

#### 2. **Preparation**

- **Setup Environment:** 
  - **Server:** Ensure you have access to a remote Linux server with SSH enabled.
  - **Client:** Have a Linux machine from which you will initiate the SSH tunnel.

#### 3. **Creating an SSH Tunnel**

**Step 1: Set Up SSH Tunnel for Local Port Forwarding**

- **Description:** Local port forwarding allows you to forward a port from your local machine to a port on a remote server.

- **Command:**
  ```bash
  ssh -L local_port:target_host:target_port username@remote_server
  ```
  - `local_port`: Port on your local machine (e.g., `8080`).
  - `target_host`: Hostname or IP address of the target server you want to access (e.g., `localhost`).
  - `target_port`: Port on the target server (e.g., `80` for HTTP).
  - `username`: Your SSH username.
  - `remote_server`: The remote server’s address.

- **Example:**
  ```bash
  ssh -L 8080:localhost:80 user@remote-server.com
  ```
  This command forwards local port 8080 to port 80 on `remote-server.com`.

**Step 2: Test the Local Port Forwarding**

- Open a web browser or use `curl` to access the forwarded port:
  ```bash
  curl http://localhost:8080
  ```
  You should see the web page or response from the target server.

#### 4. **Remote Port Forwarding**

**Step 1: Set Up Remote Port Forwarding**

- **Description:** Remote port forwarding allows a remote server to forward a port to a local machine.

- **Command:**
  ```bash
  ssh -R remote_port:local_host:local_port username@remote_server
  ```
  - `remote_port`: Port on the remote server.
  - `local_host`: Local machine's address (e.g., `localhost`).
  - `local_port`: Port on your local machine.
  - `username`: Your SSH username.
  - `remote_server`: The remote server’s address.

- **Example:**
  ```bash
  ssh -R 9090:localhost:3000 user@remote-server.com
  ```
  This forwards port 9090 on `remote-server.com` to port 3000 on your local machine.

**Step 2: Test the Remote Port Forwarding**

- Access the forwarded port from the remote server:
  ```bash
  curl http://localhost:9090
  ```
  Ensure the remote server can reach your local service running on port 3000.

#### 5. **Dynamic Port Forwarding (SOCKS Proxy)**

**Step 1: Set Up Dynamic Port Forwarding**

- **Description:** Dynamic port forwarding allows you to create a SOCKS proxy server.

- **Command:**
  ```bash
  ssh -D local_port username@remote_server
  ```
  - `local_port`: Port on your local machine where the SOCKS proxy will listen (e.g., `1080`).
  - `username`: Your SSH username.
  - `remote_server`: The remote server’s address.

- **Example:**
  ```bash
  ssh -D 1080 user@remote-server.com
  ```

**Step 2: Configure Applications to Use the SOCKS Proxy**

- **For Web Browsers:**
  - Go to network settings and configure the proxy settings to use `SOCKS5` with `localhost` and port `1080`.

- **For Command Line Tools:**
  - You can use tools like `curl` with the `--proxy` option:
    ```bash
    curl --proxy socks5h://localhost:1080 http://example.com
    ```

#### 6. **Troubleshooting**

- **Check SSH Logs:** Review SSH logs on both client and server for errors.
- **Verify Ports:** Use tools like `netstat` or `ss` to check if the ports are being forwarded correctly.
- **Test Connectivity:** Ensure the remote server can reach the local machine and vice versa.

#### 7. **Conclusion**

- **Summary:** SSH tunneling and proxying are powerful tools for securing network communications. Practice using local, remote, and dynamic port forwarding to become proficient in managing network traffic securely.


