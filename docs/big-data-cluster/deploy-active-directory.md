---
title: Implantar no modo do Active Directory
titleSuffix: SQL Server Big Data Cluster
description: Saiba como atualizar Clusters de Big Data do SQL Server em um domínio do Active Directory Domain Services.
author: NelGson
ms.author: negust
ms.reviewer: mikeray
ms.date: 02/28/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: e2ce3fd5655655686d6fb27f628f6bdb3d22ceb1
ms.sourcegitcommit: 7e544aa10f66bb1379bb5675fc063b2097631823
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/29/2020
ms.locfileid: "78200957"
---
# <a name="deploy-big-data-clusters-2019-in-active-directory-mode"></a>Implantar [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] no modo do Active Directory Domain Services

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Este documento descreve a implantação de um BDC (cluster de Big Data) do SQL Server 2019 no modo de autenticação do Active Directory Domain Services, que usará um domínio do AD existente para autenticação.

## <a name="background"></a>Segundo plano

Para habilitar a autenticação do AD (Active Directory), o BDC cria automaticamente os usuários, os grupos, as contas de computadores e os SPNs (nomes da entidade de serviço) de que os diversos serviços do cluster. Para fornecer alguma independência a essas contas e permitir a definição de escopos para as permissões, durante a implantação, indique uma UO (unidade organizacional) em que todos os objetos do AD relacionados ao BDC serão criados. Crie essa UO antes da implantação do cluster.

Para criar automaticamente todos os objetos necessários no Active Directory Domain Services, o BDC precisa de uma conta do AD durante a implantação. Essa conta precisa ter permissões para criar usuários, grupos e contas de computadores dentro da UO fornecida.

As etapas a seguir pressupõem que você já tenha um controlador de domínio do Active Directory Domain Services. Se você não tem um controlador de domínio, o [guia](https://social.technet.microsoft.com/wiki/contents/articles/37528.create-and-configure-active-directory-domain-controller-in-azure-windows-server.aspx) a seguir inclui etapas que podem ser úteis.

## <a name="create-ad-objects"></a>Criar objetos do AD

Faça o seguinte antes de implantar um BDC com a integração do AD:

1. Crie uma UO (unidade organizacional) em que todos os objetos do AD do BDC serão armazenados. Você também pode optar por indicar uma UO existente no momento da implantação.
1. Crie uma conta do AD para o BDC (ou use uma conta existente) e forneça a essa conta do AD do BDC as permissões corretas.

### <a name="create-a-user-in-ad-for-bdc-domain-service-account"></a>Crie um usuário no AD para a conta de serviço de domínio do BDC

O cluster de Big Data requer uma conta com permissões específicas. Antes de prosseguir, verifique se você tem uma conta existente do AD ou crie uma nova conta que o cluster de Big Data possa usar para configurar os objetos necessários.

Para criar um novo usuário no AD, você pode clicar com o botão direito do mouse no domínio ou na UO e selecionar **Novo** > **Usuário**:

![image12](./media/deploy-active-directory/image12.png)

Esse usuário será chamado de *conta de serviço de domínio do BDC* neste artigo.

### <a name="creating-an-ou"></a>Criando uma UO

No controlador de domínio, abra **Usuários e Computadores do Active Directory**. No painel esquerdo, clique com o botão direito do mouse no diretório no qual deseja criar a UO e selecione Novo –\> **Unidade Organizacional** e siga os prompts do assistente para criar a UO. Como alternativa, você pode criar uma UO com o PowerShell:

```powershell
New-ADOrganizationalUnit -Name "<name>" -Path "<Distinguished name of the directory you wish to create the OU in>"
```

Nos exemplos deste artigo, estamos dando à UO o seguinte nome: `bdc`

![image13](./media/deploy-active-directory/image13.png)

![image14](./media/deploy-active-directory/image14.png)

### <a name="setting-permissions-the-bdc-ad-account"></a>Definindo as permissões da conta do AD do BDC

Quer você tenha criado um novo usuário ou esteja usando um usuário existente do AD, há certas permissões que o usuário precisa ter. Essa conta é a conta de usuário que o controlador do BDC usará ao ingressar o cluster no AD.

A DSA (conta de serviço de domínio) do BDC precisa ser capaz de criar usuários, grupos e contas de máquina na UO. Nas etapas a seguir, demos à conta de serviço de domínio do BDC o nome `bdcDSA`. Você pode escolher qualquer nome para a conta.

1. No controlador de domínio, abra **Usuários e Computadores do Active Directory**

1. No painel esquerdo, navegue para seu domínio e, em seguida, para a UO que `bdc` usará

1. Clique com o botão direito do mouse na UO e selecione **Propriedades**.

1. Vá para a guia Segurança (verifique se você selecionou **Recursos Avançados** clicando com o botão direito do mouse na UO e selecionando **Exibir**)

    ![image15](./media/deploy-active-directory/image15.png)

1. Clique em **Adicionar...** e adicione o usuário do **[!INCLUDE[big-data-clusters](../includes/ssbigdataclusters-nover.md)]DSA**

    ![image16](./media/deploy-active-directory/image16.png)

    ![image17](./media/deploy-active-directory/image17.png)

1. Selecione o usuário do **[!INCLUDE[big-data-clusters](../includes/ssbigdataclusters-nover.md)]DSA**, desmarque todas as permissões e clique em **Avançado**

1. Clique em **Adicionar**

    ![image18](./media/deploy-active-directory/image18.png)

    - Clique em **Selecionar uma Entidade de Segurança**, insira **[!INCLUDE[big-data-clusters](../includes/ssbigdataclusters-nover.md)]DSA** e clique em OK

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

    - Clique em **Selecionar uma Entidade de Segurança**, insira **[!INCLUDE[big-data-clusters](../includes/ssbigdataclusters-nover.md)]DSA** e clique em OK

    - Defina o **Tipo** como **Permitir**

    - Defina **Aplica-se a** como **Objetos de computador descendentes**

    - Role até a parte inferior e clique em **Limpar tudo**

    - Role de volta para a parte superior e selecione **Redefinir senha**

    - Clique em **OK**

- Clique em **Adicionar**

    - Clique em **Selecionar uma Entidade de Segurança**, insira **[!INCLUDE[big-data-clusters](../includes/ssbigdataclusters-nover.md)]DSA** e clique em OK

    - Defina o **Tipo** como **Permitir**

    - Defina **Aplica-se a** como **Objetos de usuário descendentes**

    - Role até a parte inferior e clique em **Limpar tudo**

    - Role de volta para a parte superior e selecione **Redefinir senha**

    - Clique em **OK**

- Clique em **OK** mais duas vezes para fechar as caixas de diálogo abertas

## <a name="prepare-deployment"></a>Preparar a implantação

Para a implantação do BDC com a integração com o AD, algumas informações adicionais precisam ser fornecidas para a criação de objetos relacionados ao BDC no AD.

Usando o perfil `kubeadm-prod`, você terá automaticamente os espaços reservados para as informações relacionadas à segurança e ao ponto de extremidade que são necessárias para a integração com o AD.

Além disso, você precisa fornecer credenciais que o [!INCLUDE[big-data-clusters](../includes/ssbigdataclusters-nover.md)] usará para criar os objetos necessários no AD. Essas credenciais são fornecidas como variáveis de ambiente.

## <a name="set-security-environment-variables"></a>Definir variáveis de ambiente de segurança

As variáveis de ambiente a seguir estão fornecendo as credenciais para a conta de serviço de domínio do BDC, que serão usadas para configurar a integração com o AD. Essa conta também é usada pelo BDC para manter os objetos do AD relacionados ao BDC no futuro.

```bash
export DOMAIN_SERVICE_ACCOUNT_USERNAME=<AD principal account name>
export DOMAIN_SERVICE_ACCOUNT_PASSWORD=<AD principal password>
```

## <a name="provide-security-and-endpoint-parameters"></a>Fornecer parâmetros de segurança e ponto de extremidade

Além das variáveis de ambiente para as credenciais, você também precisa fornecer informações de segurança e de ponto de extremidade para que a integração com o AD funcione. Os parâmetros necessários fazem parte automaticamente do `kubeadm-prod` [perfil de implantação](deployment-guidance.md#configfile).

A integração com o AD requer os seguintes parâmetros. Adicione esses parâmetros aos arquivos `control.json` e `bdc.json` usando os comandos `config replace` mostrados mais adiante neste artigo. Todos os exemplos a seguir estão usando o domínio de exemplo `contoso.local`.

- `security.activeDirectory.ouDistinguishedName`: nome diferenciado de uma UO (unidade organizacional) a que todas as contas do AD criadas pela implantação do cluster serão adicionadas. Se o nome do domínio for `contoso.local`, o nome diferenciado da UO será `OU=BDC,DC=contoso,DC=local`.

- `security.activeDirectory.dnsIpAddresses`: lista de endereços IP dos controladores de domínio

- `security.activeDirectory.domainControllerFullyQualifiedDns`: lista de FQDNs do controlador de domínio. O FQDN contém o nome do computador/host do controlador de domínio. Se tiver vários controladores de domínio, você poderá fornecer uma lista aqui. Exemplo: `HOSTNAME.CONTOSO.LOCAL`

- **Parâmetro opcional** `security.activeDirectory.realm`: na maioria dos casos, o realm é igual ao nome de domínio. Para casos em que eles não são iguais, use esse parâmetro para definir o nome do realm (por exemplo, `CONTOSO.LOCAL`).

- `security.activeDirectory.domainDnsName`: nome do seu domínio (por exemplo, `contoso.local`).

- `security.activeDirectory.clusterAdmins`: esse parâmetro usa **um grupo do AD**. Os membros desse grupo receberão permissões de administrador no cluster. Isso significa que eles terão permissões de sysadmin no SQL Server, permissões de superusuário no HDFS e permissões de administrador no controlador. **Observe que esse grupo precisa existir no AD antes do início da implantação. Observe também que esse grupo não pode estar no escopo DomainLocal no Active Directory. Um grupo com escopo no domínio local resultará em falha na implantação.**

- `security.activeDirectory.clusterUsers`: lista dos grupos do AD que são usuários comuns (sem permissões de administrador) no cluster de Big Data. **Observe que esses grupos precisam existir no AD antes do início da implantação. Observe também que esses grupos não pode estar no escopo DomainLocal no Active Directory. Um grupo com escopo no domínio local resultará em falha na implantação.**

- **Parâmetro opcional** `security.activeDirectory.appOwners`: lista dos grupos do AD que têm permissões para criar, excluir e executar qualquer aplicativo. **Observe que esses grupos precisam existir no AD antes do início da implantação. Observe também que esses grupos não pode estar no escopo DomainLocal no Active Directory. Um grupo com escopo no domínio local resultará em falha na implantação.**

- **Parâmetro opcional** `security.activeDirectory.appReaders`: lista dos grupos do AD que têm permissões para executar qualquer aplicativo. **Observe que esses grupos precisam existir no AD antes do início da implantação. Observe também que esses grupos não pode estar no escopo DomainLocal no Active Directory. Um grupo com escopo no domínio local resultará em falha na implantação.**

**Como verificar o escopo do grupo do AD:** 
[clique aqui para obter instruções](https://docs.microsoft.com/powershell/module/activedirectory/get-adgroup?view=winserver2012-ps&viewFallbackFrom=winserver2012r2-ps) para verificar o escopo de um grupo do AD e determinar se ele é DomainLocal.

Se ainda não tiver inicializado o arquivo de configuração de implantação, você poderá executar esse comando para obter uma cópia da configuração.

```bash
azdata bdc config init --source kubeadm-prod  --target custom-prod-kubeadm
```

Para definir os parâmetros acima no arquivo `control.json`, use os comandos `azdata` a seguir. Os comandos substituem a configuração e fornecem seus próprios valores antes da implantação.

 > [!IMPORTANT]
 > Na versão SQL Server 2019 CU2, a estrutura da seção de configuração de segurança no perfil de implantação mudou de maneira clara e todas as configurações relacionadas ao Active Directory estão no novo *activeDirectory* na árvore json em *security* no arquivo *control.json*.

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

Além das informações acima, você também precisa fornecer nomes DNS para os diferentes pontos de extremidade do cluster. As entradas DNS que usam os nomes DNS fornecidos por você serão criadas automaticamente no servidor DNS após a implantação. Você usará esses nomes ao se conectar aos diferentes pontos de extremidade do cluster. Por exemplo, se o nome DNS da instância mestre do SQL for `mastersql`, você usará `mastersql.contoso.local,31433` para se conectar à instância mestre por meio das ferramentas.

> [!NOTE]
> Certifique-se de criar entradas DNS no servidor DNS para os nomes que você está definindo abaixo. Para implantações de `kubeadm`, você pode, por exemplo, usar o endereço IP do nó mestre do Kubernetes ao criar as entradas DNS.

```bash
# DNS names for BDC services
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.spec.endpoints[0].dnsName=<controller DNS name>.contoso.local"
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.spec.endpoints[1].dnsName=<monitoring services DNS name>.<Domain name. e.g. contoso.local>"
azdata bdc config replace -c custom-prod-kubeadm/bdc.json -j "$.spec.resources.master.spec.endpoints[0].dnsName=<SQL Master Primary DNS name>.<Domain name. e.g. contoso.local>"
azdata bdc config replace -c custom-prod-kubeadm/bdc.json -j "$.spec.resources.master.spec.endpoints[1].dnsName=<SQL Master Secondary DNS name>.<Domain name. e.g. contoso.local>"
azdata bdc config replace -c custom-prod-kubeadm/bdc.json -j "$.spec.resources.gateway.spec.endpoints[0].dnsName=<Gateway (Knox) DNS name>.<Domain name. e.g. contoso.local>"
azdata bdc config replace -c custom-prod-kubeadm/bdc.json -j "$.spec.resources.appproxy.spec.endpoints[0].dnsName=<app proxy DNS name>.<Domain name. e.g. contoso.local>"
```

Você pode encontrar aqui um script de exemplo para [implantar um cluster de Big Data do SQL Server no cluster do Kubernetes de nó único (kubeadm) com a integração com o AD](https://github.com/microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/deployment/kubeadm/ubuntu-single-node-vm-ad).

Agora, você precisa definir todos os parâmetros necessários para uma implantação do BDC com a integração do Active Directory.

Para obter a documentação completa sobre como implantar [!INCLUDE[big-data-clusters](../includes/ssbigdataclusters-nover.md)], visite a [documentação oficial](deployment-guidance.md).

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

Você pode se conectar ao ponto de extremidade do controlador usando `azdata` e a autenticação do AD.

```bash
kinit <username>@<domain name>
azdata login -e https://<controller DNS name>:30080 --auth ad
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

**Limitações a serem consideradas nesta versão:**

- atualmente, o Painel de Pesquisa de Logs e o Painel de Métricas não dão suporte à autenticação do AD. O suporte do AD para esse ponto de extremidade está planejado para uma versão futura. O nome de usuário e a senha básicos definidos na implantação podem ser usados para autenticação nesses painéis. Todos os outros pontos de extremidade do cluster dão suporte à autenticação do AD.

- No momento, o modo de segurança do AD só funciona em ambientes de implantação do `kubeadm`, e não no AKS. O perfil de implantação do `kubeadm-prod` inclui as seções de segurança por padrão.

- Somente um BDC por domínio (Active Directory) é permitido no momento. A habilitação de vários BDCs por domínio está planejada para uma versão futura.

- Nenhum dos grupos do AD especificados nas configurações de segurança pode estar com escopo DomainLocal. Para verificar o escopo de um grupo do AD, siga [estas instruções](https://docs.microsoft.com/powershell/module/activedirectory/get-adgroup?view=winserver2012-ps&viewFallbackFrom=winserver2012r2-ps).
