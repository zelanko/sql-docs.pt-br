---
title: Implantar no modo do Active Directory
titleSuffix: SQL Server Big Data Cluster
description: Saiba como atualizar Clusters de Big Data do SQL Server em um domínio do Active Directory Domain Services.
author: cloudmelon
ms.author: melqin
ms.reviewer: mikeray
ms.date: 09/30/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 48dde8000274ea74df1c6095714b54669c5becdd
ms.sourcegitcommit: ae474d21db4f724523e419622ce79f611e956a22
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/20/2020
ms.locfileid: "92257286"
---
# <a name="deploy-sql-server-big-data-cluster-in-active-directory-mode"></a>Implantar um cluster de Big Data do SQL Server no modo do Active Directory Domain Services

Este artigo descreve como implantar um cluster de Big Data do SQL Server no modo do Active Directory. As etapas deste artigo exigem acesso a um domínio do Active Directory. Antes de prosseguir, você precisará concluir os requisitos explicados em [Implantar [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] no modo do Active Directory](active-directory-prerequisites.md).

## <a name="prepare-deployment"></a>Preparar a implantação

Para a implantação do BDC com a integração com o AD, algumas informações adicionais precisam ser fornecidas para a criação de objetos relacionados ao BDC no AD.

Usando o perfil `kubeadm-prod` (ou `openshift-prod` da versão CU5 em diante), você terá automaticamente os espaços reservados para as informações relacionadas à segurança e ao ponto de extremidade que são necessárias para a integração ao AD.

Além disso, você precisa fornecer credenciais que o [!INCLUDE[big-data-clusters](../includes/ssbigdataclusters-nover.md)] usará para criar os objetos necessários no AD. Essas credenciais são fornecidas como variáveis de ambiente.

## <a name="set-security-environment-variables"></a>Definir variáveis de ambiente de segurança

As variáveis de ambiente a seguir estão fornecendo as credenciais para a conta de serviço de domínio do BDC, que serão usadas para configurar a integração com o AD. Essa conta também é usada pelo BDC para manter os objetos do AD relacionados ao BDC no futuro.

```bash
export DOMAIN_SERVICE_ACCOUNT_USERNAME=<AD principal account name>
export DOMAIN_SERVICE_ACCOUNT_PASSWORD=<AD principal password>
```

## <a name="provide-security-and-endpoint-parameters"></a>Fornecer parâmetros de segurança e ponto de extremidade

Além das variáveis de ambiente para as credenciais, você também precisa fornecer informações de segurança e de ponto de extremidade para que a integração com o AD funcione. Os parâmetros necessários fazem parte automaticamente do [perfil de implantação](deployment-guidance.md#configfile) `kubeadm-prod`/`openshift-prod`.

A integração com o AD requer os seguintes parâmetros. Adicione esses parâmetros aos arquivos `control.json` e `bdc.json` usando os comandos `config replace` mostrados mais adiante neste artigo. Todos os exemplos a seguir estão usando o domínio de exemplo `contoso.local`.

- `security.activeDirectory.ouDistinguishedName`: nome diferenciado de uma UO (unidade organizacional) a que todas as contas do AD criadas pela implantação do cluster serão adicionadas. Se o nome do domínio for `contoso.local`, o nome diferenciado da UO será `OU=BDC,DC=contoso,DC=local`.

- `security.activeDirectory.dnsIpAddresses`: contém a lista de endereços IP de servidores DNS do domínio. 

- `security.activeDirectory.domainControllerFullyQualifiedDns`: lista de FQDNs do controlador de domínio. O FQDN contém o nome do computador/host do controlador de domínio. Se tiver vários controladores de domínio, você poderá fornecer uma lista aqui. Exemplo: `HOSTNAME.CONTOSO.LOCAL`.

  > [!IMPORTANT]
  > Quando vários controladores de domínio estão atendendo a um domínio, use o controlador de domínio primário como a primeira entrada na lista `domainControllerFullyQualifiedDns` na configuração de segurança. Para obter o nome do controlador de domínio primário, digite `netdom query fsmo` no prompt de comando e clique em **ENTER** .

- **Parâmetro opcional** `security.activeDirectory.realm`: na maioria dos casos, o realm é igual ao nome de domínio. Para casos em que eles não são iguais, use esse parâmetro para definir o nome do realm (por exemplo, `CONTOSO.LOCAL`). O valor fornecido para esse parâmetro precisa ser totalmente qualificado.

  > [!IMPORTANT]
  > No momento, o BDC não oferece suporte a uma configuração em que o nome de domínio do Active Directory seja diferente do nome **NETBIOS** do domínio do Active Directory.

- `security.activeDirectory.domainDnsName`: nome do domínio DNS que será usado para o cluster (por exemplo, `contoso.local`).

- `security.activeDirectory.clusterAdmins`: esse parâmetro usa um grupo do AD. O escopo do grupo do AD precisa ser universal ou global. Os membros desse grupo terão a função de cluster `bdcAdmin`, que fornecerá permissões de administrador no cluster. Isso significa que eles têm [permissões `sysadmin` no SQL Server](../relational-databases/security/authentication-access/server-level-roles.md#fixed-server-level-roles), [permissões `superuser` no HDFS](https://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html#The_Super-User) e permissões de administrador quando conectados ao ponto de extremidade do controlador.

  >[!IMPORTANT]
  >Crie esse grupo no AD antes do início da implantação. Se o escopo desse grupo do AD for o local do domínio, a implantação falhará.

- `security.activeDirectory.clusterUsers`: lista dos grupos do AD que são usuários comuns (sem permissões de administrador) no cluster de Big Data. A lista pode incluir grupos do AD que têm o escopo definido como grupos universais ou globais. Eles não podem ser grupos locais de domínio.

Os grupos do AD dessa lista são mapeados para a função de cluster de Big Data `bdcUser` e precisam receber acesso ao SQL Server (confira [Permissões do SQL Server](../relational-databases/security/permissions-hierarchy-database-engine.md)) ou ao HDFS (confira [Guia de permissões do HDFS](https://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html#:~:text=Permission%20Checks%20%20%20%20Operation%20%20,%20%20N%2FA%20%2029%20more%20rows%20)). Quando conectados ao ponto de extremidade do controlador, esses usuários só poderão listar os pontos de extremidade disponíveis no cluster usando o comando `azdata bdc endpoint list`.

Para obter detalhes sobre como atualizar os grupos do AD para essas configurações, confira [Gerenciar o acesso ao cluster de Big Data no modo do Active Directory](manage-user-access.md).

  >[!TIP]
  >Para habilitar a experiência de navegação HDFS quando conectado ao SQL Server mestre no Azure Data Studio, um usuário com a função bdcUser deve receber permissões de VIEW SERVER STATE, pois o Azure Data Studio usa a DMV `sys.dm_cluster_endpoints` a fim de obter o ponto de extremidade do gateway Knox necessário para se conectar ao HDFS.

  >[!IMPORTANT]
  >Crie esses grupos no AD antes do início da implantação. Se o escopo de qualquer um desses grupos do AD for o local do domínio, a implantação falhará.

  >[!IMPORTANT]
  >Se os usuários de domínio tiverem um grande número de associações a um grupo, você precisará ajustar os valores para a configuração do gateway `httpserver.requestHeaderBuffer` (o valor padrão é `8192`) e a configuração do HDFS `hadoop.security.group.mapping.ldap.search.group.hierarchy.levels` (o valor padrão é `10`) usando o arquivo de configuração de implantação *bdc.json* personalizado. Essa é uma melhor prática para evitar tempos limite de conexão para respostas de gateway e/ou HTTP com um código de status 431 ( *Campos de cabeçalho da solicitação muito grandes* ). Esta é uma seção do arquivo de configuração que mostra como definir os valores dessas configurações e quais são os valores recomendados para um número maior de associações a um grupo:

```json
{
    ...
    "spec": {
        "resources": {
            ...
            "gateway": {
                "spec": {
                    "replicas": 1,
                    "endpoints": [{...}],
                    "settings": {
                        "gateway-site.gateway.httpserver.requestHeaderBuffer": "65536"
                    }
                }
            },
            ...
        },
        "services": {
            ...
            "hdfs": {
                "resources": [...],
                "settings": {
                  "core-site.hadoop.security.group.mapping.ldap.search.group.hierarchy.levels": "4"
                }
            },
            ...
        }
    }
}
```

  >[!IMPORTANT]
  >Crie os grupos fornecidos para as configurações abaixo no AD antes do início da implantação. Se o escopo de qualquer um desses grupos do AD for o local do domínio, a implantação falhará.

- **Parâmetro opcional** `security.activeDirectory.appOwners`: lista dos grupos do AD que têm permissões para criar, excluir e executar qualquer aplicativo. A lista pode incluir grupos do AD que têm o escopo definido como grupos universais ou globais. Eles não podem ser grupos locais de domínio.

- **Parâmetro opcional** `security.activeDirectory.appReaders`: lista dos grupos do AD que têm permissões para executar qualquer aplicativo. A lista pode incluir grupos do AD que têm o escopo definido como grupos universais ou globais. Eles não podem ser grupos locais de domínio.

A tabela abaixo mostra o modelo de autorização para o gerenciamento de aplicativo:

|   Funções autorizadas   |   Comando [!INCLUDE [azure-data-cli-azdata](../includes/azure-data-cli-azdata.md)]   |
|----------------------|--------------------|
|   appOwner           | azdata app create  |
|   appOwner           | azdata app update  |
|   appOwner, appReader| azdata app list    |
|   appOwner, appReader| azdata app describe|
|   appOwner           | azdata app delete  |
|   appOwner, appReader| azdata app run     |

- `security.activeDirectory.subdomain`: **Parâmetro opcional** Esse parâmetro foi introduzido na versão SQL Server 2019 CU5 para dar suporte à implantação de vários Clusters de Big Data no mesmo domínio. Usando essa configuração, você pode especificar nomes DNS diferentes para cada cluster de Big Data implantado. Se o valor desse parâmetro não for especificado na seção do Active Directory do arquivo `control.json`, por padrão, o nome do cluster de Big Data (o mesmo que o nome do namespace do Kubernetes) será usado para calcular o valor da configuração de subdomínio. 

  >[!NOTE]
  >O valor transmitido pela configuração de subdomínio não é um novo domínio do AD, mas apenas um domínio DNS usado pelo cluster BDC internamente.

  >[!IMPORTANT]
  >Você precisará instalar ou atualizar a última versão da **[!INCLUDE [azure-data-cli-azdata](../includes/azure-data-cli-azdata.md)]** da versão SQL Server 2019 CU5 em diante para aproveitar essas novas funcionalidades e implantar vários Clusters de Big Data no mesmo domínio.

  Confira [Conceito: implantar [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] no modo do Active Directory](active-directory-deployment-background.md) para obter mais detalhes sobre a implantação de vários Clusters de Big Data no mesmo domínio do Active Directory.

- `security.activeDirectory.accountPrefix`: **Parâmetro opcional** Esse parâmetro foi introduzido na versão SQL Server 2019 CU5 para dar suporte à implantação de vários Clusters de Big Data no mesmo domínio. Essa configuração garante a exclusividade dos nomes de contas para vários serviços de Clusters de Big Data, que precisam ser diferentes entre dois clusters. A personalização do nome do prefixo da conta é opcional; por padrão, o nome do subdomínio é usado como o prefixo da conta. Se o nome do subdomínio tiver mais de 12 caracteres, os primeiros 12 caracteres do nome do subdomínio serão usados como o prefixo da conta.  

  >[!NOTE]
  >O Active Directory exige que os nomes das contas sejam limitados a 20 caracteres. O cluster BDC precisa usar oito dos caracteres para distinguir pods e StatefulSets. Isso deixa 12 caracteres como limite para o prefixo da conta

[Verifique o escopo do grupo do AD](/powershell/module/addsadministration/get-adgroup) para determinar se ele é DomainLocal.

Se ainda não tiver inicializado o arquivo de configuração de implantação, você poderá executar esse comando para obter uma cópia da configuração. Os exemplos abaixo usam o perfil `kubeadm-prod`; o mesmo se aplica a `openshift-prod`.

```bash
azdata bdc config init --source kubeadm-prod  --target custom-prod-kubeadm
```

Para definir os parâmetros acima no arquivo `control.json`, use os comandos [!INCLUDE [azure-data-cli-azdata](../includes/azure-data-cli-azdata.md)] a seguir. Os comandos substituem a configuração e fornecem seus próprios valores antes da implantação.

> [!IMPORTANT]
> Na versão SQL Server 2019 CU2, a estrutura da seção de configuração de segurança no perfil de implantação mudou de maneira clara e todas as configurações relacionadas ao Active Directory estão no novo `activeDirectory` na árvore json em `security` no arquivo `control.json`.

>[!NOTE]
> Além de fornecer valores diferentes para o subdomínio, conforme descrito nesta seção, você também precisará usar números de porta diferentes para pontos de extremidade do BDC ao implantar vários BDCs no mesmo cluster do Kubernetes. Esses números de porta são configuráveis no momento da implantação por meio dos perfis de [configuração de implantação](deployment-custom-configuration.md).

O exemplo abaixo se baseia no uso do SQL Server 2019 CU2. Ele mostra como substituir os valores de parâmetro relacionados ao AD na configuração de implantação. Os detalhes do domínio a seguir são valores de exemplo.

```bash
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.activeDirectory.ouDistinguishedName=OU\=bdc\,DC\=contoso\,DC\=local"
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.activeDirectory.dnsIpAddresses=[\"10.100.10.100\"]"
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.activeDirectory.domainControllerFullyQualifiedDns=[\"HOSTNAME.CONTOSO.LOCAL\"]"
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.activeDirectory.domainDnsName=contoso.local"
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.activeDirectory.clusterAdmins=[\"bdcadminsgroup\"]"
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.activeDirectory.clusterUsers=[\"bdcusersgroup\"]"
#Example for providing multiple clusterUser groups: [\"bdcusergroup1\",\"bdcusergroup2\"]
```

Opcionalmente, da versão SQL Server 2019 CU5 em diante, você pode substituir os valores padrão das configurações de `subdomain` e `accountPrefix`.

```bash
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.activeDirectory.subdomain=[\"bdctest\"]"
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.activeDirectory.accountPrefix=[\"bdctest\"]"
```

Da mesma forma, em versões anteriores à SQL Server 2019 CU2, você pode executar:

```bash
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.ouDistinguishedName=OU\=bdc\,DC\=contoso\,DC\=local"
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.dnsIpAddresses=[\"10.100.10.100\"]"
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.domainControllerFullyQualifiedDns=[\"HOSTNAME.CONTOSO.LOCAL\"]"
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.domainDnsName=contoso.local"
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.clusterAdmins=[\"bdcadminsgroup\"]"
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.clusterUsers=[\"bdcusersgroup\"]"
#Example for providing multiple clusterUser groups: [\"bdcusergroup1\",\"bdcusergroup2\"]
```

Além das informações acima, você também precisa fornecer nomes DNS para os diferentes pontos de extremidade do cluster. As entradas DNS que usam os nomes DNS fornecidos por você serão criadas automaticamente no servidor DNS após a implantação. Você usará esses nomes ao se conectar aos diferentes pontos de extremidade do cluster. Por exemplo, se o nome DNS da instância mestra do SQL for `mastersql` e considerando que o subdomínio usará o valor padrão do nome do cluster em `control.json`, você usará `mastersql.contoso.local,31433` ou `mastersql.mssql-cluster.contoso.local,31433` (dependendo dos valores fornecidos nos arquivos de configuração da implantação para os nomes DNS do ponto de extremidade) a fim de se conectar à instância mestra por meio das ferramentas. 

```bash
# DNS names for BDC services
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.spec.endpoints[0].dnsName=<controller DNS name>.contoso.local"
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.spec.endpoints[1].dnsName=<monitoring services DNS name>.<Domain name. e.g. contoso.local>"
azdata bdc config replace -c custom-prod-kubeadm/bdc.json -j "$.spec.resources.master.spec.endpoints[0].dnsName=<SQL Master Primary DNS name>.<Domain name. e.g. contoso.local>"
azdata bdc config replace -c custom-prod-kubeadm/bdc.json -j "$.spec.resources.master.spec.endpoints[1].dnsName=<SQL Master Secondary DNS name>.<Domain name. e.g. contoso.local>"
azdata bdc config replace -c custom-prod-kubeadm/bdc.json -j "$.spec.resources.gateway.spec.endpoints[0].dnsName=<Gateway (Knox) DNS name>.<Domain name. e.g. contoso.local>"
azdata bdc config replace -c custom-prod-kubeadm/bdc.json -j "$.spec.resources.appproxy.spec.endpoints[0].dnsName=<app proxy DNS name>.<Domain name. e.g. contoso.local>"
```

> [!IMPORTANT]
> Você pode usar os nomes DNS do ponto de extremidade de sua escolha, desde que eles sejam totalmente qualificados e não entrem em conflito com os dois Clusters de Big Data implantados no mesmo domínio. Opcionalmente, você pode usar o valor de parâmetro do `subdomain` para garantir que os nomes DNS sejam diferentes nos clusters. Por exemplo:

```bash
# DNS names for BDC services
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.spec.endpoints[0].dnsName=<controller DNS name>.<subdomain e.g. mssql-cluster>.contoso.local"
```

Você pode encontrar aqui um script de exemplo para [implantar um cluster de Big Data do SQL Server no cluster do Kubernetes de nó único (kubeadm) com a integração com o AD](https://github.com/microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/deployment/kubeadm/ubuntu-single-node-vm-ad).

> [!Note]
> Pode haver cenários em que você não poderá acomodar o parâmetro `subdomain` recém-introduzido. Por exemplo, você precisa implantar uma versão anterior à CU5 e já atualizou a **[!INCLUDE [azure-data-cli-azdata](../includes/azure-data-cli-azdata.md)]** . Isso é muito improvável, mas se você precisar revertê-lo para o comportamento de antes do CU5, defina o parâmetro `useSubdomain` como `false` na seção `control.json` do Active Directory.  Este é o comando usado para fazer isso:

```bash
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.activeDirectory.useSubdomain=false"
```

Agora, você precisa definir todos os parâmetros necessários para uma implantação do BDC com a integração do Active Directory.

Agora você pode implantar o cluster BDC integrado com Active Directory usando o comando [!INCLUDE [azure-data-cli-azdata](../includes/azure-data-cli-azdata.md)] e o perfil de implantação kubeadm-prod. Para obter a documentação completa de como implantar [!INCLUDE[big-data-clusters](../includes/ssbigdataclusters-nover.md)], acesse [Como implantar Clusters de Big Data do SQL Server no Kubernetes](deployment-guidance.md).

## <a name="verify-reverse-dns-entry-for-domain-controller"></a>Verificar a entrada DNS inversa para o controlador de domínio

Verifique se há uma entrada DNS inversa (registro PTR) para o próprio controlador de domínio, registrada no servidor DNS. Você pode verificar isso executando `nslookup` do nome de domínio no controlador de domínio para ver se ele pode ser resolvido para o endereço IP do controlador de domínio.

## <a name="known-issues-and-limitations"></a>Limitações e problemas conhecidos

**Limitações a serem consideradas no SQL Server 2019 CU5**

- atualmente, o Painel de Pesquisa de Logs e o Painel de Métricas não dão suporte à autenticação do AD. O nome de usuário e a senha básicos definidos na implantação podem ser usados para autenticação nesses painéis. Todos os outros pontos de extremidade do cluster dão suporte à autenticação do AD.

- No momento, o modo de segurança do AD só funciona em ambientes de implantação do `kubeadm` e do `openshift`, não no AKS nem no ARO. Por padrão, os perfis de implantação `kubeadm-prod` e `openshift-prod` incluem as seções de segurança.

- Antes da versão SQL Server CU5 2019, somente um BDC por domínio (Active Directory) era permitido. A habilitação de vários BDCs por domínio está disponível da versão CU5 em diante.

- Nenhum dos grupos do AD especificados nas configurações de segurança pode estar com escopo DomainLocal. Para verificar o escopo de um grupo do AD, siga [estas instruções](/powershell/module/addsadministration/get-adgroup).

- A conta do AD que pode ser usada para fazer logon no BDC é permitida no mesmo domínio que foi configurado para o BDC. Não há suporte para a habilitação de logons em outro domínio confiável.

## <a name="next-steps"></a>Próximas etapas

[Conectar [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]: modo do Active Directory](active-directory-connect.md)

[Solucionar problemas de integração do Active Directory ao cluster de Big Data do SQL Server](troubleshoot-active-directory.md)

[Conceito: implantar [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] no modo do Active Directory](active-directory-deployment-background.md)
