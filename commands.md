1. run `./easyrsa init-pki`    
2. then `./easyrsa build-ca` provide passphrase = abcd123 and common name = cb-viride-acme.default.svc    
3. ./easyrsa --subject-alt-name=DNS:*.cb-viride-acme.example.com build-server-full couchbase-server nopass   

4. rename certificate present in pki/issued folder to chain.pem and couchbase key in pki/private to pkey.key   
go to pki/private folder
4. openssl rsa -in pkey.key -out pkey.key.der -outform DER    
5. openssl rsa -in pkey.key.der -inform DER -out pkey.key -outform PEM    

6. cd ..    
7. kubectl create secret generic couchbase-server-tls --from-file issued/chain.pem  --from-file private/pkey.key   
8. kubectl create secret generic couchbase-operator-tls --from-file ca.crt   

