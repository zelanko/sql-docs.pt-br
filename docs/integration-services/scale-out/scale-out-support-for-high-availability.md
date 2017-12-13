---
title: Suporte do Scale Out para Alta Disponibilidade do SSIS (SQL Server Integration Services) | Microsoft Docs
ms.custom: 
ms.date: 07/18/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: scale-out
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
caps.latest.revision: "1"
author: haoqian
ms.author: haoqian
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2202b61a9efce26edb0edcef53204351338ecee6
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="scale-out-support-for-high-availability"></a>Suporte do Scale Out para alta disponibilidade

No SSIS Scale Out, a alta disponibilidade do lado do trabalho é fornecida por meio de pacotes com vários Trabalhos do Scale Out em execução.
No lado do mestre, a alta disponibilidade é obtida com [Always On para Catálogo do SSIS](../service/ssis-catalog.md#always-on-for-ssis-catalog-ssisdb) e o cluster de failover do Windows. Várias instâncias de Mestre do Scale Out são hospedadas em um cluster de failover do Windows. Quando o serviço Mestre do Scale Out ou o SSISDB está inativo no nó primário, o serviço ou SSISDB no nó secundário continuará a aceitar solicitações do usuário e se comunicar com Trabalhos do Scale Out. 

Para configurar a alta disponibilidade do lado do mestre, siga as etapas abaixo.

## <a name="1-prerequisites"></a>1. Pré-requisitos
Configurar um cluster de failover do Windows. Confira a postagem do blog [Installing the Failover Cluster Feature and Tools for Windows Server 2012](http://blogs.msdn.com/b/clustering/archive/2012/04/06/10291601.aspx) (Instalando o recurso Cluster de Failover e as Ferramentas para o Windows Server 2012) para obter instruções. Você deve instalar o recurso e as ferramentas em todos os nós de cluster.

## <a name="2-install-scale-out-master-on-primary-node"></a>2. Instalar o Mestre do Scale Out no nó primário
Instale serviços de Mecanismo de Banco de Dados, Integration Services e Mestre do Scale Out no nó primário para o Mestre do Scale Out. 

Durante a instalação, você deve 
### <a name="21-set-the-account-running-scale-out-master-service-to-a-domain-account"></a>2.1 Defina a conta que executa o serviço Mestre do Scale Out para uma conta de domínio.
Essa conta deve ser capaz de acessar o SSISDB no nó secundário no cluster de failover do Windows no futuro. Já que o serviço de Mestre do Scale Out e SSISDB podem fazer failover separadamente, eles podem não estar no mesmo nó.

![Configuração do servidor de alta disponibilidade](media/ha-server-config.PNG)

### <a name="22-include-scale-out-master-service-dns-host-name-in-the-cns-of-scale-out-master-certificate"></a>2.2 Inclua o nome do host DNS do serviço Mestre do Scale Out nos CNs do certificado do Mestre do Scale Out.

Esse nome do host será usado no ponto de extremidade do Mestre do Scale Out. 

![Configuração do mestre de alta disponibilidade](media/ha-master-config.PNG)

## <a name="3-install-scale-out-master-on-secondary-node"></a>3. Instalar o Mestre do Scale Out no nó secundário
Instale serviços de Mecanismo de Banco de Dados, Integration Services e Mestre do Scale Out no nó secundário para o Mestre do Scale Out. 

Você deve usar o mesmo certificado do Mestre do Scale Out com o nó primário. Exportar o certificado SSL do Mestre do Scale Out no nó primário com chave privada e instalá-lo ao repositório de certificados raiz do computador local no nó secundário. Selecione este certificado durante a instalação do Mestre do Scale Out.

![Configuração do mestre de alta disponibilidade 2](media/ha-master-config2.PNG)

> [!Note]
> Você pode configurar vários Mestres do Scale Out de backup repetindo as operações realizadas para o Mestre do Scale Out secundário.

## <a name="4-set-up-ssisdb-always-on"></a>4. Configurar o SSISDB Always On

As instruções para configurar o Always On para o SSISDB podem ser vistas no [Always On para o SSISDB (Catálogo do SSIS)](../service/ssis-catalog.md#always-on-for-ssis-catalog-ssisdb).

Além disso, você precisa criar um ouvinte de grupo de disponibilidade para o grupo de disponibilidade no qual o SSISDB é adicionado. Consulte [Criar ou configurar um ouvinte de grupo de disponibilidade](../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md).

## <a name="5-update-scale-out-master-service-configuration-file"></a>5. Atualizar o arquivo de configuração de serviço do Mestre de Scale Out
Atualize o arquivo de configuração de serviço Mestre do Scale Out, \<unidade\>:\Program Files\Microsoft SQL Server\140\DTS\Binn\MasterSettings.config, nos nós primário e secundário. Atualize **SqlServerName** para *[nome DNS do ouvinte de grupo de disponibilidade],[porta]*.

## <a name="6-enable-package-execution-logging"></a>6. Habilitar log de execução de pacote

O registro em log no SSISDB é feito pelo logon **##MS_SSISLogDBWorkerAgentLogin##**, cuja senha é gerada automaticamente. Para fazer trabalhos de log para todas as réplicas do SSISDB, faça o descrito a seguir.

### <a name="61-change-the-password-of-msssislogdbworkeragentlogin-on-primary-sql-server"></a>6.1 Altere a senha de **##MS_SSISLogDBWorkerAgentLogin##** no SQL Server primário.
### <a name="62-add-the-login-to-secondary-sql-server"></a>6.2 Adicione o logon para o SQL Server secundário.
### <a name="63-update-connection-string-of-logging"></a>6.3 Atualize a cadeia de conexão do registro em log.
Chame o procedimento armazenado [catalog].[update_logdb_info] com 

@server_name = '*[Nome DNS do ouvinte de grupo de disponibilidade],[Porta]*' 

e @connection_string = 'Data Source=*[Nome DNS do ouvinte de grupo de disponibilidade]*,*[Porta]*;Initial Catalog=SSISDB;User Id=##MS_SSISLogDBWorkerAgentLogin##;Password=*[Senha]*];'.

## <a name="7-congifure-scale-out-master-service-role-of-windows-failover-cluster"></a>7. Configure a função de serviço do Mestre do Scale Out do cluster de failover do Windows

No Gerenciador de Cluster de Failover, conecte-se ao cluster para o Scale Out. Selecione o cluster e clique em **Ação** no menu e depois em **Configurar Função...**.

No **Assistente Para Alta Disponibilidade** mostrado, selecione **Serviço Genérico** na página **Selecionar Função** e escolha Mestre do SQL Server Integration Services Scale Out 14.0 na página **Selecionar Serviço**.

Na página **Ponto de Acesso para Cliente**, insira o nome de host do DNS do serviço Mestre do Scale Out.

![Assistente de Alta Disponibilidade 1](media/ha-wizard1.PNG)

Conclua o assistente.

## <a name="8-update-master-address-in-ssisdb"></a>8. Atualizar o endereço do Mestre no SSISDB

No SQL Server primário, execute o procedimento armazenado [SSIS].[catalog].[update_master_address] com o parâmetro @MasterAddress = N'https://[Nome do host DNS do serviço Mestre do Scale Out]:[Porta do Mestre]'. 

## <a name="9-add-scale-out-worker"></a>9. Adicionar Trabalho do Scale Out

Agora, você pode adicionar Trabalhos do Scale Out com a ajuda do [Gerenciador do Scale Out](integration-services-ssis-scale-out-manager.md). Digite *[Nome DNS do ouvinte de grupo de disponibilidade do SQL Server]*,*[Porta]* na página de conexão.




