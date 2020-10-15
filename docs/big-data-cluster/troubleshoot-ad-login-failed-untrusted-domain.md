---
title: Falha no logon no modo AD – domínio não confiável
titleSuffix: SQL Server Big Data Cluster
description: Corrigir comportamento – os clientes falham em Autenticar quando as entradas DNS dos pontos de extremidade são configuradas como CNAME apontando para um nome de alias.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mikeray
ms.date: 05/01/2020
ms.topic: how-to
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 669d8f050c3dd86d733c33741eb6fc846245aff2
ms.sourcegitcommit: 783b35f6478006d654491cb52f6edf108acf2482
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/09/2020
ms.locfileid: "91891036"
---
# <a name="symptom-ad-mode-login-fails---untrusted-domain-big-data-clusters"></a>Sintoma: Falhas de logon no modo AD – domínio não confiável (Clusters de Big Data)

Em um SQL Server BDC (Cluster de Big Data) no modo Active Directory, uma tentativa de conexão pode falhar e a tentativa de conexão retorna o seguinte erro:

`Login failed. The login is from an untrusted domain and cannot be used with Integrated authentication.`

Isso pode ocorrer quando você configurou entradas DNS como CNAME apontando para um nome de alias de proxy reverso que distribui o tráfego para nós do Kubernetes.

## <a name="root-cause"></a>Causa raiz

Quando os pontos de extremidade são configurados com entradas DNS com CNAME apontando para um nome de alias de proxy reverso que distribui o tráfego para nós do Kubernetes:

- O processo de autenticação Kerberos procura um SPN (nome da entidade de serviço) que corresponda à entrada para CNAME. Não é o SPN verdadeiro registrado pelo BDC no Active Directory
- A autenticação falha 

## <a name="confirm-root-cause"></a>Confirmar causa raiz

Após a falha de autenticação, verifique o cache de tíquetes do Kerberos. 

Para verificar o cache de tíquetes, use o comando `klist`. 

Procure um tíquete com um SPN correspondente ao ponto de extremidade ao qual você tentou se conectar.

O tíquete esperado não está lá.

Neste exemplo, um ponto de extremidade mestre, registro DNS `bdc-sql` é o CNAME definido como proxy reverso chamado `ServerReverseProxy`

```PowerShell
Resolve-DnsName bdc-sql
```

A seção a seguir mostra os resultados do comando anterior.

```
Name                           Type   TTL   Section    NameHost
----                           ----   ---   -------    --------
bdc-sql.mydomain.com           CNAME  3600  Answer     ReverseProxyServer.mydomain.com

Name       : ReverseProxyServer.mydomain.com
QueryType  : A
TTL        : 3600
Section    : Answer
IP4Address : 193.168.5.10
```

>[!NOTE]
>A seção a seguir faz referência a [`tshark`](https://www.wireshark.org/docs/man-pages/tshark.html). `tshark` o é um utilitário de linha de comando instalado como parte do utilitário de rastreamento de rede [Wireshark](https://www.wireshark.org/docs/).

Para ver o SPN solicitado no Active Directory, use `tshark`. O comando a seguir limita a captura de rastreamento de rede para a comunicação do protocolo Kerberos e mostra apenas `krb-error (30)` mensagens. Essas mensagens devem conter mensagens de solicitação de SPN com falha.

```bash
tshark -Y "kerberos && kerberos.msg_type == 30" -T fields -e kerberos.error_code -e kerberos.SNameString
```

Em um shell de comando diferente, tente se conectar ao pod mestre:

```bash
klist purge

sqlcmd -S bdc-sql.mydomain.com,31433 -E
```

Confira o exemplo de saída a seguir.

```bash
klist purge

Current LogonId is 0:0xf6b58
        Deleting all tickets:
        Ticket(s) purged!

sqlcmd -S bdc-sql.mydomain.com,31433 -E
sqlcmd: Error: Microsoft ODBC Driver 17 for SQL Server : Login failed. The login is from an untrusted domain and cannot be used with Integrated authentication.
```

Verifique a saída `tshark`. 

```bash
Capturing on 'Ethernet 3'
25      krbtgt,RLAZURE.COM
7       MSSQLSvc,ReverseProxyServer.mydomain.com:31433
2 packets captured
```

Observe que o cliente solicita `SPN MSSQLSvc,ReverseProxyServer.mydomain.com:31433`, que não existe. A tentativa de conexão acaba falhando com o erro 7. O erro 7 significa `KRB5KDC_ERR_S_PRINCIPAL_UNKNOWN Server not found in Kerberos database`.

Na configuração correta, o cliente solicita o SPN registrado pelo BDC. No exemplo, o SPN correto teria sido `MSSQLSvc,bdc-sql.mydomain.com:31433`.

>[!NOTE]
>O erro 25 significa `KDC_ERR_PREAUTH_REQUIRED` – pré-autenticação adicional é necessária. Isso pode ser ignorado com segurança. `KDC_ERR_PREAUTH_REQUIRED` é retornado na solicitação inicial do AD do Kerberos. Por padrão, o cliente Kerberos do Windows não está incluindo informações de pré-autenticação nesta primeira solicitação.

Para ver a lista de SPN registrada pelo BDC para o ponto de extremidade mestre, execute `setspn -L mssql-master`. 

Confira o seguinte exemplo de saída:

```bash
Registered ServicePrincipalNames for CN=mssql-master,OU=bdc,DC=mydomain,DC=com:
        MSSQLSvc/bdc-sqlread.mydomain.com:31436
        MSSQLSvc/-sqlread:31436
        MSSQLSvc/bdc-sqlread.mydomain.com
        MSSQLSvc/bdc-sqlread
        MSSQLSvc/bdc-sql.mydomain.com:31433
        MSSQLSvc/bdc-sql:31433
        MSSQLSvc/bdc-sql.mydomain.com
        MSSQLSvc/bdc-sql
        MSSQLSvc/master-p-svc.mydomain.com:1533
        MSSQLSvc/master-p-svc:1533
        MSSQLSvc/master-p-svc.mydomain.com:1433
        MSSQLSvc/master-p-svc:1433
        MSSQLSvc/master-p-svc.mydomain.com
        MSSQLSvc/master-p-svc
        MSSQLSvc/master-svc.mydomain.com:1533
        MSSQLSvc/master-svc:1533
        MSSQLSvc/master-svc.mydomain.com:1433
        MSSQLSvc/master-svc:1433
        MSSQLSvc/master-svc.mydomain.com
        MSSQLSvc/master-svc
```

Nos resultados acima, o endereço do proxy reverso não deve ser registrado.

## <a name="resolve"></a>Resolver

Esta seção mostra duas maneiras de resolver o problema. Depois de fazer as alterações apropriadas, execute `ipconfig -flushdns` e `klist purge` em seu cliente. Então tente conectar novamente.

### <a name="option-1"></a>Opção 1

Remova o registro CNAME de cada ponto de extremidade do BDC no DNS e substitua por vários registros de `A` que apontam para cada nó do Kubernetes ou cada mestre do Kubernetes se você tiver mais de um mestre.

>[!TIP]
>O script descrito abaixo usa o PowerShell. Confira [Como instalar o PowerShell no Linux](/powershell/scripting/install/installing-powershell-core-on-linux) para obter mais informações.

Você pode usar o script do PowerShell a seguir para atualizar os registros de pontos de extremidade de DNS. Execute o script de qualquer computador conectado ao mesmo domínio:

```powershell
#Specify the DNS server, example contoso.local
$Domain_DNS_name=mydomain.com'

#DNS records for bdc endpoints
$Controller_DNS_name = 'bdc-control'
$Managment_proxy_DNS_name= 'bdc-proxy'
$Master_Primary_DNS_name = 'bdc-sql'
$Master_Secondary_DNS_name = 'bdc-sqlread'
$Gateway_DNS_name = 'bdc-gateway'
$AppProxy_DNS_name = 'bdc-appproxy'

#Performing Endpoint DNS records Checks..

#Build array of endpoints 
$BdcEndpointsDns = New-Object System.Collections.ArrayList

[void]$BdcEndpointsDns.Add($Controller_DNS_name)
[void]$BdcEndpointsDns.Add($Managment_proxy_DNS_name)
[void]$BdcEndpointsDns.Add($Master_Primary_DNS_name)
[void]$BdcEndpointsDns.Add($Master_Secondary_DNS_name)
[void]$BdcEndpointsDns.Add($Gateway_DNS_name)
[void]$BdcEndpointsDns.Add($AppProxy_DNS_name)

#Build arrary for results 
$BdcEndpointsDns_Result = New-Object System.Collections.ArrayList

foreach ($DnsName in $BdcEndpointsDns) {
    try {
        $endpoint_DNS_record = Resolve-DnsName $DnsName -Type A -Server $Domain_DNS_IP_address -ErrorAction Stop 
        foreach ($ip in $endpoint_DNS_record.IPAddress) {
            [void]$BdcEndpointsDns_Result.Add("OK - $DnsName is an A record with an IP $ip")
        }
    }
    catch {
        [void]$BdcEndpointsDns_Result.Add("MisConfiguration - $DnsName is not an A record or does not exists")
    }  
}

#show the results 
$BdcEndpointsDns_Result
```

### <a name="option-2"></a>Opção 2

Como alternativa, é possível contornar o problema modificando o CNAME para apontar para o endereço IP do proxy reverso, em vez do nome do proxy reverso.

## <a name="confirm-resolution"></a>Confirmar resolução

Depois de resolver a correção com uma das opções acima, confirme a correção conectando-se ao Cluster de Big Data com o Active Directory.

## <a name="next-steps"></a>Próximas etapas

[Verificar a entrada DNS reversa (registro PTR) para o controlador de domínio](active-directory-deploy.md#verify-reverse-dns-entry-for-domain-controller).
