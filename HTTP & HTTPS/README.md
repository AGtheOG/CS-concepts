<xaiArtifact artifact_id="693db1a5-7c24-4404-9411-bf7734418dc8" artifact_version_id="20e83b8f-e399-46dd-ad3c-c4da4c3ba069" title="HTTP_vs_HTTPS.md" contentType="text/markdown">

# Understanding HTTP vs HTTPS: Security and Key Exchange Explained

## HTTP

**Protocol**: HyperText Transfer Protocol  
**OSI Layer**: Application (L7)  
**Encryption**: ❌ None — data (headers, JWT, cookies, passwords) is in plain text  
**Port**: 80 (default)  
**Use case**: Testing, internal networks, not secure on the internet  

## HTTPS

**Protocol**: HTTP over TLS/SSL  
**OSI Layers**: Application (L7) + Presentation (L6) (TLS encryption)  
**Encryption**: ✅ All HTTP content (headers + body, including JWTs) is encrypted  
**Port**: 443 (default)  
**Use case**: Always use on public internet (security, privacy, trust)  

## Key Difference

With **HTTP**:  
Wireshark (or anyone sniffing) can directly see:  
```
Authorization: Bearer eyJhbGciOi...
```

With **HTTPS**:  
Wireshark sees only encrypted blobs unless you have the TLS keys.  

👉 **Conclusion**: JWTs must be sent only over HTTPS — otherwise, anyone on the same network can steal them.

## Why Sending Encrypted Data with the Key is Insecure

If you encrypt data and send the key along with it:  
- Anyone sniffing the traffic can grab both the ciphertext and the key.  
- They can decrypt it immediately.  
- 👉 This is effectively the same as sending plain text.

### Why HTTPS is Different

HTTPS (TLS) uses **asymmetric cryptography** to avoid this issue:  
- The server has a **public key** and a **private key**.  
- The client uses the public key to encrypt a random symmetric session key.  
- Only the server (with the private key) can decrypt this session key.  
- Both sides then use the symmetric key for fast encryption.  
- ⚠️ **Key point**: The symmetric key is never sent in the clear.

So:  
- Rolling your own scheme (sending encrypted data + key) is insecure.  
- HTTPS/TLS ensures a secure key exchange because the private key never leaves the server.  
- ✅ **Best practice**: Don’t invent your own crypto. Use TLS.

## How Asymmetric Cryptography Works in HTTPS

Here’s the key rule of RSA-style encryption:  
- Data encrypted with a **public key** can only be decrypted with the **private key**.  
- Data encrypted with a **private key** can be verified (decrypted) with the **public key** (used for digital signatures).  

####How TLS Uses HTTPS in a Handshake?

Here’s how the process happens when you visit a secure website:

🔑 Step 1 – Server shares its public key

The client connects and receives the server’s public key as part of its SSL certificate.

🔑 Step 2 – Client generates a session key

The client randomly generates a symmetric session key, which will be used for encrypting all further communication.

🔑 Step 3 – Client encrypts session key

The client encrypts the session key using the server’s public key and sends it to the server.

🔑 Step 4 – Server decrypts session key

The server uses its private key to decrypt the session key.

🔑 Step 5 – Both sides use the session key

Both the client and server now use this shared symmetric key to encrypt the rest of the communication, which is fast and efficient.

🔑 Step 6 – Authentication and trust

The server’s certificate, issued by a trusted Certificate Authority (CA), ensures the client is connecting to the right server and not an imposter.

### TLS Handshake Step-by-Step

During the HTTPS/TLS handshake:  
1. The client gets the server’s **public key** (from the SSL certificate).  
2. The client generates a random **session key** (symmetric key).  
3. The client encrypts the session key with the server’s **public key** and sends it.  
4. Only the server, with its **private key**, can decrypt and recover the session key.  
5. Both sides use the session key for fast symmetric encryption of all data.  

⚠️ **Important**:  
- If you only have the public key, you can encrypt but not decrypt.  
- The client cannot decrypt its own message once it’s encrypted with the server’s public key. Only the server can, using the private key.  
- 👉 The private key is the “lock-opener.” Without it, ciphertext remains unreadable.

## Final Thoughts

Using HTTPS ensures that sensitive data, like JWTs, is protected through secure key exchange and encryption. Avoid custom encryption schemes where keys are sent alongside data, as they offer no real security. Stick to HTTPS for safe, reliable communication over the internet.

</xaiArtifact>
