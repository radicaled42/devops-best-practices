# SSL Protocol

## What is SSL/TLS?

SSL/TLS uses certificates to establish an encrypted link between a server and a client. This allows sensitive information like credit card details to be transmitted securely over the internet.

The certificate contains a public key that authenticates the website’s identity and allows for encrypted data transfer through asymmetric, or public-key cryptography. The matching private key is kept secret on the server.

## What is an SSL certificate?

SSL can only be implemented by websites that have an SSL certificate (technically a "TLS certificate"). An SSL certificate is like an ID card or a badge that proves someone is who they say they are. SSL certificates are stored and displayed on the Web by a website's or application's server.

One of the most important pieces of information in an SSL certificate is the website's public key. The public key makes encryption and authentication possible. A user's device views the public key and uses it to establish secure encryption keys with the web server. Meanwhile the web server also has a private key that is kept secret; the private key decrypts data encrypted with the public key.

Certificate authorities (CA) are responsible for issuing SSL certificates.

## What are the benefits of SSL

- Safeguards sensitive information — To establish and maintain secure connections with a website server, browsers verify the SSL certificate of the website. SSL technology plays a crucial role in encrypting all communication between your browser and the website, ensuring the protection of private data.
- Enhances customer trust — Informed online users value privacy and seek to trust the websites they visit. A website secured with SSL displays the green padlock icon, instilling confidence in customers. SSL protection assures customers that their data is safeguarded when shared with your business.
- Ensures regulatory compliance — Certain businesses are required to comply with industry regulations governing data confidentiality and security. For instance, entities in the payment card industry must adhere to PCI DSS standards, which mandate securing web servers with SSL certificates for secure online transactions.
- Boosts SEO — Major search engines consider SSL protection as a ranking factor for search engine optimization. Consequently, a website with SSL encryption is likely to achieve higher rankings compared to a similar website lacking an SSL certificate. This, in turn, attracts more visitors from search engines to the SSL-protected website.

## High-level flow in SSL Handshake

Browsers initiate a secure connection with the web server using the SSL certificate through the SSL handshake. The SSL handshake is an integral aspect of the Hypertext Transfer Protocol Secure (HTTPS) communication technology, which combines HTTP and SSL. HTTP serves as a protocol for browsers to transmit information in plain text to a web server. Since HTTP transmits unencrypted data, it exposes information sent from a browser to potential interception and reading by third parties. To ensure fully secure communication, browsers utilize HTTP with SSL, commonly known as HTTPS. For more understanding on HTTP please read my previous blog on HTTP with link below.

- The browser initiates a secure connection to an SSL-protected website, establishing a link with the web server.
- To authenticate the web server, the browser requests identifiable information.
- In response, the web server transmits the SSL certificate, encompassing a public key.
- The browser scrutinizes the SSL certificate for validity and domain matching. Once satisfied, it utilizes the public key to encrypt and dispatch a message containing a confidential session key.
- The web server decrypts the message using its private key, extracting the session key. Subsequently, it encrypts and sends an acknowledgment message to the browser using the session key.
- With both the browser and web server now utilizing the same session key, they transition to secure message exchange.

**Bibliography**:
- https://www.cloudflare.com/learning/ssl/what-is-ssl/
- https://www.ssl.com/article/what-is-ssl-tls-an-in-depth-guide/
- https://medium.com/codenx/technology-security-22641732382f
- https://medium.com/codenx/technology-security-22641732382f