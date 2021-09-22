# GCDSExampleWebApp
This example closely aligns with this [document](https://docs.microsoft.com/en-us/azure/active-directory/develop/tutorial-v2-asp-webapp)


<br/> 

## Summary
- Install the Nuget Packages
 - 	Microsoft.Owin.Security.OpenIdConnect
 - 	Microsoft.Owin.Security.Cookies
 - 	Microsoft.Owin.Host.SystemWeb

<br/>

- Add Startup.cs

<br/>

- Add code to Startup.cs class 
  - Step 1 and 2 [here](https://docs.microsoft.com/en-us/azure/active-directory/develop/tutorial-v2-asp-webapp#configure-the-authentication-pipeline)

TODO: ValidateIssuer = False

- Add the following to the login/logout controller
  - [Follow documentation](https://docs.microsoft.com/en-us/azure/active-directory/develop/tutorial-v2-asp-webapp#add-a-controller-to-handle-sign-in-and-sign-out-requests)




Under configuration\appsettings in the web.config add the following:
```
	<add key="ClientId" value="spectre-localhost-5001" />
	<add key="redirectUri" value="https://localhost:5001/authentication/login-callback" />
	<add key="Tenant" value="oidc" />
	<add key="Authority" value="https://federation.dev.cce.af.mil/{0}/spectre-localhost-5001" />
  ```

> **NOTE** We will add these to key vault later


### Using another Port (Optional)

- Change the port to 5001 under Right click the **project** -> **Properties** -> **Web** 
 - 	**Save** and **Accept** to create virtual directory
 <br/><br/>
 
IIS http ports are only configured for 44300 and 44399 and using the IIS Express self-signed certificate. Here is the [documentation](https://docs.microsoft.com/en-us/iis/extensions/using-iis-express/handling-url-binding-failures-in-iis-express#using-a-custom-ssl-port) for more details.

Command to show the certs: 
```
netsh http show sslcert

```

<br/> 
-Look for the port 44300 and copy the cert hash and appid <br/> 
-Replace the following with the values:

```
IP:port                      : 0.0.0.0:44300
    Certificate Hash             : {cert hash}
    Application ID               : {appid}
    
    
```

```
netsh http add sslcert ipport=0.0.0.0:5001 certhash={certhash} appid={appid}

```
