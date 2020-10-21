---
title: Suporte do Scale Out para alta disponibilidade | Microsoft Docs
description: Saiba como configurar o lado do SSIS (SQL Server Integration Services) Scale Out Master para alta disponibilidade.
ms.custom: performance
ms.date: 05/23/2018
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
author: haoqian
ms.author: haoqian
ms.openlocfilehash: 19db6aeab39dc93c2dcfd6a869d3b54e0a1ceaa6
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/19/2020
ms.locfileid: "92192447"
---
# <a name="scale-out-support-for-high-availability"></a>Suporte do Scale Out para alta disponibilidade

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]



No SSIS Scale Out, a alta disponibilidade do lado do Trabalho do Scale Out é fornecida com a execução de pacotes com vários Trabalhos do Scale Out.

No lado do Mestre do Scale Out, a alta disponibilidade é obtida com o [Always On para o Catálogo do SSIS](../catalog/ssis-catalog.md#always-on-for-ssis-catalog-ssisdb) e o clustering de failover do Windows. Nesta solução, várias instâncias de Mestre do Scale Out são hospedadas em um cluster de failover do Windows. Quando o serviço Mestre do Scale Out ou o SSISDB está inativo no nó primário, o serviço ou o SSISDB no nó secundário continua aceitando as solicitações do usuário e se comunicando com os Trabalhos do Scale Out.

Como alternativa, a alta disponibilidade no lado do Mestre do Scale Out pode ser obtida com a instância de cluster de failover do SQL Server. Consulte [Suporte do Scale Out para alta disponibilidade por meio da instância de cluster de failover do SQL Server](scale-out-failover-cluster-instance.md).

Para configurar a alta disponibilidade no lado do Mestre do Scale Out com o Always On para o catálogo do SSIS, siga estas etapas:

## <a name="1-prerequisites"></a>1. Pré-requisitos
Configurar um cluster de failover do Windows. Confira a postagem no blog [Instalando o recurso Cluster de Failover e as Ferramentas para o Windows Server 2012](https://techcommunity.microsoft.com/t5/failover-clustering/installing-the-failover-cluster-feature-and-tools-in-windows/ba-p/371733) para obter instruções. Instale o recurso e as ferramentas em todos os nós de cluster.

## <a name="2-install-scale-out-master-on-the-primary-node"></a>2. Instalar o Mestre do Scale Out no nó primário
Instale os Serviços de Mecanismo de Banco de Dados do SQL Server, o Integration Services e o Mestre do Scale Out no nó primário do Mestre do Scale Out. 

Durante a instalação, faça o seguinte:

### <a name="21-set-the-account-running-scale-out-master-service-to-a-domain-account"></a>2.1 Defina a conta que executa o serviço Mestre do Scale Out com uma conta de domínio
Essa conta deve poder acessar o SSISDB no nó secundário no cluster de failover do Windows no futuro. Já que o serviço Mestre do Scale Out e o SSISDB podem fazer failover separadamente, eles podem não estar no mesmo nó após o failover.

![Configuração do servidor de alta disponibilidade](media/ha-server-config.PNG)

### <a name="22-include-the-dns-host-name-for-the-scale-out-master-service-in-the-cns-of-the-scale-out-master-certificate"></a>2.2 Inclua o nome do host DNS do serviço Mestre do Scale Out nos CNs do certificado do Mestre do Scale Out

Esse nome de host é o ponto de extremidade Mestre do Scale Out, que é criado como um Serviço Genérico em cluster no cluster de failover (veja a etapa 7).   (Certifique-se de fornecer um nome do host DNS, e não um nome do servidor).

![Configuração do mestre de alta disponibilidade](media/ha-master-config.PNG)

## <a name="3-install-scale-out-master-on-the-secondary-node"></a>3. Instalar o Mestre do Scale Out no nó secundário
Instale os Serviços de Mecanismo de Banco de Dados do SQL Server, o Integration Services e o Mestre do Scale Out no nó secundário do Mestre do Scale Out. 

Use o mesmo certificado do Mestre do Scale Out usado no nó primário. Exporte o certificado TLS/SSL do Mestre do Scale Out no nó primário com uma chave privada e instale-o no repositório de certificados Raiz do computador local no nó secundário. Selecione esse certificado durante a instalação do Mestre do Scale Out no nó secundário.

![Configuração do mestre de alta disponibilidade 2](media/ha-master-config2.PNG)

> [!NOTE]
> Configure vários Mestres do Scale Out de backup repetindo essas operações para o Mestre do Scale Out nos outros nós secundários.

## <a name="4-set-up-and-configure-ssisdb-support-for-always-on"></a>4. Configurar o suporte ao SSISDB para Always On

Siga as instruções para configurar o suporte ao SSISDB para Always On em [Always On para o Catálogo do SSIS (SSISDB)](../catalog/ssis-catalog.md#always-on-for-ssis-catalog-ssisdb).

Além disso, é necessário criar um ouvinte do grupo de disponibilidade para o grupo de disponibilidade ao qual o SSISDB será adicionado. Consulte [Criar ou configurar um ouvinte de grupo de disponibilidade](../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md).

## <a name="5-update-the-scale-out-master-service-configuration-file"></a>5. Atualizar o arquivo de configuração de serviço do Mestre do Scale Out
Atualize o arquivo de configuração de serviço do Mestre do Scale Out, `\<drive\>:\Program Files\Microsoft SQL Server\140\DTS\Binn\MasterSettings.config`, nos nós primários e secundários. Atualize **SqlServerName** para *[Nome DNS do Ouvinte do Grupo de Disponibilidade],[Porta]* .

## <a name="6-enable-package-execution-logging"></a>6. Habilitar log de execução de pacote

O log no SSISDB é feito pelo logon **##MS_SSISLogDBWorkerAgentLogin##** , cuja senha é gerada automaticamente. Para fazer com que o log funcione em todas as réplicas do SSISDB, faça o seguinte

### <a name="61-change-the-password-of-ms_ssislogdbworkeragentlogin-on-the-primary-sql-server"></a>6.1 Altere a senha de **##MS_SSISLogDBWorkerAgentLogin##** no SQL Server primário

### <a name="62-add-the-login-to-the-secondary-sql-server"></a>6.2 Adicione o logon ao SQL Server secundário

### <a name="63-update-the-connection-string-used-for-logging"></a>6.3 Atualize a cadeia de conexão usada para o log.
Chame o procedimento armazenado `[catalog].[update_logdb_info]` com os seguintes valores de parâmetro:

-   `@server_name = '[Availability Group Listener DNS name],[Port]'`

-   `@connection_string = 'Data Source=[Availability Group Listener DNS name],[Port];Initial Catalog=SSISDB;User Id=##MS_SSISLogDBWorkerAgentLogin##;Password=[Password]];'`

## <a name="7-configure-the-scale-out-master-service-role-of-the-windows-server-failover-cluster"></a>7. Configure a função de serviço Mestre de Expansão do cluster de failover do Windows Server

1.  No Gerenciador de Cluster de Failover, conecte-se ao cluster do Scale Out. Selecione o cluster. Selecione **Ação** no menu e, em seguida, selecione **Configurar Função**.

2.  Na caixa de diálogo **Assistente para Alta Disponibilidade**, selecione **Serviço Genérico** na página **Selecionar Função**. Selecione o Mestre do SQL Server Integration Services Scale Out 14.0 na página **Selecionar Serviço**.

3.  Na página **Ponto de Acesso para Cliente**, insira o nome do host DNS do serviço Mestre do Scale Out.

    ![Assistente de Alta Disponibilidade 1](media/ha-wizard1.PNG)

4.  Conclua o assistente.

Em máquinas virtuais do Azure, essa etapa de configuração requer etapas adicionais. Uma explicação completa desses conceitos e dessas etapas está fora do escopo deste artigo.

1.  É necessário configurar um domínio do Azure. O Clustering de failover do Windows Server requer que todos os computadores no cluster sejam membros do mesmo domínio. Para obter mais informações, consulte [Enable Azure Active Directory Domain Services using the Azure portal](/azure/active-directory-domain-services/create-instance) (Habilitar o Azure Active Directory Domain Services usando o portal do Azure).

2. É necessário configurar um balanceador de carga do Azure. Esse é um requisito para o ouvinte do grupo de disponibilidade. Para obter mais informações, confira [Tutorial: balancear o tráfego interno de carga com o balanceador de carga básico para VMs usando o portal do Azure](/azure/load-balancer/tutorial-load-balancer-basic-internal-portal).

## <a name="8-update-the-scale-out-master-address-in-ssisdb"></a>8. Atualizar o endereço do Mestre do Scale Out no SSISDB

No SQL Server primário, execute o procedimento armazenado `[catalog].[update_master_address]` com o valor de parâmetro `@MasterAddress = N'https://[Scale Out Master service DNS host name]:[Master Port]'`. 

## <a name="9-add-the-scale-out-workers"></a>9. Adicionar os Trabalhos do Scale Out

Agora, você pode adicionar Trabalhos do Scale Out com a ajuda do [Gerenciador do Integration Services Scale Out](integration-services-ssis-scale-out-manager.md). Insira `[SQL Server Availability Group Listener DNS name],[Port]` na página de conexão.

## <a name="upgrade-scale-out-in-high-availability-environment"></a>Atualizar o Scale Out em um ambiente de alta disponibilidade
Para atualizar o Scale Out em um ambiente de alta disponibilidade, execute as [etapas de atualização do Always On para catálogo do SSIS](../catalog/ssis-catalog.md#Upgrade), atualize o Mestre do Scale Out e Trabalho do Scale Out em cada máquina e recrie a função do cluster de failover do Windows Server na etapa 7 acima com a nova versão do serviço Mestre do Scale Out.

## <a name="next-steps"></a>Próximas etapas
Para obter mais informações, confira os seguintes artigos:
-   [Mestre do SSIS (Integration Services) Scale Out](integration-services-ssis-scale-out-master.md)
-   [Trabalho do SSIS (Integration Services) Scale Out](integration-services-ssis-scale-out-worker.md)