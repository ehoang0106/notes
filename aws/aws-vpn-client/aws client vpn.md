
generate certificate for server and user

- **Clone the Easy-RSA repository:**
    
    ```bash
    git clone https://github.com/OpenVPN/easy-rsa.git
    cd easy-rsa/easyrsa3
    ```
    
- **Initialize a new PKI environment:**
    
    ```bash
    ./easyrsa init-pki
    ```
    
- **Build a new Certificate Authority (CA):** You'll be prompted to enter a Common Name for your CA. You can leave it blank to use the default or provide a descriptive name (e.g., `ClientVPN-CA`).
    
    ```bash
    ./easyrsa build-ca nopass
    ```
    
- **Generate the server certificate and key:** You'll be prompted to enter a Common Name for the server. **It is crucial that this Common Name resembles a domain name** (e.g., `vpn.yourcompany.com` or `server.clientvpn.local`). If you use a simple name like `server`, the certificate might not appear in the AWS Client VPN console.
    
    ```bash
    ./easyrsa build-server-full vpn.yourcompany.com nopass
    ```
    
- **Generate the client certificate and key:** You'll be prompted to enter a Common Name for the client. Use a unique name for each user (e.g., `user1.client.vpn`). Repeat this step for each user who needs VPN access.
    
    ```bash
    ./easyrsa build-client-full user1.client.vpn nopass
    ```
    
- **Copy certificates and keys to a dedicated folder:** Create a directory to store your generated certificates and keys for easy access. Remember to use the full Common Name for the server certificate.
    
    ```bash
    mkdir -p ~/client_vpn_certs
    cp pki/ca.crt ~/client_vpn_certs/
    cp pki/issued/vpn.yourcompany.com.crt ~/client_vpn_certs/
    cp pki/private/vpn.yourcompany.com.key ~/client_vpn_certs/
    cp pki/issued/user1.client.vpn.crt ~/client_vpn_certs/
    cp pki/private/user1.client.vpn.key ~/client_vpn_certs/
    ```