# destroy
```
npm ls -gp --depth=0 | awk -F/ '/node_modules/ && !/\/npm$/ {print $NF}' | xargs npm -g rm
```

# when your openssl base64 sucks
```
node -e "process.stdout.write(new Buffer(process.argv[1]).toString('base64'))" "batman1234"
```
```bash
node -e "process.stdout.write(Buffer.from(process.argv[1], 'base64').toString('utf8'))" "YmF0bWFuMTIzNA=="
```
# quick check if base64 string
```
const isBase64 = payload => (Buffer.from(Buffer.from(payload, 'base64').toString()).toString('base64') == payload)
```

# generate keys
```
openssl req -newkey rsa:2048 -nodes -keyout key.pem -x509 -days 365 -out certificate.pem
```

# quick bash with docker
```
docker run -it ubuntu:16.04 /bin/bash
```

# jenkins pipeline
To allowing Java packages in pipeline scripts : 
```
import java.text.SimpleDateFormat

node {
    def dateFormat = new SimpleDateFormat("yyyyMMddHHmm")
    println(new Date())
}
```
Just approve the package via `YOUR_JENKINS_URL/scriptApproval`

# npm
Error : 
```
npm ERR! shasum check failed for ...\aws-sdk-2.82.0.tgz
npm ERR! Expected: a94cfe90c15ee0e403f00f0665dccb98aa93e1f8
npm ERR! Actual:   389d0fbf87429007d3bd3e0293d883fcca84b529
npm ERR! From:     http://xxxxx/aws-sdk-2.82.0.tgz
```
Try :
``
npm cache clean
``
# ios
Error when app unable to load local src from WebView, try this Info.plist:
```
 <dict>
    <key>NSExceptionDomains</key>
    <dict>
      <key>localhost</key>
			<dict>
				<key>NSExceptionAllowsInsecureHTTPLoads</key>
				<true/>
			</dict>
			<key>NSAllowsArbitraryLoads</key>
			<true/>
			<key>NSAllowsArbitraryLoadsInWebContent</key>
			<true/>
			<key>NSAllowsLocalNetworking</key>
			<true/>
		</dict>
	</dict>
```

# open ssl common
Create a private key
```
openssl genrsa -out server.key 4096
```

Generate a new private key and certificate signing request
```
openssl req -out server.csr -new -newkey rsa:4096 -nodes -keyout server.key
```

Generate a self-signed certificate
```
openssl req -x509 -sha256 -nodes -days 365 -newkey rsa:4096 -keyout server.key -out server.crt
```

Generate a certificate signing request (CSR) for an existing private key
```
openssl req -out server.csr -key server.key -new
```
Sign a CSR
```
openssl x509 -req -days 360 -in verifier.csr -CA rootCA.pem -CAkey rootCA.key -CAcreateserial -out verifier.pem
```

Generate a certificate signing request based on an existing certificate
```
openssl x509 -x509toreq -in server.crt -out server.csr -signkey server.key
```

Remove a passphrase from a private key
```
openssl rsa -in server.pem -out newserver.pem
```

Parse a list of revoked serial numbers
```
openssl crl -inform DER -text -noout -in list.crl
```

Check a certificate signing request (CSR)

```
openssl req -text -noout -verify -in server.csr
```

Check a private key

```
openssl rsa -in server.key -check
```

Check a public key

```
openssl rsa -inform PEM -pubin -in pub.key -text -noout
openssl pkey -inform PEM -pubin -in pub.key -text -noout
```
Check a certificate

```
openssl x509 -in server.crt -text -noout
openssl x509 -in server.cer -text -noout
```
Check a PKCS#12 file (.pfx or .p12)
```
openssl pkcs12 -info -in server.p12
```
Verify a private key matches an certificate

```

openssl x509 -noout -modulus -in server.crt | openssl md5
openssl rsa -noout -modulus -in server.key | openssl md5
openssl req -noout -modulus -in server.csr | openssl md5
```

Display all certificates including intermediates

```
openssl s_client -connect www.google.com:443
```

Convert a DER file (.crt .cer .der) to PEM
```
openssl x509 -inform der -in server.cer -out server.pem
```

Convert a PEM file to DER
```

openssl x509 -outform der -in server.pem -out server.der
```

Convert a PKCS#12 file (.pfx .p12) containing a private key and certificates to PEM
```
openssl pkcs12 -in server.pfx -out server.pem -nodes
```

Convert a PEM certificate file and a private key to PKCS#12 (.pfx .p12)
```
openssl pkcs12 -export -out server.pfx -inkey server.key -in server.crt -certfile CACert.crt
```

Check URL cert
```
echo | openssl s_client -showcerts -servername gnupg.org -connect bass.bnshosting.net:443 2>/dev/null | openssl x509 -inform pem -noout -text
```

# when you forget wifi password in Mac
```
security find-generic-password -ga "MY_ROUTER" | grep "password:"
```
