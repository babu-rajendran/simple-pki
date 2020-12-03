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


### References:
https://pki-tutorial.readthedocs.io/en/latest/simple/
