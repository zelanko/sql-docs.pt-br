---
title: Implantação do modo AD interrompida – entrada da zona de pesquisa inversa ausente para o DC
titleSuffix: SQL Server Big Data Cluster
description: A implantação do BDC com o modo AD está paralisada devido à ausência da entrada da zona de pesquisa inversa para o controlador de domínio no servidor DNS do controlador de domínio.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mikeray
ms.date: 04/21/2020
ms.topic: how-to
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 63086a762e8c55109a43a32e39868b65808108f9
ms.sourcegitcommit: ae474d21db4f724523e419622ce79f611e956a22
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/20/2020
ms.locfileid: "92257086"
---
# <a name="ad-mode-deployment-stopped---missing-reverse-lookup-zone-entry-for-dc"></a>Implantação do modo AD interrompida – entrada da zona de pesquisa inversa ausente para o DC

A implantação no modo AD (Active Directory) congela. Verifique os sintomas para ver se a causa é a entrada de zona de pesquisa inversa ausente no servidor DNS do controlador de domínio. 

## <a name="symptom"></a>Sintoma

Você começou a implantar o BDC com o modo AD, mas a implantação está paralisada e não está avançando.

O exemplo a seguir mostra os resultados da implantação em um shell com o bash.

```
The privacy statement can be viewed at:
https://go.microsoft.com/fwlink/?LinkId=853010
 
The license terms for SQL Server Big Data Cluster can be viewed at:
Enterprise: https://go.microsoft.com/fwlink/?linkid=2104292
Standard: https://go.microsoft.com/fwlink/?linkid=2104294
Developer: https://go.microsoft.com/fwlink/?linkid=2104079
 
Cluster deployment documentation can be viewed at:
https://aka.ms/bdc-deploy
 
NOTE: Cluster creation can take a significant amount of time depending on
configuration, network speed, and the number of nodes in the cluster.
 
Starting cluster deployment.
Cluster controller endpoint is available at bdc-control.contoso.com:30080, 193.168.5.14:30080.
Waiting for control plane to be ready after 5 minutes.
Waiting for control plane to be ready after 10 minutes.
Waiting for control plane to be ready after 15 minutes.
Waiting for control plane to be ready after 20 minutes.
Waiting for control plane to be ready after 25 minutes.
```

Verifique os pods implantados atualmente.

```bash
kubectl get pods -n mssql-cluster
```

Os resultados abaixo indicam que somente os pods que pertencem ao controlador foram implantados. Os pods para computação, dados ou armazenamento não estão sendo criados.

```
NAME              READY   STATUS    RESTARTS   AGE
control-rts5t     3/3     Running   0          18m
controldb-0       2/2     Running   0          18m
controlwd-csgst   1/1     Running   0          16m
dns-7kfnz         2/2     Running   0          16m
logsdb-0          1/1     Running   0          16m
logsui-2pc29      1/1     Running   0          16m
metricsdb-0       1/1     Running   0          16m
metricsdc-4rtm4   1/1     Running   0          16m
metricsdc-6lr2t   1/1     Running   0          16m
metricsdc-ftx9m   1/1     Running   0          16m
metricsdc-h59jb   1/1     Running   0          16m
metricsui-lvdpt   1/1     Running   0          16m
mgmtproxy-mkmxp   2/2     Running   0          16m
```

Inspecione os logs de contêiner de suporte de segurança. Procure por erros de LDAP. 

## <a name="check-security-support-container"></a>Verificar contêiner de suporte de segurança 

Examine os logs de contêiner de suporte de segurança.

O comando a seguir coleta os logs de suporte de segurança em um cluster no namespace `mssql-cluster`.

```bash
azdata bdc debug copy-logs -n mssql-cluster -c security-support
```

Extraia os logs e localize `\mssql-cluster\control-<identifier>\controller\control-rts5t-controller-stdout.log`.

> [!TIP]
> Há várias maneiras de coletar os logs. Em vez de copiar os logs com [!INCLUDE [azure-data-cli-azdata](../includes/azure-data-cli-azdata.md)], você pode usar um bloco de anotações no Azure Data Studio.
> No Azure Data Studio, conecte-se ao cluster de Kubernetes e execute um bloco de anotações de solução de problemas apropriado. Estes são exemplos de bloco de anotações:
>
> - TSG027 – Observar a implantação de cluster
> - TSG061 – Obter a parte final de todos os logs de contêiner para os pods no namespace do BDC
> - TSG001 – Executar `azdata copy-logs`
>

## <a name="inspect-the-logs"></a>Inspecionar os logs

Localize o log. O exemplo a seguir aponta para um log de implantação do controlador. 

`<folderOfDebugCopyLog>\debuglogs-mssql-cluster-YYYYMMDD-HHMMSS\<namespace>\control-<identifier>\controller\control-<identifier>-controller-stdout.log`"

```
YYYY-MM-DD HH:MM:SS.ms | ERROR | Failed to create AD user account 'cntrl-controller'. Error code: 53. Message: Failed to create user object: Failed to add object 'CN=cntrl-controller,OU=bdc, DC=CONTOSO, DC=com' to 'CONTOSO.COM': Server is unwilling to perform. 
YYYY-MM-DD HH:MM:SS.ms | ERROR | Failed to create AD user account 'ldap-user'. Error code: 53. Message: Failed to create user object: Failed to add object 'CN=ldap-user,OU=bdc, DC=CONTOSO, DC=com' to 'CONTOSO.COM': Server is unwilling to perform. 
YYYY-MM-DD HH:MM:SS.ms | ERROR | Failed to create AD user account 'nginx-mgmtproxy'. Error code: 53. Message: Failed to create user object: Failed to add object 'CN=nginx-mgmtproxy,OU=bdc, DC=CONTOSO, DC=com' to 'CONTOSO.COM': Server is unwilling to perform. 
```

## <a name="cause"></a>Causa

A entrada da zona de pesquisa inversa para o controlador de domínio na entrada DNS do controlador de domínio está ausente. 

## <a name="resolution"></a>Resolução

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

## <a name="next-steps"></a>Próximas etapas

[Verificar a entrada DNS reversa (registro PTR) para o controlador de domínio](active-directory-deploy.md#verify-reverse-dns-entry-for-domain-controller).
