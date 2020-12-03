# Building a simple PKI infrastructure
We are assuming an organisation named Simple Inc, which has control over the domain simple.org. Let’s look at the steps involved in building the PKI infrastructure which includes Root CA, Signing CA and TLS certificate.

Clone the Simple PKI example files and change directory:

```
git clone https://bitbucket.org/stefanholek/pki-example-1
cd pki-example-1
```
<img width="888" alt="image7" src="https://user-images.githubusercontent.com/6368257/101059490-561c1b00-35b4-11eb-8aab-352f0a0444d3.png">

#### Create Root CA:

Create the directories to hold the CA resources, CRLs and certificates:

```
mkdir -p ca/root-ca/private ca/root-ca/db crl certs
chmod 700 ca/root-ca/private
```

Create the database:

```
cp /dev/null ca/root-ca/db/root-ca.db
cp /dev/null ca/root-ca/db/root-ca.db.attr
echo 01 > ca/root-ca/db/root-ca.crt.srl
echo 01 > ca/root-ca/db/root-ca.crl.srl
```

After this the directory structure should be as given in the screenshot below:

<img width="891" alt="image6" src="https://user-images.githubusercontent.com/6368257/101060131-0e49c380-35b5-11eb-9e16-5d05b4079989.png">

Create the root CA request:

Use the “openssl req -new” command as given below to create a private key and a certificate signing request for the root CA.

```
openssl req -new \
    -config etc/root-ca.conf \
    -out ca/root-ca.csr \
    -keyout ca/root-ca/private/root-ca.key
```

<img width="889" alt="image15" src="https://user-images.githubusercontent.com/6368257/101060561-8dd79280-35b5-11eb-9b6b-f101911e3a5b.png">

Create the root CA certificate:

Next we will use the “openssl ca” command to issue a self-signed root CA certificate based on the certificate signing request(CSR) created in the previous step. Once the command given below is executed, there will be a prompt for passphrase for the private key of the root CA. After entering the passphrase, the certificate details will be displayed and it can then be signed.

```
openssl ca -selfsign \
    -config etc/root-ca.conf \
    -in ca/root-ca.csr \
    -out ca/root-ca.crt \
    -extensions root_ca_ext
```

<img width="891" alt="image10" src="https://user-images.githubusercontent.com/6368257/101060985-04749000-35b6-11eb-9d20-7d1a339320e2.png">
<img width="891" alt="image8" src="https://user-images.githubusercontent.com/6368257/101061141-2c63f380-35b6-11eb-8f04-27e226d585dd.png">

#### Create Signing CA:

Create the directories to hold the signing CA resources:
```
mkdir -p ca/signing-ca/private ca/signing-ca/db
chmod 700 ca/signing-ca/private
```

Create the database for signing CA:
```
cp /dev/null ca/signing-ca/db/signing-ca.db
cp /dev/null ca/signing-ca/db/signing-ca.db.attr
echo 01 > ca/signing-ca/db/signing-ca.crt.srl
echo 01 > ca/signing-ca/db/signing-ca.crl.srl
```

<img width="947" alt="image4" src="https://user-images.githubusercontent.com/6368257/101061662-ba3fde80-35b6-11eb-8f4e-1b619e070450.png">
<img width="130" alt="image20" src="https://user-images.githubusercontent.com/6368257/101061750-d479bc80-35b6-11eb-9a7b-7d581779f737.png">


### References:
https://pki-tutorial.readthedocs.io/en/latest/simple/
