
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

