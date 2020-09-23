---
title: Implantar no modo do Active Directory
titleSuffix: SQL Server Big Data Cluster
description: Saiba como atualizar Clusters de Big Data do SQL Server em um domínio do Active Directory Domain Services.
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
ms.date: 08/04/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 345002bdf21ee13fc6d33c9cbc1e9938a8b58377
ms.sourcegitcommit: 1126792200d3b26ad4c29be1f561cf36f2e82e13
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/14/2020
ms.locfileid: "90076658"
---
# <a name="deploy-big-data-clusters-2019-in-active-directory-mode"></a>Implantar [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] no modo do Active Directory Domain Services

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

Este documento explica como implantar um BDC (cluster de Big Data) do SQL Server no modo de autenticação do Active Directory. O cluster usa um domínio existente do AD para autenticação.

>[!Note]
>Antes do lançamento do SQL Server 2019 CU5, havia uma restrição nos Clusters de Big Data que especificava que apenas um cluster podia ser implantado em um domínio do Active Directory. Essa restrição foi removida na versão CU5. Confira [Conceito: implantar [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] no modo do Active Directory](active-directory-deployment-background.md) para obter detalhes sobre as novas funcionalidades. Os exemplos deste artigo foram ajustados para acomodar os dois casos de uso de implantação.

## <a name="background"></a>Segundo plano

Para habilitar a autenticação do AD (Active Directory), o BDC cria automaticamente os usuários, os grupos, as contas de computadores e os SPNs (nomes da entidade de serviço) de que os diversos serviços do cluster. Para fornecer alguma independência a essas contas e permitir a definição de escopos para as permissões, durante a implantação, escolha uma UO (unidade organizacional) em que todos os objetos do AD relacionados ao BDC serão criados. Crie essa UO antes da implantação do cluster.

Para criar automaticamente todos os objetos necessários no Active Directory Domain Services, o BDC precisa de uma conta do AD durante a implantação. Essa conta precisa ter permissões para criar usuários, grupos e contas de computadores dentro da UO fornecida.

>[!IMPORTANT]
>Dependendo da política de expiração de senha definida no Controlador de Domínio, as senhas dessas contas podem expirar. A política de expiração padrão é de 42 dias. Não há mecanismo para girar credenciais para todas as contas no BDC, portanto, o cluster se tornará inoperante assim que o período de expiração for atingido. Para solucionar esse problema, atualize a política de expiração das contas de serviço BDC para “A senha nunca expira” no controlador de domínio. Essa ação pode ser realizada antes ou depois do horário de expiração. No último caso, o Active Directory reativará as senhas expiradas.
>
>A imagem a seguir mostra onde definir essa propriedade em Usuários e Computadores do Active Directory.
>
>:::image type="content" source="media/deploy-active-directory/image25.png" alt-text="Definir política de expiração de senha":::

Para obter uma lista de contas e grupos do AD, confira [Objetos do Active Directory gerados automaticamente](active-directory-objects.md).

As etapas a seguir pressupõem que você já tenha um controlador de domínio do Active Directory Domain Services. Se você não tem um controlador de domínio, o [guia](https://social.technet.microsoft.com/wiki/contents/articles/37528.create-and-configure-active-directory-domain-controller-in-azure-windows-server.aspx) a seguir inclui etapas que podem ser úteis.

## <a name="create-ad-objects"></a>Criar objetos do AD

Faça o seguinte antes de implantar um BDC com a integração do AD:

1. Crie uma UO (unidade organizacional) em que todos os objetos do AD do BDC serão armazenados. Como alternativa, você pode escolher uma UO existente durante a implantação.
1. Crie uma conta do AD para o BDC (ou use uma conta existente) e forneça a essa conta do AD do BDC as permissões corretas.

### <a name="create-a-user-in-ad-for-bdc-domain-service-account"></a>Crie um usuário no AD para a conta de serviço de domínio do BDC

O cluster de Big Data requer uma conta com permissões específicas. Antes de prosseguir, verifique se você tem uma conta existente do AD ou crie uma nova conta que o cluster de Big Data possa usar para configurar os objetos necessários.

Para criar um novo usuário no AD, você pode clicar com o botão direito do mouse no domínio ou na UO e selecionar **Novo** > **Usuário**:

![image12](./media/deploy-active-directory/image12.png)

Esse usuário será chamado de *conta de serviço de domínio do BDC* neste artigo.

### <a name="create-an-ou"></a>Criar uma UO

No controlador de domínio, abra **Usuários e Computadores do Active Directory**. No painel esquerdo, clique com o botão direito do mouse no diretório no qual deseja criar a UO e selecione **Nova** \> **Unidade Organizacional** e siga os avisos do assistente para criar a UO. Como alternativa, você pode criar uma UO com o PowerShell:

```powershell
New-ADOrganizationalUnit -Name "<name>" -Path "<Distinguished name of the directory you wish to create the OU in>"
```

Os exemplos deste artigo usam `bdc` como o nome da UO.

![image13](./media/deploy-active-directory/image13.png)

![image14](./media/deploy-active-directory/image14.png)

### <a name="set-permissions-for-an-ad-account"></a>Definir permissões para uma conta do AD 

Quer você tenha criado um novo usuário ou esteja usando um usuário existente do AD, há certas permissões que o usuário precisa ter. Essa conta é a conta de usuário que o controlador do BDC usará ao ingressar o cluster no AD.

A DSA (conta de serviço de domínio) do BDC precisa ser capaz de criar usuários, grupos e contas de máquina na UO. Nas etapas a seguir, demos à conta de serviço de domínio do BDC o nome `bdcDSA`. Você pode escolher qualquer nome para a conta.

1. No controlador de domínio, abra **Usuários e Computadores do Active Directory**

1. No painel esquerdo, navegue para seu domínio e, em seguida, para a UO que `bdc` usará

1. Clique com o botão direito do mouse na UO e selecione **Propriedades**.

1. Vá para a guia Segurança (verifique se você selecionou **Recursos Avançados** clicando com o botão direito do mouse na UO e selecionando **Exibir**)

    ![image15](./media/deploy-active-directory/image15.png)

1. Clique em **Adicionar...** e adicione o usuário do **bdcDSA**

    ![image16](./media/deploy-active-directory/image16.png)

    ![image17](./media/deploy-active-directory/image17.png)

1. Selecione o usuário do **bdcDSA**, desmarque todas as permissões e clique em **Avançado**

1. Clique em **Adicionar**

    ![image18](./media/deploy-active-directory/image18.png)

    - Clique em **Selecionar uma Entidade de Segurança**, insira **bdcDSA** e clique em OK

    - Defina o **Tipo** como **Permitir**

    - Defina **Aplica-se a** como **Este objeto e todos os descendentes**

        ![image19](./media/deploy-active-directory/image19.png)

    - Role até a parte inferior e clique em **Limpar tudo**

    - Role de volta para a parte superior e selecione:
       - **Ler todas as propriedades**
       - **Gravar todas as propriedades**
       - **Criar Objetos de computador**
       - **Excluir Objetos de computador**
       - **Criar Objetos de grupo**
       - **Excluir Objetos de grupo**
       - **Criar Objetos de usuário**
       - **Excluir objetos de usuário**

    - Clique em **OK**

- Clique em **Adicionar**

    - Clique em **Selecionar uma Entidade de Segurança**, insira **bdcDSA** e clique em OK

    - Defina o **Tipo** como **Permitir**

    - Defina **Aplica-se a** como **Objetos de computador descendentes**

    - Role até a parte inferior e clique em **Limpar tudo**

    - Role de volta para a parte superior e selecione **Redefinir senha**

    - Clique em **OK**

- Clique em **Adicionar**

    - Clique em **Selecionar uma Entidade de Segurança**, insira **bdcDSA** e clique em OK

    - Defina o **Tipo** como **Permitir**

    - Defina **Aplica-se a** como **Objetos de usuário descendentes**

    - Role até a parte inferior e clique em **Limpar tudo**

    - Role de volta para a parte superior e selecione **Redefinir senha**

    - Clique em **OK**

- Clique em **OK** mais duas vezes para fechar as caixas de diálogo abertas

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
  > Quando vários controladores de domínio estão atendendo a um domínio, use o controlador de domínio primário como a primeira entrada na lista `domainControllerFullyQualifiedDns` na configuração de segurança. Para obter o nome do controlador de domínio primário, digite `netdom query fsmo` no prompt de comando e clique em **ENTER**.

- **Parâmetro opcional** `security.activeDirectory.realm`: na maioria dos casos, o realm é igual ao nome de domínio. Para casos em que eles não são iguais, use esse parâmetro para definir o nome do realm (por exemplo, `CONTOSO.LOCAL`). O valor fornecido para esse parâmetro precisa ser totalmente qualificado.

  > [!IMPORTANT]
  > No momento, o BDC não oferece suporte a uma configuração em que o nome de domínio do Active Directory seja diferente do nome **NETBIOS** do domínio do Active Directory.

- `security.activeDirectory.domainDnsName`: nome do domínio DNS que será usado para o cluster (por exemplo, `contoso.local`).

- `security.activeDirectory.clusterAdmins`: esse parâmetro usa um grupo do AD. O escopo do grupo do AD precisa ser universal ou global. Os membros desse grupo terão a função de cluster *bdcAdmin*, que fornecerá permissões de administrador no cluster. Isso significa que eles têm [permissões `sysadmin` no SQL Server](../relational-databases/security/authentication-access/server-level-roles.md#fixed-server-level-roles), [permissões `superuser` no HDFS](https://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html#The_Super-User) e permissões de administrador quando conectados ao ponto de extremidade do controlador.

  >[!IMPORTANT]
  >Crie esse grupo no AD antes do início da implantação. Se o escopo desse grupo do AD for o local do domínio, a implantação falhará.

- `security.activeDirectory.clusterUsers`: lista dos grupos do AD que são usuários comuns (sem permissões de administrador) no cluster de Big Data. A lista pode incluir grupos do AD que têm o escopo definido como grupos universais ou globais. Eles não podem ser grupos locais de domínio.

Os grupos do AD dessa lista são mapeados para a função de cluster de Big Data *bdcUser* e precisam receber acesso ao SQL Server (confira [Permissões do SQL Server](../relational-databases/security/permissions-hierarchy-database-engine.md)) ou ao HDFS (confira [Guia de permissões do HDFS](https://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html#:~:text=Permission%20Checks%20%20%20%20Operation%20%20,%20%20N%2FA%20%2029%20more%20rows%20)). Quando conectados ao ponto de extremidade do controlador, esses usuários só poderão listar os pontos de extremidade disponíveis no cluster usando o comando *azdata bdc endpoint list*.

Para obter detalhes sobre como atualizar os grupos do AD para essas configurações, confira [Gerenciar o acesso ao cluster de Big Data no modo do Active Directory](manage-user-access.md).

  >[!TIP]
  >Para habilitar a experiência de navegação HDFS quando conectado ao SQL Server mestre no Azure Data Studio, um usuário com a função bdcUser deve receber permissões de VIEW SERVER STATE, pois o Azure Data Studio usa a DMV *sys.dm_cluster_endpoints* a fim de obter o ponto de extremidade do gateway Knox necessário para se conectar ao HDFS.

  >[!IMPORTANT]
  >Crie esses grupos no AD antes do início da implantação. Se o escopo de qualquer um desses grupos do AD for o local do domínio, a implantação falhará.

  >[!IMPORTANT]
  >Se os usuários de domínio tiverem um grande número de associações a um grupo, você precisará ajustar os valores para a configuração do gateway *httpserver.requestHeaderBuffer* (o valor padrão é *8192*) e a configuração do HDFS *hadoop.security.group.mapping.ldap.search.group.hierarchy.levels* (o valor padrão é *10*) usando o arquivo de configuração de implantação *bdc.json* personalizado. Essa é uma melhor prática para evitar tempos limite de conexão para respostas de gateway e/ou HTTP com um código de status 431 (*Campos de cabeçalho da solicitação muito grandes*). Esta é uma seção do arquivo de configuração que mostra como definir os valores dessas configurações e quais são os valores recomendados para um número maior de associações a um grupo: 

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

|   Funções autorizadas   |   azdata command   |
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
  >Você precisará instalar ou atualizar a última versão da **CLI do azdata** da versão SQL Server 2019 CU5 em diante para aproveitar essas novas funcionalidades e implantar vários Clusters de Big Data no mesmo domínio.

  Confira [Conceito: implantar [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] no modo do Active Directory](active-directory-deployment-background.md) para obter mais detalhes sobre a implantação de vários Clusters de Big Data no mesmo domínio do Active Directory.

- `security.activeDirectory.accountPrefix`: **Parâmetro opcional** Esse parâmetro foi introduzido na versão SQL Server 2019 CU5 para dar suporte à implantação de vários Clusters de Big Data no mesmo domínio. Essa configuração garante a exclusividade dos nomes de contas para vários serviços de Clusters de Big Data, que precisam ser diferentes entre dois clusters. A personalização do nome do prefixo da conta é opcional; por padrão, o nome do subdomínio é usado como o prefixo da conta. Se o nome do subdomínio tiver mais de 12 caracteres, os primeiros 12 caracteres do nome do subdomínio serão usados como o prefixo da conta.  

  >[!NOTE]
  >O Active Directory exige que os nomes das contas sejam limitados a 20 caracteres. O cluster BDC precisa usar oito dos caracteres para distinguir pods e StatefulSets. Isso deixa 12 caracteres como limite para o prefixo da conta

[Verifique o escopo do grupo do AD](/powershell/module/activedirectory/get-adgroup?view=winserver2012-ps&viewFallbackFrom=winserver2012r2-ps) para determinar se ele é DomainLocal.

Se ainda não tiver inicializado o arquivo de configuração de implantação, você poderá executar esse comando para obter uma cópia da configuração. Os exemplos abaixo usam o perfil `kubeadm-prod`; o mesmo se aplica a `openshift-prod`.

```bash
azdata bdc config init --source kubeadm-prod  --target custom-prod-kubeadm
```

Para definir os parâmetros acima no arquivo `control.json`, use os comandos `azdata` a seguir. Os comandos substituem a configuração e fornecem seus próprios valores antes da implantação.

> [!IMPORTANT]
> Na versão SQL Server 2019 CU2, a estrutura da seção de configuração de segurança no perfil de implantação mudou de maneira clara e todas as configurações relacionadas ao Active Directory estão no novo *activeDirectory* na árvore json em *security* no arquivo *control.json*.

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

Além das informações acima, você também precisa fornecer nomes DNS para os diferentes pontos de extremidade do cluster. As entradas DNS que usam os nomes DNS fornecidos por você serão criadas automaticamente no servidor DNS após a implantação. Você usará esses nomes ao se conectar aos diferentes pontos de extremidade do cluster. Por exemplo, se o nome DNS da instância mestra do SQL for `mastersql` e considerando que o subdomínio usará o valor padrão do nome do cluster em *control.json*, você usará `mastersql.contoso.local,31433` ou `mastersql.mssql-cluster.contoso.local,31433` (dependendo dos valores fornecidos nos arquivos de configuração da implantação para os nomes DNS do ponto de extremidade) a fim de se conectar à instância mestra por meio das ferramentas. 

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
> Pode haver cenários em que você não poderá acomodar o parâmetro `subdomain` recém-introduzido. Por exemplo, você precisará implantar uma versão anterior à CU5 e já ter atualizado a **CLI do azdata**. Isso é muito improvável, mas se você precisar revertê-lo para o comportamento de antes do CU5, defina o parâmetro `useSubdomain` como `false` na seção `control.json` do Active Directory.  Este é o comando usado para fazer isso:

```bash
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.activeDirectory.useSubdomain=false"
```

Agora, você precisa definir todos os parâmetros necessários para uma implantação do BDC com a integração do Active Directory.

Agora você pode implantar o cluster BDC integrado com Active Directory usando o comando `azdata` e o perfil de implantação kubeadm-prod. Para obter a documentação completa de como implantar [!INCLUDE[big-data-clusters](../includes/ssbigdataclusters-nover.md)], acesse [Como implantar Clusters de Big Data do SQL Server no Kubernetes](deployment-guidance.md).

## <a name="verify-reverse-dns-entry-for-domain-controller"></a>Verificar a entrada DNS inversa para o controlador de domínio

Verifique se há uma entrada DNS inversa (registro PTR) para o próprio controlador de domínio, registrada no servidor DNS. Você pode verificar isso executando `nslookup` do nome de domínio no controlador de domínio para ver se ele pode ser resolvido para o endereço IP do controlador de domínio.

## <a name="connect-to-cluster-endpoints-in-ad-mode"></a>Conectar-se a pontos de extremidade do cluster no modo do AD

Faça logon na instância mestre do SQL Server com AD Auth.

Para verificar as conexões do AD com a instância do SQL Server, conecte-se à instância do SQL mestre com `sqlcmd`. Os logons são criados automaticamente para os grupos fornecidos na implantação (`clusterUsers` e `clusterAdmins`).

Se estiver usando Linux, primeiro execute `kinit` como o usuário do AD e, em seguida, execute `sqlcmd`. Se estiver usando o Windows, basta fazer logon como o usuário desejado em um **computador cliente ingressado no domínio**.

### <a name="connect-to-master-instance-from-linuxmac"></a>Conectar-se à instância mestre do Linux/Mac

```bash
kinit <username>@<domain name>
sqlcmd -S <DNS name for master instance>,31433 -E
```

### <a name="connect-to-master-instance-from-windows"></a>Conectar-se à instância mestre do Windows

```cmd
sqlcmd -S <DNS name for master instance>,31433 -E
```

### <a name="log-in-to-sql-server-master-instance-using-azure-data-studio-or-ssms"></a>Faça logon na instância mestre do SQL Server usando o Azure Data Studio ou o SSMS

Em um cliente ingressado no domínio, você pode abrir o SSMS ou o Azure Data Studio e conectar-se à instância mestre. Essa é a mesma experiência que se conectar a qualquer instância do SQL Server usando a autenticação do AD.

Do SSMS:

![image23](./media/deploy-active-directory/image23.png)

Do Azure Data Studio:

![image24](./media/deploy-active-directory/image24.png)}

### <a name="log-in-to-controller-with-ad-authentication"></a>Fazer logon no controlador com a autenticação do AD

#### <a name="connect-to-controller-with-ad-authentication-from-linuxmac"></a>Conectar-se ao controlador com a autenticação do AD do Linux/Mac

Há duas opções para se conectar ao ponto de extremidade do controlador usando o `azdata` e a autenticação do AD. Use o parâmetro *--endpoint/-e*:

```bash
kinit <username>@<domain name>
azdata login -e https://<controller DNS name>:30080 --auth ad
```

Como alternativa, você pode se conectar usando o parâmetro *--namespace/-n*, que é o nome do cluster de Big Data:

```bash
kinit <username>@<domain name>
azdata login -n <clusterName> --auth ad
```

#### <a name="connect-to-controller-with-ad-authentication-from-windows"></a>Conectar-se ao controlador com a autenticação do AD do Windows

```cmd
azdata login -e https://<controller DNS name>:30080 --auth ad
```

### <a name="use-ad-authentication-to-knox-gateway-webhdfs"></a>Usar a autenticação do AD para o gateway do Knox (webHDFS)

Você também pode emitir comandos do HDFS usando ondulação por meio do ponto de extremidade do gateway do Knox. Isso requer a autenticação do AD para o Knox. O comando de ondulação abaixo emite uma chamada REST webHDFS por meio do gateway do Knox para criar um diretório chamado `products`

```bash
curl -k -v --negotiate -u : https://<Gateway DNS name>:30443/gateway/default/webhdfs/v1/products?op=MKDIRS -X PUT
```

## <a name="known-issues-and-limitations"></a>Limitações e problemas conhecidos

**Limitações a serem consideradas no SQL Server 2019 CU5**

- atualmente, o Painel de Pesquisa de Logs e o Painel de Métricas não dão suporte à autenticação do AD. O nome de usuário e a senha básicos definidos na implantação podem ser usados para autenticação nesses painéis. Todos os outros pontos de extremidade do cluster dão suporte à autenticação do AD.

- No momento, o modo de segurança do AD só funciona em ambientes de implantação do `kubeadm` e do `openshift`, não no AKS nem no ARO. Por padrão, os perfis de implantação `kubeadm-prod` e `openshift-prod` incluem as seções de segurança.

- Antes da versão SQL Server CU5 2019, somente um BDC por domínio (Active Directory) era permitido. A habilitação de vários BDCs por domínio está disponível da versão CU5 em diante.

- Nenhum dos grupos do AD especificados nas configurações de segurança pode estar com escopo DomainLocal. Para verificar o escopo de um grupo do AD, siga [estas instruções](/powershell/module/activedirectory/get-adgroup?view=winserver2012-ps&viewFallbackFrom=winserver2012r2-ps).

- A conta do AD que pode ser usada para fazer logon no BDC é permitida no mesmo domínio que foi configurado para o BDC. Não há suporte para a habilitação de logons em outro domínio confiável.

## <a name="next-steps"></a>Próximas etapas

[Solucionar problemas de integração do Active Directory ao cluster de Big Data do SQL Server](troubleshoot-active-directory.md)

[Conceito: implantar [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] no modo do Active Directory](active-directory-deployment-background.md)
