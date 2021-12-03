C:\WINDOWS\system32>rclone config
2021/11/19 21:56:53 NOTICE: Config file "C:\\Users\\26575\\.config\\rclone\\rclone.conf" not found - using defaults
No remotes found - make a new one
n) New remote
s) Set configuration password
q) Quit config
n/s/q> n
name> 23
Type of storage to configure.
Enter a string value. Press Enter for the default ("").
Choose a number from below, or type in your own value
 1 / 1Fichier
   \ "fichier"
 2 / Alias for an existing remote
   \ "alias"
 3 / Amazon Drive
   \ "amazon cloud drive"
 4 / Amazon S3 Compliant Storage Provider (AWS, Alibaba, Ceph, Digital Ocean, Dreamhost, IBM COS, Minio, etc)
   \ "s3"
 5 / Backblaze B2
   \ "b2"
 6 / Box
   \ "box"
 7 / Cache a remote
   \ "cache"
 8 / Citrix Sharefile
   \ "sharefile"
 9 / Dropbox
   \ "dropbox"
10 / Encrypt/Decrypt a remote
   \ "crypt"
11 / FTP Connection
   \ "ftp"
12 / Google Cloud Storage (this is not Google Drive)
   \ "google cloud storage"
13 / Google Drive
   \ "drive"
14 / Google Photos
   \ "google photos"
15 / Hubic
   \ "hubic"
16 / In memory object storage system.
   \ "memory"
17 / Jottacloud
   \ "jottacloud"
18 / Koofr
   \ "koofr"
19 / Local Disk
   \ "local"
20 / Mail.ru Cloud
   \ "mailru"
21 / Mega
   \ "mega"
22 / Microsoft Azure Blob Storage
   \ "azureblob"
23 / Microsoft OneDrive
   \ "onedrive"
24 / OpenDrive
   \ "opendrive"
25 / OpenStack Swift (Rackspace Cloud Files, Memset Memstore, OVH)
   \ "swift"
26 / Pcloud
   \ "pcloud"
27 / Put.io
   \ "putio"
28 / QingCloud Object Storage
   \ "qingstor"
29 / SSH/SFTP Connection
   \ "sftp"
30 / Sugarsync
   \ "sugarsync"
31 / Tardigrade Decentralized Cloud Storage
   \ "tardigrade"
32 / Transparently chunk/split large files
   \ "chunker"
33 / Union merges the contents of several upstream fs
   \ "union"
34 / Webdav
   \ "webdav"
35 / Yandex Disk
   \ "yandex"
36 / http Connection
   \ "http"
37 / premiumize.me
   \ "premiumizeme"
38 / seafile
   \ "seafile"
Storage> 23
** See help for onedrive backend at: https://rclone.org/onedrive/ **

Microsoft App Client Id
Leave blank normally.
Enter a string value. Press Enter for the default ("").
client_id>
Microsoft App Client Secret
Leave blank normally.
Enter a string value. Press Enter for the default ("").
client_secret>
Edit advanced config? (y/n)
y) Yes
n) No (default)
y/n> n
Remote config
Use auto config?
 * Say Y if not sure
 * Say N if you are working on a remote or headless machine
y) Yes (default)
n) No
y/n> y
If your browser doesn't open automatically go to the following link: http://127.0.0.1:53682/auth?state=iaYCafBVN84Bas67PxqO9w
Log in and authorize rclone for access
Waiting for code...
Got code
Choose a number from below, or type in an existing value
 1 / OneDrive Personal or Business
   \ "onedrive"
 2 / Root Sharepoint site
   \ "sharepoint"
 3 / Type in driveID
   \ "driveid"
 4 / Type in SiteID
   \ "siteid"
 5 / Search a Sharepoint site
   \ "search"
Your choice> 1
Found 1 drives, please select the one you want to use:
0: OneDrive (business) id=b!OZedneScrUmdYF2xuvCoenl8mMSrvBxHvHm_hDeEqhnom7xn7SWjSZWYTqrw2N4T
Chose drive to use:> 0
Found drive 'root' of type 'business', URL: https://mrwangwys-my.sharepoint.com/personal/mwang_mrwangwys_onmicrosoft_com/Documents
Is that okay?
y) Yes (default)
n) No
y/n> y
--------------------
[23]
type = onedrive
token = {"access_token":"eyJ0eXAiOiJKV1QiLCJub25jZSI6Im5nZFRfeFRNZWNFVkIxQ0hueFAySDlHMkQtejRYSi02RGlrU0E3elpTc1kiLCJhbGciOiJSUzI1NiIsIng1dCI6Imwzc1EtNTBjQ0g0eEJWWkxIVEd3blNSNzY4MCIsImtpZCI6Imwzc1EtNTBjQ0g0eEJWWkxIVEd3blNSNzY4MCJ9.eyJhdWQiOiIwMDAwMDAwMy0wMDAwLTAwMDAtYzAwMC0wMDAwMDAwMDAwMDAiLCJpc3MiOiJodHRwczovL3N0cy53aW5kb3dzLm5ldC8xMWUyMjBjYy0yMmYzLTQxZTctODgyZC0wZjg3Yjk3NTg3NjYvIiwiaWF0IjoxNjM3MzI5OTQwLCJuYmYiOjE2MzczMjk5NDAsImV4cCI6MTYzNzMzNDg2NywiYWNjdCI6MCwiYWNyIjoiMSIsImFpbyI6IkFTUUEyLzhUQUFBQVBXWEN6TkRHTkhkSzhEblRLQWpRaG9qWmhtM1NsYVN4dFZGRXlXTW0vbWs9IiwiYW1yIjpbInB3ZCIsInJzYSJdLCJhcHBfZGlzcGxheW5hbWUiOiJyY2xvbmUiLCJhcHBpZCI6ImIxNTY2NWQ5LWVkYTYtNDA5Mi04NTM5LTBlZWMzNzZhZmQ1OSIsImFwcGlkYWNyIjoiMSIsImRldmljZWlkIjoiYTVjMGU4MzYtMzRkOC00NTdhLWJmY2YtYTBiNDgzY2FmYTE4IiwiZmFtaWx5X25hbWUiOiLnjosiLCJnaXZlbl9uYW1lIjoi5rC46IOcIiwiaWR0eXAiOiJ1c2VyIiwiaXBhZGRyIjoiMzQuODAuMzIuMTYiLCJuYW1lIjoi546LIOawuOiDnCIsIm9pZCI6IjA0YjVhNmZlLWE4YjItNDI2YS1iYWI3LThhZTdkMGEyNjgyMSIsInBsYXRmIjoiMyIsInB1aWQiOiIxMDAzMjAwMEQwMzJGQUU1IiwicHdkX2V4cCI6IjAiLCJwd2RfdXJsIjoiaHR0cHM6Ly9wb3J0YWwubWljcm9zb2Z0b25saW5lLmNvbS9DaGFuZ2VQYXNzd29yZC5hc3B4IiwicmgiOiIwLkFWTUF6Q0RpRWZNaTUwR0lMUS1IdVhXSFp0bGxWckdtN1pKQWhUa083RGRxX1ZsVEFKVS4iLCJzY3AiOiJGaWxlcy5SZWFkIEZpbGVzLlJlYWQuQWxsIEZpbGVzLlJlYWRXcml0ZSBGaWxlcy5SZWFkV3JpdGUuQWxsIFNpdGVzLlJlYWQuQWxsIHByb2ZpbGUgb3BlbmlkIGVtYWlsIiwic2lnbmluX3N0YXRlIjpbImttc2kiXSwic3ViIjoiMThldFRWV29sTmk1VXFmdjhJaGVnZnJzckQ4a3lhQ0JTOWxuek9qbUFUWSIsInRlbmFudF9yZWdpb25fc2NvcGUiOiJBUyIsInRpZCI6IjExZTIyMGNjLTIyZjMtNDFlNy04ODJkLTBmODdiOTc1ODc2NiIsInVuaXF1ZV9uYW1lIjoiTXdhbmdAbXJ3YW5nd3lzLm9ubWljcm9zb2Z0LmNvbSIsInVwbiI6Ik13YW5nQG1yd2FuZ3d5cy5vbm1pY3Jvc29mdC5jb20iLCJ1dGkiOiJxdW5SbTBnTnlFT21tbzZxcVJnLUFBIiwidmVyIjoiMS4wIiwid2lkcyI6WyI2MmU5MDM5NC02OWY1LTQyMzctOTE5MC0wMTIxNzcxNDVlMTAiLCJiNzlmYmY0ZC0zZWY5LTQ2ODktODE0My03NmIxOTRlODU1MDkiXSwieG1zX3N0Ijp7InN1YiI6Iks1NW91Z3ktRkZlMGgtRENBdHdIZ2w0ZFR0RjFXTktMcmFWTFVsNld4bkkifSwieG1zX3RjZHQiOjE1OTQ5MDI4NTl9.TJOyijN6IqnCAMNS3P27zAZ519KefhbjrzdbYDnpGjIT2WLXABR3YvFM1HGUu2JwEv9wNGrkynYKgKh9SVeDBEn5zg062u_IC41gQGcY6-qrsS16M0yfvRRXdnuoQSka4biT_nERRSli2CnhQo-hkvJZMsf2Trg18LfF57mgazYKWbUdT6xoDNnZDVvdbvqch-6Z5X7SazPekk_BzL22jg24gLNlXVJjSIh-pc9yK94LlCXyiHWHNvjl6K7Fe_EDKcuyqXTk7DENTOPk9O_h-SBrbjq8BNT_fzrdicWm6yih43zaRdEQYHivpiet3dcugQUIHvXM390ZT-aGSsmdkQ","token_type":"Bearer","refresh_token":"0.AVMAzCDiEfMi50GILQ-HuXWHZtllVrGm7ZJAhTkO7Ddq_VlTAJU.AgABAAAAAAD--DLA3VO7QrddgJg7WevrAgDs_wQA9P9LNZ0wHIvPnSbDED3cqMnpQ6n_VThxn2qp4fo90LU1tLVetSpZzMHmfqpgVDPuBghURhdVZhyi_iIaqH9zFVT9tARkq99axqEVY1NNdTB3x5G-1mMPTGKqF7JzHT_uDyPqHexNtTxEsdkrkBXh9EzUR8sjWmxgPNMmSTA6vKOTdeTCHk3DFWJc6O9yneFzu6GjEzmTTBuNJcVdlhYSiU8MVN5fBa2Unveacq-vIspQtKa6B-QC8woLxYYgI0vAAGPd_cog96yoCfD4aKgXF921hdkj0Ymqx2BtUdrQwiJRcFbWuvJ_KWqoHhf5WzBRS4kUYrsVjhWduZvtvxSSolLe-7ionCHfrkqDp7HIQEbBApIu-20OwSA4NRTVrmOQ2ssCCcKDtgl5cRgd_o2VZWIHZeqysJBRfSQXEbcnLxs4vDLhifwuX_uS6ugiw97iIF07OSsHr3Zx5kcP7Wl24nU_A-Ufgve4O8d_DiGSFBXTnAlp8p21wNhGSWirwYt-rgVcrQf3LWmVRcu-7E7YNvx5G-8uXKbR-Cky-o9ZPmAXrzjCySjkiaJzNO15ELq515snMT68ibUheM1hpzPjcjp75_9iwI1VaGw6L53ZkwolzkG7Ckdfykd6YjaCaLc76TFz0ZA5VjjYILLT_p4x_7FdQk064bhnYSBVNWlK4RFLQRgZT7ly6Fsp5TDnnCs4uY43nYrgEtvTMIdjVAcVoFQprZZBWR3D3dWDfu2kggYMhugeVadNTCJMyrDdCX3W2p3AYXyCGfZ6lkmFZH314h4U-YpkTVLLVcF1YWgJPyXGMGvZpSnI_-z_OdPcj8RLIFalwtIY9ffJsJqU-Xaoi27Wu3X6I680aHWHy2RoymXAEH-ow0AQJ2eFPj-fs6DKZCBQGA6ZA47iEl_9-QVQ4bDZ0LAj5VeasQtB3lx9jfZ8TS9Xb5WSncSBPj3EyHvwsNEZA1PwONluH_Fni9QnUw_8hImQGYlZuSupla2KgT4FdzEmik24IBlw58nDqZBrbmYaXkmV2GYUWJAiX2HN-lB1FHVbj1MDT83IXqom9ZfVPOxhZ2X5k8mP1un45Eswbx32Enn5","expiry":"2021-11-19T23:14:27.7373053+08:00"}
drive_id = b!OZedneScrUmdYF2xuvCoenl8mMSrvBxHvHm_hDeEqhnom7xn7SWjSZWYTqrw2N4T
drive_type = business
--------------------
y) Yes this is OK (default)
e) Edit this remote
d) Delete this remote
y/e/d>