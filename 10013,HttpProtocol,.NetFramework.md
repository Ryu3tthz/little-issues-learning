<!--
 * @Author       : Primimy
 * @Date         : 2020-05-07 23:11:41
 -->
# Windows Event Log TLS shows that _A fatal error occurred while creating a TLS client credential. The internal error state is 10013._
## Description
1. Windows Event Log TLS shows that _A fatal error occurred while creating a TLS client credential. The internal error state is 10013_.
2. Failed to login in Github in Visual Studio with its extension, explorer shows that _waiting for localhost_.
3. Failed to clone Github repository: _Git failed with a fetal error_.
4. Failed to update/download extensions in marketplace with a error _Could not create SSL/TLS secure channel_ or _The underlying connection was closed: An unexpected error occurred on a send_.
## Reproduce
Use IIS Crypto to change default protool(server, client)with ___Best Prctice___ template and manually change it on TLS/SSL protocols.
## Fix
Use IIS Crypto to apply its best practice template.
Modify registry.(constrst newly installed Windows registry will be more accurate)
1. _[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL]_
  Delete every item in its sub keys.
2. _[HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\.NETFramework\v4.0.30319]"SchUseStrongCrypto"=dword:00000001_
3. _[HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\.NETFramework\v4.5.25000]"SchUseStrongCrypto"=dword:00000001_
4._[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v4.0.30319]_"SchUseStrongCrypto"=dword:00000001_
5. Reboot.
## Reason
Modification on registry of IIS Crypto will break default tendency protocol on Windows, when visit websites only supporting TLS 1.2 or above, will be failed to (*?*)handshake with the site.
## Reference
1. _https://www.smarterasp.net/support/kb/a1968/how-to-fix-error-underlying-connection-was-closed-an-unexpected-error-occurred-on.aspx_
2. _https://stackoverflow.com/questions/2859790/the-request-was-aborted-could-not-create-ssl-tls-secure-channel_
3. _https://developercommunity.visualstudio.com/content/problem/298616/failing-to-clone-github-repository-ssl-error.html_
4. _https://www.smarterasp.net/support/kb/a1968/how-to-fix-error-underlying-connection-was-closed-an-unexpected-error-occurred-on.aspx_
5. _https://support.microsoft.com/en-us/help/4458166/applications-that-rely-on-tls-1-2-strong-encryption-experience-connect_
6. _https://www.microsoft.com/en-us/download/details.aspx?id=55266_
7. _https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2003/cc776467(v=ws.10)?redirectedfrom=MSDN_
