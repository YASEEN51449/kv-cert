# kv-cert
key-vault-certificate-upload
Key Vault Certificates Officer
Key Vault Secrets User
Key Vault Reader
Key Vault Certificates Officer
certmgr.msc


# 1.connect to azure account
    Connect-AzAccount -UseDeviceAuthentication
# 2.Create certificate
    New-SelfSignedCertificate -DnsName "yourdomain.com" -CertStoreLocation "Cert:\LocalMachine\My"
    
    Get-ChildItem -Path Cert:\LocalMachine\My | Where-Object { $_.DnsNameList -like "*yourdomain.com*" }
  
    $cert = New-SelfSignedCertificate -DnsName "yourdomain.com" -CertStoreLocation "Cert:\LocalMachine\My"


    $cert

# 3.list certificates list
    Get-ChildItem -Path Cert:\LocalMachine\My
# 4.UPLOAD CERTICATE TO KEYVAULT
    $vaultName = "Testkeyval"
    $certFilePath = "C:\Users\ny4010532\Documents\YourCertificate.pfx"  # Full path to the .pfx file
    $certName = "YourCertificate"          # The name for the certificate in Key Vault
    $certPassword = ConvertTo-SecureString -String "key@123" -AsPlainText -Force  # Password for the certificate

    # Import the certificate into Key Vault
    $cert = Import-AzKeyVaultCertificate -VaultName $vaultName -FilePath $certFilePath -Password $certPassword -Name $certName

    # Check if the certificate is uploaded successfully
    $cert
