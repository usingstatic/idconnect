# id Connect
Primer about distributed identity management

# Why

# JWT
header = {...}
payload = {
"sub": "",
"iat": <seconds from epoch>,
"exp": <seconds from epoch>,
}
signature = {...}

# Anonymous Identity Verification

## Shared Secret Tokens
1. Create a strong secret that cannot be guessed easily.
2. Securely provide it to your clients
4. create a JWT containing whatever information you want
5. Sign it with HMAC
6. Verify the token has not been tempered by anyone who doesn't know the secret

Pros and cons
* Anyone with the shared secret can claim to be anyone else with no way of claiming identity.

## RSA PKI Tokens
1. The client creates an RSA keypair and stores it securely
2. Create a JWT signed with the RSA keypair (RSA-SHA256 for example)
3. Send the public key (for example in the JWT)
4. Verify the token has not been tempered with
5. Only holder of the private key can sign the token, no one can fake that specific public key

header = {...}
payload = {
"pub": <RSA public key>,
"sub": "",
"iat": <seconds from epoch>,
"exp": <seconds from epoch>,
}
signature = {...}

Pros and cons
* Key can get lost
* RSA is considered weak
* The signature and public key is big, creating large requests.

## EC-DSA PKI Tokens
1. The client creates an EC-DSA keypair and stores it securely
2. Create a JWT signed with the EC-DSA keypair
3. Send the public key (for example in the JWT)
4. Verify the token has not been tempered with
5. Only holder of the private key can sign the token, no one can fake that specific public key

Pros and cons
* Key can get still get lost
* Contemporary security
* The signature is much smaller

## Generating Unique Identity From Public Key
Calculate a unique identity
1. Take the public key and calculate sha256
2. On the sha256 calculate RIPEMD160
3. Take the result and encode in Base64Url or Base58

To verify the identity
1. Take the public key from the JWT
2. Calculate the identity and validate the result

* The JWT is signed so it cannot be tempered
* The identity is derived from the public key so it cannot be 
