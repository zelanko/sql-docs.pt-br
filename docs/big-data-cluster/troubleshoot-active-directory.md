---
title: Solucionar problemas de implantação do modo Active Directory
titleSuffix: SQL Server Big Data Cluster
description: Solucionar problemas de implantação de um cluster de Big Data do SQL Server em um domínio do Active Directory.
author: rl-msft
ms.author: rafidl
ms.reviewer: mikeray
ms.date: 03/12/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 5d887eadd021641241516a1478c6ac13e0d0bdec
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "79191207"
---
# <a name="troubleshoot-sql-server-big-data-cluster-active-directory-mode-deployment"></a>Solucionar problemas da implantação do modo Active Directory do Cluster de Big Data do SQL Server

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Este artigo explica como solucionar problemas de implantação de um Cluster de Big Data do SQL Server no modo Active Directory.

## <a name="check-deployment-progress"></a>Verificar o progresso da implantação

A implantação pode levar vários minutos. Se o cluster não estiver pronto após 15 minutos, verifique os logs do controlador para obter mais detalhes.

Durante a implantação do cluster, verifique os pods.

```console
kubectl get pods -n mssql-cluster
```

Verifique se a lista de pods retornada inclui:

- `compute-`$
- `data-`
- `storage-`

Se os pods de computação, dados e armazenamento não forem criados, verifique os logs para identificar o motivo.

## <a name="check-logs"></a>Verificar os logs

Para identificar por que a implantação é encerrada sem criar pods de computação, dados ou armazenamento, verifique os seguintes logs: 

- Verifique `controller.log` (`<folderOfDebugCopyLog>\debuglogs-mssql-cluster-20200219-093941\mssql-cluster\control-<suffix>\controller\controller\<date>\controller.log`). Procure a seguinte entrada:

  `WARN | StatefulSet master is not ready with 0 ready pods and 3 unready pods `

- Verifique `master-0` `provisioner.log` (`<folderOfDebugCopyLog>\debuglogs-mssql-cluster-20200219-093941\mssql-cluster\master-0\mssql-server\provisioner\provisioner.log`)

  ```
  ERROR | Failed to create sql login for domain user [<domain>.<top-level-domain>\<domain-group>]
    Traceback (most recent call last):
      File "/opt/provisioner/bin/scripts/provisioningpool.py", line 214, in executeNonQueries
        connection.execute_non_query(command)
      File "src/_mssql.pyx", line 1033, in _mssql.MSSQLConnection.execute_non_query
      File "src/_mssql.pyx", line 1061, in _mssql.MSSQLConnection.execute_non_query
      File "src/_mssql.pyx", line 1634, in _mssql.check_and_raise
      File "src/_mssql.pyx", line 1683, in _mssql.maybe_raise_MSSQLDatabaseException
    _mssql.MSSQLDatabaseException: (15401, b"Windows NT user or group '<domain>.<top-level-domain>\\<domain-group>' not found. Check the name again.DB-Lib error message 20018, severity 16:\nGeneral SQL Server error: Check messages from the SQL Server\n")
  WARNING | [3/3] Provisioning exception occurred during provisioning step: ProvisioningMasterPool.
  WARNING | Failed to create sql login for domain user [<domain>.<top-level-domain>\<domain-group>]
  WARNING | Retrying.
  ```

  No exemplo acima, a implantação não cria um logon para o usuário de domínio porque o grupo de domínio está no escopo como domínio local. Use grupos no escopo de domínio universal ou de domínio global. [Implantar [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] no modo Active Directory](deploy-active-directory.md) explica os requisitos de escopo do grupo do AD.

## <a name="check-the-scope-of-domain-groups"></a>Verifique o escopo dos grupos de domínio.

Verifique o escopo do grupo de domínio (<`domain-group`>). Use [get-adgroup](/powershell/module/addsadministration/get-adgroup/).

Se o escopo do grupo `<domain-group>` for local do domínio (`DomainLocal`), a implantação falhará. 

O script do PowerShell a seguir verifica o escopo de dois grupos do AD chamados `bdcadmins` e `bdcusers`. Substitua os nomes pelos nomes dos grupos. 

```powershell
#Administrators and users AD groups
$Cluster_admins_group='bdcadmins'
$Cluster_users_group='bdcusers'

#Performing AD Group Checks...

#AD admin group Check
$ClusterAdminGroupScope_Result = New-Object System.Collections.ArrayList
try {
    $GroupScope = Get-ADgroup -Identity $Cluster_admins_group | Select-Object -ExpandProperty GroupScope
    
    if ($GroupScope -eq 'DomainLocal') {
        [void]$ClusterAdminGroupScope_Result.Add("Misconfiguration - $Cluster_admins_group Group scope is $GroupScope, this scope is not supported, Please change group scope to either Global or Univesal") 
    }
    else {
        [void]$ClusterAdminGroupScope_Result.Add("OK - $Cluster_admins_group Group scope is $GroupScope")
    }
}
catch {
    [void]$ClusterAdminGroupScope_Result.Add("Error - " + $_.exception.message)
}
#Ad users group check
$ClusterUsersGroupScope_Result = New-Object System.Collections.ArrayList
$GroupScope = ''
try {
    $GroupScope = Get-ADgroup -Identity $Cluster_users_group | Select-Object -ExpandProperty GroupScope
    
    if ($GroupScope -eq 'DomainLocal') {
        [void]$ClusterUsersGroupScope_Result.Add("Misconfiguration - $Cluster_users_group Group scope is $GroupScope, this scope is not supported, Please change group scope to either Global or Univesal")
    } 
    else 
    { [void]$ClusterUsersGroupScope_Result.Add("OK - $Cluster_users_group Group scope is $GroupScope") }
}
catch {
    [void]$ClusterUsersGroupScope_Result.Add("Error - " + $_.exception.message)
}

#Display the results
$ClusterUsersGroupScope_Result
```

## <a name="check-security-support-container"></a>Verificar contêiner de suporte de segurança 

Examine os logs de contêiner de suporte de segurança.

O comando a seguir coleta os logs de suporte de segurança em um cluster no namespace `mssql-cluster`.

```console
azdata bdc debug copy-logs -n mssql-cluster -c security-support
```

Extraia os logs e localize `\mssql-cluster\control-<identifier>\controller\control-rts5t-controller-stdout.log`.

Procure as seguintes entradas no log:

```
ERROR    | Failed to create AD user account 'cntrl-controller'. Error code: 53. Message: Failed to create user object: Failed to add object 'CN=cntrl-controller,OU=bdc, DC=CONTOSO, DC=com' to '  <domain>.<top-level-domain>  ': Server is unwilling to perform. 
ERROR | Failed to create AD user account 'ldap-user'. Error code: 53. Message: Failed to create user object: Failed to add object 'CN=ldap-user,OU=bdc, DC=CONTOSO, DC=com' to '  <domain>.<top-level-domain>  ': Server is unwilling to perform. 
ERROR | Failed to create AD user account 'nginx-mgmtproxy'. Error code: 53. Message: Failed to create user object: Failed to add object 'CN=nginx-mgmtproxy,OU=bdc, DC=CONTOSO, DC=com' to '  <domain>.<top-level-domain>  ': Server is unwilling to perform.
```

Essas entradas podem acontecer quando o servidor DNS do controlador de domínio não tem uma entrada DNS reversa (registro PTR).

## <a name="verify-reverse-lookup-ptr-record"></a>Verificar a pesquisa inversa (registro PTR)
    
Execute o seguinte script do PowerShell para confirmar se você tem a entrada de DNS reversa (registro PTR) configurada.

```powershell
#Domain Controller FQDN 'DCserver01.contoso.local'
$Domain_controller_FQDN = 'DCserver01.contoso.local'

#Performing Domain Controller DNS record, reverse PTR Checks...
$DcControllerDnsPtr_Result = New-Object System.Collections.ArrayList
try {
    $Domain_controller_DNS_Record = Resolve-DnsName $Domain_controller_FQDN -Type A -Server $Domain_DNS_IP_address -ErrorAction Stop
    foreach ($ip in $Domain_controller_DNS_Record.IPAddress) {
        #resolving hostname by IP address to make sure we have reverse PTR record 
        if ((Resolve-DnsName $ip).NameHost -eq $Domain_controller_FQDN) {
            [void]$DcControllerDnsPtr_Result.add("OK - $Domain_controller_FQDN has an A record with an IP $ip, Reverse PTR record is in place") 
        }
        else {
            [void]$DcControllerDnsPtr_Result.add("Missing - $Domain_controller_FQDN has an A record with an IP $ip, But no reverse PTR record was found for the host")
        }
    }
}
catch {
    [void]$DcControllerDnsPtr_Result.add("Error - " + $_.exception.message)
}

#show the results 
$DcControllerDnsPtr_Result
```

[Verificar a entrada DNS reversa (registro PTR) para o controlador de domínio](deploy-active-directory.md#verify-reverse-dns-entry-for-domain-controller).