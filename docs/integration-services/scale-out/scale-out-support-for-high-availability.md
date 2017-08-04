---
title: "SQL Server Integration Services (SSIS) expansão Support for High Availability | Microsoft Docs"
ms.custom: 
ms.date: 07/18/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
caps.latest.revision: 1
author: haoqian
ms.author: haoqian
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 2405235bcfa09d2cc49e007f4eae6975d9ebf7a5
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="scale-out-support-for-high-availability"></a>Suporte de expansão para alta disponibilidade

No SSIS expansão, do lado do trabalho de alta disponibilidade é fornecida por meio de pacotes com vários escala Out trabalhadores em execução.
No lado do mestre de alta disponibilidade é obtida com [sempre no catálogo do SSIS](../service/ssis-catalog.md#always-on-for-ssis-catalog-ssisdb) e o cluster de failover do Windows. Várias instâncias de escala Out mestre são hospedadas em um cluster de failover do Windows. Quando o serviço de escala Out mestre ou o SSISDB está inativo no nó primário, o serviço ou SSISDB no nó secundário continuará aceitar solicitações do usuário e se comunicar com operadores fora de escala. 

Para configurar a alta disponibilidade do lado do mestre, siga as etapas abaixo.

## <a name="1-prerequisites"></a>1. Pré-requisitos
Configurar um cluster de failover do Windows. Confira a postagem do blog [Installing the Failover Cluster Feature and Tools for Windows Server 2012](http://blogs.msdn.com/b/clustering/archive/2012/04/06/10291601.aspx) (Instalando o recurso Cluster de Failover e as Ferramentas para o Windows Server 2012) para obter instruções. Você deve instalar o recurso e as ferramentas em todos os nós de cluster.

## <a name="2-install-scale-out-master-on-primary-node"></a>2. Instalar escala Out mestre no nó primário
Instale serviços de mecanismo de banco de dados, serviços de integração e escala Out mestre no nó primário para escala Out mestre. 

Durante a instalação, você deve: 
### <a name="21-set-the-account-running-scale-out-master-service-to-a-domain-account"></a>2.1 Defina a conta que executa o serviço de escala Out mestre para uma conta de domínio.
Essa conta deve ser capaz de acessar SSISDB no nó secundário no cluster de failover do Windows no futuro. Como serviço de escala Out mestre e SSISDB separadamente de failover, eles podem não estar no mesmo nó.

![Configuração do servidor de alta disponibilidade](media/ha-server-config.PNG)

### <a name="22-include-scale-out-master-service-dns-host-name-in-the-cns-of-scale-out-master-certificate"></a>2.2 incluem escala Out mestre serviço nome de host DNS no certificado CNs de escala Out mestre.

Esse nome de host será usado no ponto de extremidade de escala Out mestre. 

![Configuração de HA mestre](media/ha-master-config.PNG)

## <a name="3-install-scale-out-master-on-secondary-node"></a>3. Instalar escala Out mestre no nó secundário
Instale serviços de mecanismo de banco de dados, serviços de integração e escala Out mestre no nó secundário para escala Out mestre. 

Você deve usar o mesmo certificado de escala Out mestre com o nó primário. Exportar o certificado SSL de escala Out mestre no nó primário com chave privada e instalá-lo ao repositório de certificados raiz da máquina loacl no nó secundário. Selecione este certificado durante a instalação mestre fora de escala.

![Configuração HA mestre 2](media/ha-master-config2.PNG)

> [!Note]
> Você pode definir o backup de vários mestres fora de escala, repetindo as operações de escala secundária Out mestre.

## <a name="4-set-up-ssisdb-always-on"></a>4. Configurar o SSISDB sempre no

As instruções para configurar o sempre em para SSISDB pode ser visto no [sempre ligado para catálogo do SSIS (SSISDB)](../service/ssis-catalog.md#always-on-for-ssis-catalog-ssisdb).

Além disso, você precisa criar um ouvinte de gourp de disponibilidade para o grupo de disponibilidade do que SSISDB é adicionado ao. Consulte [criar ou configurar um ouvinte de grupo de disponibilidade](../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md).

## <a name="5-update-scale-out-master-service-configuration-file"></a>5. Atualizar o arquivo de configuração do serviço de escala Out mestre
Arquivo de configuração de serviço de escala Out mestre de atualização, \<driver\>: \Program Files\Microsoft Server\140\DTS\Binn\MasterSettings.config SQL, em nós primários e secundários. Atualização **SqlServerName** para *[nome do DNS do ouvinte de grupo de disponibilidade], [porta]*.

## <a name="6-enable-package-execution-logging"></a>6. Habilitar log de execução do pacote

Registro em log no SSISDB é feito pelo logon **MS_SSISLogDBWorkerAgentLogin # # # #**, cuja senha é gerado automaticamente. Para fazer log funciona para todas as réplicas do SSISDB, faça o seguinte.

### <a name="61-change-the-password-of-msssislogdbworkeragentlogin-on-primary-sql-server"></a>6.1 alterar a senha de **MS_SSISLogDBWorkerAgentLogin # # # #** no Sql Server primário.
### <a name="62-add-the-login-to-secondary-sql-server"></a>6.2 Adicione o logon para o Sql Server secundário.
### <a name="63-update-connection-string-of-logging"></a>6.3 Atualize a cadeia de caracteres de conexão do log.
Chame o procedimento armazenado [catalog]. [update_logdb_info] com 

@server_name= '*[Nome do DNS do ouvinte de grupo de disponibilidade], [porta]*' 

e @connection_string = ' Data Source =*[nome do DNS do ouvinte de grupo de disponibilidade]*,*[Port]*; Initial Catalog = SSISDB; Id de usuário = # # MS_SSISLogDBWorkerAgentLogin # #; Senha =*[senha]*];'.

## <a name="7-congifure-scale-out-master-service-role-of-windows-failover-cluster"></a>7. Função de serviço Congifure escala Out mestre de cluster de failover do Windows

Gerenciador de cluster de failover, conecte-se ao cluster para expansão. Selecione o cluster e clique em **ação** no menu e, em seguida, **configurar função...** .

Na ser exibido para cima **Assistente para alta disponibilidade**, selecione **serviço genérico** em **Selecionar função** página e selecione SQL Server Integration Services escala Out mestre 14.0 no **Selecionar serviço** página.

No **ponto de acesso para cliente** , insira o nome de host do DNS de serviço escala Out mestre.

![HA assistente 1](media/ha-wizard1.PNG)

Conclua o assistente.

## <a name="8-update-master-address-in-ssisdb"></a>8. Atualizar mestre endereço no SSISDB

No SQL Server primário, execute o procedimento armazenado [SSIS]. [catalog]. [update_master_address] com o parâmetro @MasterAddress = N'https: / / [nome do host DNS do serviço de escala Out mestre]: [porta mestre]'. 

## <a name="9-add-scale-out-worker"></a>9. Adicionar o trabalho de expansão

Agora, você pode adicionar operadores fora de escala com a Ajuda de [gerenciador fora de escala](integration-services-ssis-scale-out-manager.md). Digite *[nome do DNS de ouvinte de grupo de disponibilidade do SQL Server]*,*[Port]* na página de conexão.





