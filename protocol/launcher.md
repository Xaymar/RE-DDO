# Launcher Protocol
- The launcher was built with minimal debug information, though no PDB is present.
    - There are still direct string references to what functions are actually called.
	- Much of the information the launcher gathers dynamically is embedded into the launcher itself.
	- Necessary protocol information that would be hidden by HTTPS is visible in plain text while debugging or decompiling.
	- It uses Qt Framework.
- Communication for information is entirely HTTP/S, rather unique for an early MMO.
    - Protocol is entirely SOAP based, and will just redirect you to a different page if you don't speak SOAP.
- Patching is using a binary protocol.
- It appears to be 32-bit?

## Worlds, Authentication
### 1. Retrieve launcher configuration
<details><summary>Query</summary>
```
GET /launcher/ddo/dndlauncher.server.config.xml HTTP/1.1
Connection: Keep-Alive
Accept-Encoding: gzip
Accept-Language: en-US,*
User-Agent: Mozilla/5.0
Host: gls.ddo.com
```
</details>

Reply is UTF-8 with BOM. I stripped away some empty lines.

<details><summary>Response</summary>

```
HTTP/1.1 200 OK
Content-Type: text/xml
Content-Encoding: gzip
Last-Modified: Wed, 08 May 2024 19:48:05 GMT
Accept-Ranges: bytes
ETag: "808895a480a1da1:0"
Vary: Accept-Encoding
Server: Microsoft-IIS/8.5
X-Powered-By: ASP.NET
Date: Sun, 02 Jun 2024 00:05:45 GMT
Content-Length: 2285

ï»¿<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <appSettings>
    <add key="LauncherConfig.DateTime" value="10/20/10 6:40 AM"/>
    <add key="LauncherConfig.RefreshFrequency" value="15"/> <!-- minutes -->
    <add key="GameName" value="DDO"/>
    <add key="Patching.ProductCode" value="DDO"/>
    <!-- CLIENT LAUNCHING -->
    <add key="GameClient.WIN32.Filename" value="dndclient.exe"/>
	<add key="GameClient.WIN64.Filename" value="dndclient64.exe" />
    <add key="GameClient.WIN32.ArgTemplate" value="-a {SUBSCRIPTION} -h {LOGIN} --glsticketdirect {GLS} --chatserver {CHAT} --rodat on --language {LANG} --gametype DDO --authserverurl {AUTHSERVERURL} --glsticketlifetime {GLSTICKETLIFETIME}"/>
	<add key="GameClient.WIN32Legacy.Filename" value="dndclient_awesomium.exe" />
    <add key="EnableStayLoggedInFeature" value="False" />
    <add key="GameClient.OSX.Filename" value="dndclient.app"/>
    <add key="GameClient.OSX.ArgTemplate" value="-a {SUBSCRIPTION} -h {LOGIN} --glsticketdirect {GLS} --chatserver {CHAT} --rodat on --language {LANG} --gametype DDO --authserverurl {AUTHSERVERURL} --glsticketlifetime {GLSTICKETLIFETIME} --supporturl {SUPPORTURL} --bugurl {BUGURL} --supportserviceurl {SUPPORTSERVICEURL}"/>
    <add key="GameClient.Arg.crashreceiver" value="http://crash.ddo.com:8080/CrashReceiver-1.0"/>
    <add key="GameClient.Arg.authserverurl" value="https://gls.ddo.com/GLS.AuthServer/Service.asmx"/>
    <add key="GameClient.Arg.glsticketlifetime" value="21600"/>
    <!-- CLIENT LAUNCHING -->	
    <add key="GameClient.ResetGraphicsArg" value=" --safe"/>
    <add key="GameClient.AlwaysPatchHighRes" value="true"/>
    <!-- Standalone Updater -->
    <add key="GameClient.RequiredVersion" value="0"/>
    <add key="GameClient.ForwardVersion" value="0"/>
    <add key="URL.UpdateDownload" value="http://downloads.turbine.com" />
    <add key="Patch.UpdaterNameFormat" value="{0}updater_{1}_{2}.exe" />
    <add key="DataCenterBrowser.BatchWorldStatus" value="true"/>
    <add key="URL.Support" value="https://help.standingstonegames.com"/>
    <add key="URL.Home" value="http://www.ddo.com"/>
    <add key="URL.Community" value="https://forums.ddo.com/index.php"/>
    <add key="URL.Account" value="https://myaccount.standingstonegames.com/?billing[target_lang]={lang}"/>
    <add key="URL.NewAccount" value="https://signup.ddo.com/ddo.php"/>
    <add key="URL.ForgotPassword" value="https://myaccount.standingstonegames.com/?page_id=29&amp;billing[process]=13"/>
    <add key="URL.BannerSource.Steam" value="http://live.ddo.com/sites/ddolauncher/steam/{lang}/ddo_launcherad.png?x=0&amp;y=78" />
    <add key="URL.NewAccount.Steam" value="http://live.ddo.com/sites/launcher/ddo/redirects/NewAccountSteam.php?lang={lang}" />
	<add key="URL.PermaDeathServerInfo" value="https://www.ddo.com/news/ddo-hardcore-league"/>
    <add key="URL.Account.Post" value="https://myaccount.standingstonegames.com/?page_id=29&amp;billing[target_lang]={lang}"/>
    <add key="Format.Account.Login" value=""/>
    <add key="Format.Account.BuyNow" value="form_user_name={0}&amp;form_user_pass={1}&amp;siteuser[action]=login&amp;billing[process]=17&amp;billing[forms][subscriptionName]={2}&amp;billing[scenario]=DDO_BUY_NOW_POPUP&amp;billing[forms][productCode]=DDO&amp;billing[forms][purchaseProductCode]=DDOBuy&amp;billing[forms][purchasePlanCode]=DDO-F2PUp" />
    <add key="Activate.Account.BuyNow" value="false"/>
    <add key="Activate.Account.VIPDisplay" value="true"/>
    <add key="Threshold.Account.DaysLeft" value="15"/>
    <add key="Activate.Account.DaysLeft" value="true"/>
    <add key="LauncherConfig.SubscriptionRefreshFrequency" value="60"/>
    <add key="Subscription.FreeToPlay" value="true"/>
    <add key="URL.PrivacyPolicy" value="http://www.turbine.com/?page_id=59"/>
    <add key="URL.NewsFeed" value="https://forums-old.ddo.com/en/launcher-feed.xml"/>
    <add key="Launcher.NewsFeedCSSUrl" value="http://live.ddo.com/sites/launcher/ddo/newsfeed.css"/>
    <add key="URL.NewsStyleSheet" value="http://live.ddo.com/sites/launcher/ddo/newsstylesheet.xslt"/>
    <add key="URL.AlertsStyleSheet" value="http://live.ddo.com/sites/launcher/ddo/alertsstylesheet.xslt"/>
	<add key="URL.GameLaunchReportURL" value="https://webevents.daybreakgames.com/events"/>
    <add key="URL.NewsFeed.Timeout" value="10" />
    <add key="URL.LogoButton1" value="http://www.turbine.com"/>
    <add key="URL.LogoButton2" value="http://www.wizards.com"/>
    <add key="URL.LogoButton3" value="http://www.hasbro.com"/>
    <add key="URL.LogoButton4" value="http://www.atari.com"/>
    <add key="WorldUpdateRate" value="1"/>	            <!-- minutes -->
    <add key="PatchWindow" value="30"/>	                <!-- minutes -->
    <add key="PatchConnectRetryInterval" value="1"/>	<!-- minutes -->
    <add key="DisablePatch" value="false"/>
    <add key="EmailAddress.Errors" value="LauncherErrors@turbine.com"/>
    <add key="Eula.en.FilePath" value="en\DDO Eula.rtf"/>
    <add key="Legal.en.Titles" value="End User License Agreement|Terms of Service"/>
    <add key="Legal.DE.Titles" value="Endnutzer-Lizenzvereinbarung|Nutzungsbedingungen"/>
    <add key="Legal.FR.Titles" value="Contrat de License Utilisateur Final|Conditions de Service"/>
    <add key="Legal.English.Titles" value="End User License Agreement|Terms of Service"/>
    <add key="Legal.en-GB.Titles" value="End User License Agreement|Terms of Service"/>
    <add key="Legal.en.FilePaths" value="en\DDO EULA.rtf|en\DDO TOS.rtf"/>
    <add key="Legal.DE.FilePaths" value="DE\DDO EULA.rtf|DE\DDO TOS.rtf"/>
    <add key="Legal.FR.FilePaths" value="FR\DDO EULA.rtf|FR\DDO TOS.rtf"/>
    <add key="Legal.English.FilePaths" value="en\DDO EULA.rtf|en\DDO TOS.rtf"/>
    <add key="Legal.en-GB.FilePaths" value="en\DDO EULA.rtf|en\DDO TOS.rtf"/>
    <add key="URL.DownloadFilesList" value="http://akamai.ddo.com/ddo/patch/splashscreen/DownloadFilesList.xml"/>
    <add key="URL.ReqSoftwareInstall" value="http://akamai.ddo.com/ddo/PreReqProd/PreInstallListDDOProd.xml"/>
    <add key="URL.BannerSource" value="http://live.ddo.com/sites/ddolauncher/{lang}/ddo_launcherad.png?x=1&amp;y=77"/>
    <add key="URL.BannerTarget" value="http://live.ddo.com/sites/launcher/ddo/redirects/BannerTarget.php?lang={lang}"/> 
    <!-- Login Queue -->
    <add key="WorldQueue.LoginQueue.URL" value="https://gls.ddo.com/GLS.AuthServer/LoginQueue.aspx"/> 
    <add key="WorldQueue.TakeANumber.Parameters" value="command=TakeANumber&amp;subscription={0}&amp;ticket={1}&amp;ticket_type=GLS&amp;queue_url={2}"/>    
    <add key="WorldQueue.LeaveQueue.Parameters" value="command=LeaveQueue&amp;subscription={0}&amp;context={1}&amp;ticket_type=GLS&amp;queue_url={2}"/> 
    <add key="WorldQueue.Threshold.WaitTimeMultiplier" value="1.00" />
    <add key="WorldQueue.Threshold.Medium" value="300" />
    <add key="WorldQueue.Threshold.Long" value="900" />
    <add key="WorldQueue.PollTimer" value ="120" />	
    <!-- ENABLE TRANSFER -->
    <add key="ShardTransfer.Enabled" value="true" />
    <add key="ShardTransfer.ServiceURL" value="http://xfer.ddo.com/TurbineTransferService/TurbineTransferService.svc" />
    <add key="ShardTransfer.StoreURL" value="http://d12.parature.com/ics/support/kbanswer.asp?deptID=24047&amp;task=knowledge&amp;questionID=6781" />	
    <!-- END ENABLE TRANSFER -->
    <!-- Akamai Download Information -->		
    <add key="URL.AkamaiDownloadURL" value="http://installer.ddo.com/dnd/"/>
    <add key="Game.Version" value="5000.0050.3264.4021"/>
  </appSettings>
</configuration>
```
</details>

The launcher proceeds to individually download every file listed here, even if it already has them. It does so for every language, not just the language the user has selected.

### 2. Query "World" list (happens every 30s or so)
<details><summary>Query</summary>
	
```
POST /GLS.DataCenterServer/Service.asmx HTTP/1.1
POST: /Service.asmx
Host: gls.ddo.com
User-Agent: User Agent
Content-Type: text/xml; charset=utf-8
SOAPAction: "http://www.turbine.com/SE/GLS/GetDatacenters"
Content-Length: 313
Connenction: Keep-Alive
Accept-Encoding: gzip
Accept-Language: en-US, *

<soap:Envelope
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xmlns:xsd="http://www.w3.org/2001/XMLSchema"
	xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
	<soap:Body>
		<GetDatacenters
			xmlns="http://www.turbine.com/SE/GLS">
			<game>
		</GetDatacenters>
	</soap:Body>
</soap:Envelope>
```
</details>

<details><summary>Response</summary>
	
```
HTTP/1.1 200 OK
Cache-Control: private, max-age=0
Content-Type: text/xml; charset=utf-8
Server: Microsoft-IIS/8.5
X-AspNet-Version: 2.0.50727
X-Powered-By: ASP.NET
Date: Sun, 02 Jun 2024 00:05:45 GMT
Content-Length: 3304

<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema">
	<soap:Body>
		<GetDatacentersResponse xmlns="http://www.turbine.com/SE/GLS">
			<GetDatacentersResult>
				<Datacenter>
					<Name>DDO</Name>
					<Worlds>
						<World>
							<Name>Ghallanda</Name>
							<LoginServerUrl>(invalid service specified)</LoginServerUrl>
							<ChatServerUrl>198.252.160.42:2900</ChatServerUrl>
							<StatusServerUrl>http://gls.ddo.com/GLS.DataCenterServer/StatusServer.aspx?s=10.192.145.23</StatusServerUrl>
							<Order>0</Order>
							<Language>EN</Language>
						</World>
						<World>
							<Name>Argonnessen</Name>
							<LoginServerUrl>(invalid service specified)</LoginServerUrl>
							<ChatServerUrl>198.252.160.161:2900</ChatServerUrl>
							<StatusServerUrl>http://gls.ddo.com/GLS.DataCenterServer/StatusServer.aspx?s=10.192.145.11</StatusServerUrl>
							<Order>1</Order>
							<Language>EN</Language>
						</World>
						<World>
							<Name>Cannith</Name>
							<LoginServerUrl>(invalid service specified)</LoginServerUrl>
							<ChatServerUrl>198.252.160.41:2900</ChatServerUrl>
							<StatusServerUrl>http://gls.ddo.com/GLS.DataCenterServer/StatusServer.aspx?s=10.192.145.17</StatusServerUrl>
							<Order>2</Order>
							<Language>EN</Language>
						</World>
						<World>
							<Name>Hardcore</Name>
							<LoginServerUrl>(invalid service specified)</LoginServerUrl>
							<ChatServerUrl>198.252.160.153:2900</ChatServerUrl>
							<StatusServerUrl>http://gls.ddo.com/GLS.DataCenterServer/StatusServer.aspx?s=10.192.145.80</StatusServerUrl>
							<Order>3</Order>
							<Language />
						</World>
						<World>
							<Name>Khyber</Name>
							<LoginServerUrl>(invalid service specified)</LoginServerUrl>
							<ChatServerUrl>198.252.160.43:2900</ChatServerUrl>
							<StatusServerUrl>http://gls.ddo.com/GLS.DataCenterServer/StatusServer.aspx?s=10.192.145.29</StatusServerUrl>
							<Order>4</Order>
							<Language>EN</Language>
						</World>
						<World>
							<Name>Orien</Name>
							<LoginServerUrl>(invalid service specified)</LoginServerUrl>
							<ChatServerUrl>198.252.160.44:2900</ChatServerUrl>
							<StatusServerUrl>http://gls.ddo.com/GLS.DataCenterServer/StatusServer.aspx?s=10.192.145.35</StatusServerUrl>
							<Order>5</Order>
							<Language>EN</Language>
						</World>
						<World>
							<Name>Sarlona</Name>
							<LoginServerUrl>(invalid service specified)</LoginServerUrl>
							<ChatServerUrl>198.252.160.45:2900</ChatServerUrl>
							<StatusServerUrl>http://gls.ddo.com/GLS.DataCenterServer/StatusServer.aspx?s=10.192.145.41</StatusServerUrl>
							<Order>6</Order>
							<Language>EN</Language>
						</World>
						<World>
							<Name>Thelanis</Name>
							<LoginServerUrl>(invalid service specified)</LoginServerUrl>
							<ChatServerUrl>198.252.160.46:2900</ChatServerUrl>
							<StatusServerUrl>http://gls.ddo.com/GLS.DataCenterServer/StatusServer.aspx?s=10.192.145.47</StatusServerUrl>
							<Order>7</Order>
							<Language>EN</Language>
						</World>
						<World>
							<Name>Wayfinder</Name>
							<LoginServerUrl>(invalid service specified)</LoginServerUrl>
							<ChatServerUrl>198.252.160.47:2900</ChatServerUrl>
							<StatusServerUrl>http://gls.ddo.com/GLS.DataCenterServer/StatusServer.aspx?s=10.192.145.53</StatusServerUrl>
							<Order>8</Order>
							<Language>DE</Language>
						</World>
					</Worlds>
					<AuthServer>https://gls-auth.ddo.com/GLS.AuthServer/Service.asmx</AuthServer>
					<PatchServer>patch.ddo.com:5015</PatchServer>
					<LauncherConfigurationServer>http://gls.ddo.com/launcher/ddo/dndlauncher.server.config.xml</LauncherConfigurationServer>
				</Datacenter>
			</GetDatacentersResult>
		</GetDatacentersResponse>
	</soap:Body>
</soap:Envelope>
```
</details>

We can retrieve the real Login Server using the provided status URL. Legacy Code Alert!

### 3. Login
When the user provides Username and Password, the Launcher proceeds to communicate with a HTTPS/TLS1.2 server that provides a weak encryption key. I had to intentionally make libcurl unsafe with `--ciphers DEFAULT@SECLEVEL=1`, and was able to proceed further.

<details><summary>Query</summary>
	
```
POST /GLS.AuthServer/Service.asmx HTTP/1.1
Host: gls-auth.ddo.com
Accept: */*
Content-Length: {VARIES}
Post: /Service.asmx
User-Agent: User Agent
Content-Type: text/xml; charset=utf-8

<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xmlns:xsd="http://www.w3.org/2001/XMLSchema"
	xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
	<soap:Body>
		<LoginAccount xmlns="http://www.turbine.com/SE/GLS">
			<username>ENCODED_USERNAME</username>
			<password>ENCODED_PASSWORD</password>
			<additionalInfo>
</additionalInfo>
		</LoginAccount>
	</soap:Body>
</soap:Envelope>
```
</details>

#### 3.1 Failed Authentication
<details><summary>Response</summary>
	
```
<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema">
	<soap:Body>
		<soap:Fault>
			<faultcode>BIS</faultcode>
			<faultstring>No Subscriber Formal Entity was found.</faultstring>
			<faultactor>BIS</faultactor>
			<detail>
				<result>0x8004C002</result>
			</detail>
		</soap:Fault>
	</soap:Body>
</soap:Envelope>
```
</details>

#### 3.2 Successful Authentication
<details><summary>Response</summary>
	
```
HTTP/1.1 200 OK
Cache-Control: private, max-age=0
Content-Type: text/xml; charset=utf-8
Server: Microsoft-IIS/8.5
X-AspNet-Version: 2.0.50727
X-Powered-By: ASP.NET
Date: Sun, 02 Jun 2024 01:52:49 GMT
Content-Length: 6852

<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema">
	<soap:Body>
		<LoginAccountResponse xmlns="http://www.turbine.com/SE/GLS">
			<LoginAccountResult>
				<Subscriptions>
					<GameSubscription>
						<Game>DDO</Game>
						<Name>{SUBSCRIPTION}</Name>
						<Description>... stripped private information ...</Description>
						<ProductTokens>
							... stripped private information ...
						</ProductTokens>
						<CustomerServiceTokens />
						<Status>... stripped private information ...</Status>
						<BillingSystemTime>... stripped private information ...</BillingSystemTime>
						<AdditionalInfo />
					</GameSubscription>
					<GameSubscription>
						<Game>Web_DDO</Game>
						<Name>... stripped private information ...</Name>
						<Description>... stripped private information ...</Description>
						<ProductTokens>
							<string>BASE</string>
						</ProductTokens>
						<CustomerServiceTokens />
						<Status>... stripped private information ...</Status>
						<BillingSystemTime>... stripped private information ...</BillingSystemTime>
						<AdditionalInfo />
					</GameSubscription>
				</Subscriptions>
				<Ticket>{GLS}</Ticket>
			</LoginAccountResult>
		</LoginAccountResponse>
	</soap:Body>
</soap:Envelope>
```
</details>

### 4. Status Query
The launcher now queries the status URL to find the actual URLs for queueing and connecting.

### 5. Queueing
Before we can actually launch the client, we're forced to sit in queue. This is different from games like World of Warcraft, where you sit in queue while the game is open, wasting massive amounts of electricity and blocking you from doing other tasks. I'm not sure how this is done, as the provided queueurls are in private addressing space.

### 6. Actually launching the game.
We should now have everything needed to launch the game:

```
dndclient -a ${SUBSCRIPTION} -h ${LOGINURL} --glsticketdirect ${GLS} --chatserver ${CHATURL} --rodat on --language English --gametype DDO --authserverurl ${AUTHURL} --glsticketlifetime 21600
```

## Other Data
### Old Forums
When launched, and every few minutes afterwards, the launcher communicates with forums-old.ddo.com. This is done entirely in HTTPS and ignores SSLKEYLOGFILE.


## Patching
### Part 1
The launcher makes an invalid query that should return a 5xx or 4xx code, but the Server responds fine. More legacy code where the solution was "fix it or you're fired" to the wrong team.

<details><summary>Query</summary>
	
```
POST /stateless2 HTTP/1.1
Host: patch.ddo.com:5015
Accept: */*
Content-Length: 233
Content-Type: application/x-www-form-urlencoded

0000   50 4f 53 54 20 2f 73 74 61 74 65 6c 65 73 73 32
0010   20 48 54 54 50 2f 31 2e 31 0d 0a 48 6f 73 74 3a
0020   20 70 61 74 63 68 2e 64 64 6f 2e 63 6f 6d 3a 35
0030   30 31 35 0d 0a 41 63 63 65 70 74 3a 20 2a 2f 2a
0040   0d 0a 43 6f 6e 74 65 6e 74 2d 4c 65 6e 67 74 68
0050   3a 20 32 33 33 0d 0a 43 6f 6e 74 65 6e 74 2d 54
0060   79 70 65 3a 20 61 70 70 6c 69 63 61 74 69 6f 6e
0070   2f 78 2d 77 77 77 2d 66 6f 72 6d 2d 75 72 6c 65
0080   6e 63 6f 64 65 64 0d 0a 0d 0a
```
</details>

We get a reply that I have not decoded yet. 
<details><summary>Response</summary>
	
```
HTTP/1.1 200 
Cache-Control: no-cache
Content-Type: binary
Server: Microsoft-HTTPAPI/2.0
Date: Sun, 02 Jun 2024 00:59:04 GMT
Content-Length: 128

0000   2a 58 ca 2c 92 38 e7 f4 97 c3 18 b1 33 4a 33 9c
0010   bf 28 0f 6f 94 8f 53 d8 9f c6 5e 1e 84 6d 35 b2
0020   df f1 22 0e c9 ca a9 b4 c0 37 e3 89 d7 76 93 16
0030   1e c6 0a 65 c9 35 6c b5 73 0d c8 c6 2a cd 6a 4f
0040   01 5d ce 19 08 7e 1b 1c 11 4e 4d fb 74 c8 73 2f
0050   c8 85 69 7c d8 51 54 d5 1b fc 6a c6 87 fd 6f 3f
0060   e1 16 70 43 f5 2d 21 e1 25 74 07 69 ba 81 76 99
0070   9f 47 c9 0b 8e 7b 5e 5f 45 ec 3f 1d 6e 61 97 22
```
</details>

### Part 2 (and repeating for a few files)
Because the first time wasn't bad enough, let's do it a 2nd time.
<details><summary>Query</summary>
	
```
POST /stateless2 HTTP/1.1
Host: patch.ddo.com:5015
Accept: */*
Content-Length: 385
Content-Type: application/x-www-form-urlencoded

0000   6d 01 00 80 04 33 64 65 73 80 00 00 00 8c 30 7e
0010   f4 01 97 b1 c1 8a d0 96 75 08 11 67 3a c2 d5 fb
0020   7e 7d 67 ba b1 c6 ff 74 26 b4 ff dc 44 39 d4 48
0030   d9 21 5d e8 fe 28 14 13 a3 2f 19 5c 9f dd fe 59
0040   cd fd 48 68 84 e0 d9 f9 b4 68 d6 75 17 a4 eb c7
0050   b7 fb 9c 4d 7b b6 a1 b4 b6 c9 11 26 b1 76 45 98
0060   c2 10 a4 e8 c8 69 1f 2b 94 bd 3e f2 9e 02 ed 24
0070   1d 11 8a 39 59 58 3a a1 10 86 3e 8e 80 a2 6d a5
0080   d9 84 49 92 eb 2f e9 43 8d be 59 ae a0 18 00 00
0090   00 d8 00 00 00 80 ba f5 67 34 4b 57 d3 ba 3f ee
00a0   42 2a 2b ed 47 12 98 89 ad b5 0b df 2c 68 ca 6d
00b0   74 01 91 4a 04 da d9 af 64 7a 5c da 94 b6 4d 0a
00c0   ca 45 eb 9c 2e 76 3b 8d d2 45 16 1f 08 11 31 f9
00d0   fb 2d 05 5d fd 9c 83 1a f6 9b 9a 28 46 c1 8a ab
00e0   05 eb 89 29 64 f9 33 68 97 6a 5f 95 19 27 e4 20
00f0   6f 20 57 10 26 f1 fd 9f 3a ba f0 3d 76 37 81 bd
0100   77 7e d3 dd fa 77 32 8e 0f 5d a1 c9 78 55 ef e4
0110   87 dc 47 44 ac 51 0e d9 bf 88 aa c7 18 e5 c2 fb
0120   5e f7 e0 9a 0b 43 eb 2b 2b 38 37 5b ad f3 61 86
0130   fc e8 24 f6 af ea 7c 6b 39 48 26 13 25 db fa 81
0140   89 32 05 b6 fa 2c 72 45 ae 5b 14 d1 8a eb ae 23
0150   f5 54 f7 29 1e 30 b5 2c e2 33 d9 a3 3e cc 88 84
0160   d3 26 32 cb fd 79 57 90 f3 7b cb 1d 9a 02 00 00
0170   00 a5 d2 7c 01 01 00 00 00 65 72 6f 43 02 00 00
0180   00
```
</details>

The response is 70KB, so I'll only include the header
<details><summary>Response</summary>
	
```
HTTP/1.1 200
Cachte-Control: no-cache
Content-Type: binary
Server: Microsoft-HTTPAPI/2.0
Date: Sun, 02 Jun 2024 00:59:04 GMT
Content-Length: 74024

(binary data)
```
</details>

This happens multiple times.

