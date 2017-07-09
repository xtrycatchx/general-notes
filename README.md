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
