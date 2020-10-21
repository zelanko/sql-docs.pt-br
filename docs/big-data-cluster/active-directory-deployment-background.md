---
title: Implantar vários no domínio do Active Directory
titleSuffix: SQL Server Big Data Cluster
description: Saiba como implantar vários Clusters de Big Data do SQL Server em um só domínio do Active Directory.
author: cloudmelon
ms.author: melqin
ms.reviewer: mikeray
ms.date: 09/30/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 4d5c30e4c3d7c3188920ecd15104b20a5472e306
ms.sourcegitcommit: 783b35f6478006d654491cb52f6edf108acf2482
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/09/2020
ms.locfileid: "91892496"
---
# <a name="deploy-multiple-big-data-clusters-2019-in-the-same-active-directory-domain"></a>Implantar vários [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] no mesmo domínio do Active Directory

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

Este artigo explica as atualizações do SQL Server 2019 CU 5 que habilitam a capacidade para que vários Clusters de Big Data do SQL Server 2019 sejam implantados e integrados ao mesmo Domínio do Active Directory.

Antes da CU5, havia dois problemas impedindo a implantação de vários BDCs (clusters de Big Data) em um domínio do AD.

- Conflito de nomenclatura para nomes da entidade de serviço e domínio DNS
- Nome da entidade de segurança da conta do domínio

## <a name="object-name-collisions"></a>Colisões de nome de objeto

### <a name="service-principal-names-spn-and-dns-domain-naming-conflict"></a>Conflito de SPN (nomes da entidade de serviço) e de nomenclatura de domínio DNS

O nome de domínio fornecido no momento da implantação é usado como domínio DNS do AD. Isso significa que os pods podem se conectar entre si na rede interna usando esse domínio DNS. Além disso, os usuários se conectam aos pontos de extremidade do BDC usando esse domínio DNS. Como resultado, qualquer SPN (nome da entidade de serviço) criado para um serviço no BDC terá o nome do pod, do serviço ou do ponto de extremidade do Kubernetes qualificado com esse domínio DNS do AD. Se um usuário implantar um segundo cluster no domínio, os SPNs que serão gerados terão o mesmo FQDN, pois os nomes de pod e o nome de domínio DNS não são diferentes entre os dois clusters. Como exemplo, considere um caso em que o domínio DNS do AD é `contoso.local`. Um dos SPNs gerados para o SQL Server do pool mestre no pod `master-0` seria `MSSQLSvc/master-0.contoso.local:1433`. No segundo cluster que o usuário tentasse implantar, o nome do pod para `master-0` seria o mesmo e o usuário forneceria o mesmo domínio DNS do AD (``contoso.local``), resultando na mesma cadeia de caracteres de SPN. O Active Directory proibiria a criação de um SPN conflitante ocasionando uma falha de implantação para o segundo cluster.

### <a name="domain-account-principal-names"></a>Nome da entidade de segurança da conta do domínio

Durante uma implantação do BDC com um domínio do Active Directory, várias entidades de segurança de conta são geradas para serviços em execução dentro do BDC. Essas entidades são basicamente contas de usuário do AD. Antes da CU5 os nomes dessas contas não seriam exclusivos entre clusters. Isso se manifesta na tentativa de criar o mesmo nome de conta de usuário para um serviço específico no BDC em dois clusters diferentes. O segundo cluster que está sendo implantado vai se deparar com um conflito no AD e não poderá criar sua conta.

## <a name="resolution-for-collisions"></a>Resolução para colisões

### <a name="solution-to-solve-the-problem-with-spns-and-dns-domain---cu5"></a>Solução para o problema com SPNs e domínio DNS – CU5

Como os SPNs devem diferir em dois clusters, o nome de domínio DNS passado no momento da implantação deve ser diferente. Você pode especificar nomes DNS diferentes usando a configuração introduzida recentemente no arquivo de configuração de implantação: `subdomain`. Se o subdomínio diferir entre dois clusters e a comunicação interna puder ocorrer nesse subdomínio, os SPNs incluirão o subdomínio, alcançando a exclusividade necessária.

>[!NOTE]
>O valor passado pela configuração do subdomínio não é um novo domínio do AD, mas um domínio DNS que é usado internamente.

Por exemplo, considere o caso de um SPN de SQL Server do pool mestre novamente. Se o subdomínio for `bdc`, o SPN abordado anteriormente será alterado para `MSSQLSvc/master-0.bdc.contoso.local:1433`.  

A personalização do valor do parâmetro subdomínio recém introduzido na especificação de configuração do Active Directory é opcional. Por padrão, o nome do cluster BDC ou o nome do namespace será usado para calcular o valor da configuração do subdomínio. Quando os usuários desejam substituir o nome do subdomínio, eles podem fazer isso por meio do novo parâmetro de subdomínio que está sendo introduzido na especificação de configuração do Active Directory.

### <a name="solution-to-solve-the-problem-regarding-account-names-uniqueness"></a>Solução para resolver o problema da exclusividade dos nomes de conta

Para atualizar os nomes de conta para um esquema que garanta a exclusividade, introduzimos o conceito de prefixo de conta. O prefixo de conta é uma parte do nome da conta que é exclusiva entre dois clusters. A parte restante do nome da conta é constante para um determinado serviço. O novo formato do nome da conta será parecido com `<prefix>-<name>-<podId>`. 

>[!NOTE]
>O Active Directory exige que os nomes das contas sejam limitados a 20 caracteres. O cluster BDC precisa usar oito dos caracteres para distinguir pods e StatefulSets. Isso deixa 12 caracteres como limite para o prefixo da conta

A personalização do nome da conta é opcional. Use o parâmetro `accountPrefix` na especificação de configuração do Active Directory. O SQL Server 2019 CU5 introduz o `accountPrefix` na especificação de configuração. Por padrão, o nome do subdomínio é usado como o prefixo da conta. Se o nome do subdomínio tiver mais de 12 caracteres, a substring inicial de 12 caracteres do nome do subdomínio será usada como prefixo da conta.

O subdomínio só se aplica ao DNS. Portanto, o novo nome de conta de usuário do LDAP é `bdc-ldap@contoso.local`. O nome da conta não seria `bdc-ldap@bdc.contoso.local`.

## <a name="semantics"></a>Semântica

Em suma, essas são as semânticas dos parâmetros adicionados na CU5 para vários clusters em um domínio:

### `subdomain`

- Campo opcional
- Tipo de dados: cadeia de caracteres
- Definição: Um subdomínio DNS exclusivo a ser usado para este BDC. Esse valor deve ser diferente para cada cluster implantado no domínio do Active Directory.  
- Valor padrão: Quando não for fornecido, o nome do cluster será usado como o valor padrão
- Comprimento máximo: 63 caracteres por rótulo (o rótulo sendo cada cadeia de caracteres separada por um ponto).
- Comentários: Os nomes DNS do ponto de extremidade devem usar o subdomínio em seu FQDN.

### `accountPrefix`

- Campo opcional
- Tipo de dados: cadeia de caracteres
- Definição: Um prefixo exclusivo para contas do AD que o cluster BDC gerará. Esse valor deve ser diferente para cada cluster implantado no domínio do Active Directory.
- Valor padrão: Quando não for fornecido, o nome do subdomínio será usado como o valor padrão. Quando o subdomínio não for fornecido, o nome do cluster será usado como o nome do subdomínio e, portanto, o nome do cluster também será herdado como accountPrefix. Se o subdomínio for fornecido e for um nome com várias partes (que contém um ou mais pontos), o usuário deverá fornecer um accountPrefix. 
- Comprimento máximo: 12 caracteres 

## <a name="impact-on-ad-domain-and-dns-server"></a>Impacto no domínio do AD e no servidor DNS 

Não há nenhuma alteração necessária no domínio do AD ou no controlador de domínio para acomodar a implantação de vários BDCs no mesmo domínio do Active Directory. O subdomínio DNS será criado automaticamente no servidor DNS ao registrar nomes DNS de pontos de extremidade externos. 

## <a name="impact-on-setting-up-the-deployment-configuration-file-used-for-the-bdc-deployment"></a>Impacto na configuração do arquivo de configuração de implantação usado para a implantação do BDC 

A seção *activeDirectory* na configuração do painel de controle *control.json* terá dois novos parâmetros opcionais: `subdomain` e `accountPrefix`. Forneça valores para essas configurações apenas se desejar substituir o comportamento padrão, que é usar o nome do cluster para cada um deles. O nome do cluster é o mesmo que o nome do namespace.

Além disso, você pode usar os nomes DNS do ponto de extremidade de sua escolha, desde que eles sejam totalmente qualificados e não entrem em conflito com os dois Clusters de Big Data implantados no mesmo domínio. Opcionalmente, você pode usar o valor de parâmetro do subdomínio para garantir que os nomes DNS sejam diferentes entre clusters.  Por exemplo, considere o ponto de extremidade do gateway. Se você quiser usar o nome `gateway` para o ponto de extremidade e registrá-lo no servidor DNS automaticamente como parte da implantação do BDC, use `gateway.bdc1.contoso.local` como o nome DNS. Se `bdc1` for o subdomínio e `contoso.local` for o nome de domínio DNS do AD. Outros valores aceitáveis são: `gateway-bdc1.contoso.local` ou simplesmente `gateway.contoso.local`.

## <a name="examples"></a>Exemplos

Abaixo está um exemplo de configuração de segurança do Active Directory, caso você queira substituir subdomínio e accountPrefix. 

```json
    "security": { 
        "activeDirectory": { 
            "ouDistinguishedName":"OU=contosoou,DC=contoso,DC=local", 
            "dnsIpAddresses": [ "10.10.10.10" ], 
            "domainControllerFullyQualifiedDns": [ "contoso-win2016-dc.contoso.local" ], 
            "domainDnsName":"contoso.local", 
            "subdomain": "bdc", 
            "accountPrefix": "myprefix", 
            "clusterAdmins": [ "contosoadmins" ], 
            "clusterUsers": [ "contosousers1", "contosousers2" ] 
        } 
    } 
  
```

Abaixo está um exemplo de especificação de ponto de extremidade para pontos de extremidades de painel de controle. Use qualquer valor para nomes DNS, contanto que eles sejam exclusivos e totalmente qualificados:
  
```json
        "endpoints": [ 
            { 
                "serviceType": "NodePort", 
                "port": 30080, 
                "name": "Controller", 
                "dnsName": "control-bdc1.contoso.local" 
            }, 
            { 
                "serviceType": "NodePort", 
                "port": 30777, 
                "name": "ServiceProxy", 
                "dnsName": "monitor-bdc1.contoso.local" 
            } 
        ] 
  
```

## <a name="questions"></a>Perguntas

### <a name="do-you-need-to-create-separate-ous-for-different-clusters"></a>Você precisa criar UOs separadas para clusters diferentes?

Isso não é obrigatório, mas é recomendado. Fornecer UOs separadas para clusters separados ajuda você a gerenciar as contas de usuário geradas.

### <a name="how-to-revert-back-to-the-pre-cu5-behavior"></a>Como reverter para o comportamento de antes da versão CU5?

Pode haver cenários em que você não poderá acomodar o parâmetro `subdomain` recém-introduzido. Por exemplo, você deve implantar uma versão anterior à CU5 e já atualizou a CLI `azdata`. Isso é muito improvável, mas se você precisar reverter para o comportamento de antes da versão CU5, defina o parâmetro `useSubdomain` como `false` na seção do Active Directory do `control.json`.

O exemplo a seguir define `useSubdomain` como `false` para esse cenário.

```console
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.activeDirectory.useSubdomain=false" 
```

## <a name="next-steps"></a>Próximas etapas

[Solucionar problemas de integração do Active Directory ao cluster de Big Data do SQL Server](troubleshoot-active-directory.md)
