<!--

 \* @Author    : Primimy

 \* @Date     : 2020-05-07 23:11:41

 -->

# Windows Event Log TLS shows that _A fatal error occurred while creating a TLS client credential. The internal error state is 10013._

## Description

1. Windows Event Log TLS shows that ***A fatal error occurred while creating a TLS client credential. The internal error state is 10013.***

2. Failed to login in Github in Visual Studio with its extension, explorer shows that ***waiting for localhost***.

3. Failed to clone Github repository: ***Git failed with a fetal error***.

4. Failed to update/download extensions in marketplace with a error ***Could not create SSL/TLS secure channel*** or ***The underlying connection was closed: An unexpected error occurred on a send***.

## Reproduce

Use IIS Crypto to change default protocol (server, client) with ***Best Practice*** template and manually change it on TLS/SSL protocols.

## Fix

Use IIS Crypto to apply its best practice template.

Modify registry.(contrast newly installed Windows registry will be more accurate)

1. _[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL]_
   ​       delete every item in its sub keys.

2. _[HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\\.NETFramework\v4.0.30319]"SchUseStrongCrypto"=dword:00000001_

3. _[HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\\.NETFramework\v4.5.25000]"SchUseStrongCrypto"=dword:00000001_
4. _[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\\.NETFramework\v4.0.30319]"SchUseStrongCrypto"=dword:00000001_

<<<<<<< HEAD
Uncheck the box ___USE SSL 3.0___ in the Control Panel->Internet Explorer->Internet Control Panel->Advanced Page.

=======
>>>>>>> parent of 4ff47f3... Update 10013,HttpProtocol,.NetFramework.md
Reboot.

## Reason

Modification on registry of IIS Crypto will break default tendency protocol on Windows, when visit websites only supporting TLS 1.2 or above, will be failed to (***?***) handshake with the site.

## Reference

1. *https://www.smarterasp.net/support/kb/a1968/how-to-fix-error-underlying-connection-was-closed-an-unexpected-error-occurred-on.aspx*

2. *https://stackoverflow.com/questions/2859790/the-request-was-aborted-could-not-create-ssl-tls-secure-channel*

3. *https://developercommunity.visualstudio.com/content/problem/298616/failing-to-clone-github-repository-ssl-error.html*

4. *https://www.smarterasp.net/support/kb/a1968/how-to-fix-error-underlying-connection-was-closed-an-unexpected-error-occurred-on.aspx*

5. *https://support.microsoft.com/en-us/help/4458166/applications-that-rely-on-tls-1-2-strong-encryption-experience-connect*

6. *https://www.microsoft.com/en-us/download/details.aspx?id=55266*

7. *https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2003/cc776467(v=ws.10)?redirectedfrom=MSDN*