# examples use RSA, but you should look up when to use RSA vs EC

# generate key pair
openssl genrsa -out keys/keypair.pem 8192

# extract public key
openssl rsa -in keys/keypair.pem -pubout -out keys/pubkey.pem

# ENCRYPT TO SEND MESSAGE
# encrypt message with public key (use intended recipients public key, not your own)
PLAINTEXT=./key-pair-operations.md
sudo openssl pkeyutl -encrypt -in $PLAINTEXT -out $PLAINTEXT.encrypt -pubin -inkey keys/pubkey.pem

# DECRYPT RECEIVED MESSAGE
# decrypt message with private key
ENCRYPTED=./key-pair-operations.md.encrypt
DECRYPTED_OUTPUT=./decrypted.md
sudo openssl pkeyutl -decrypt -in $ENCRYPTED -out $DECRYPTED_OUTPUT -inkey keys/keypair.pem
