---
title: Suporte do SSIS (SQL Server Integration Services) Scale Out para alta disponibilidade por meio da instância de cluster de failover do SQL Server | Microsoft Docs
description: Este artigo descreve como configurar o SSIS Scale Out para alta disponibilidade com a instância de cluster de failover do SQL Server
ms.custom: performance
ms.date: 04/10/2018
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
author: haoqian
ms.author: haoqian
ms.openlocfilehash: 5c4d5cc303d297a21b730abc30e10b85c65cc3d2
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "68811202"
---
# <a name="scale-out-support-for-high-availability-via-sql-server-failover-cluster-instance"></a>Suporte do Scale Out para alta disponibilidade por meio da instância de cluster de failover do SQL Server

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



Para configurar a alta disponibilidade do lado do Mestre do Scale Out com a instância de cluster de failover do SQL Server, siga estas etapas:

## <a name="1-prerequisites"></a>1. Prerequisites
Configurar um cluster de failover do Windows. Confira a postagem no blog [Instalando o recurso Cluster de Failover e as Ferramentas para o Windows Server 2012](https://blogs.msdn.com/b/clustering/archive/2012/04/06/10291601.aspx) para obter instruções. Instale o recurso e as ferramentas em todos os nós de cluster.

## <a name="2-install-sql-server-failover-cluster"></a>2. Instalar um cluster de failover do SQL Server
Instale um cluster de failover do SQL Server. Consulte [Instalação do cluster de failover do SQL Server](../../sql-server/failover-clusters/install/sql-server-failover-cluster-installation.md) para obter instruções. Durante a instalação, selecione Serviços de Mecanismo de Banco de Dados na página Seleção de Recursos. Registre em log o nome da rede do SQL Server para configuração futura.

![Nome da rede do SQL](media/sql-network-name.PNG)

Adicione um nó secundário ao cluster de failover do SQL Server.

## <a name="3-install-scale-out-master-on-the-primary-node"></a>3. Instalar o Mestre do Scale Out no nó primário
Instale o Integration Services e o Mestre do Scale Out no nó primário com o assistente de instalação para a instalação não clusterizada. 

Durante a instalação, inclua o nome da rede do SQL Server nos CNs do certificado do Mestre do Scale Out.

> [!NOTE]
> Se desejar fazer failover do SSISDB e do serviço Mestre do Scale Out separadamente, siga [2. Instale o Mestre do Scale Out no nó primário](scale-out-support-for-high-availability.md#2-install-scale-out-master-on-the-primary-node) para a configuração do Mestre do Scale Out.

## <a name="4-install-scale-out-master-on-the-secondary-node"></a>4. Instalar o Mestre do Scale Out no nó secundário
Siga [3. Instalar o Mestre do Scale Out no nó secundário](scale-out-support-for-high-availability.md#3-install-scale-out-master-on-the-secondary-node)

## <a name="5-update-the-scale-out-master-service-configuration-file"></a>5. Atualizar o arquivo de configuração de serviço do Mestre do Scale Out
Atualize o arquivo de configuração de serviço do Mestre do Scale Out, \<drive\>:\Program Files\Microsoft SQL Server\140\DTS\Binn\MasterSettings.config, nos nós primário e secundário. Atualize **SqlServerName** para [SQL Server network name]//[Instance name] ou [SQL Server network name] para a instância padrão.

## <a name="6-add-scale-out-master-service-to-sql-server-role-in-windows-failover-cluster"></a>6. Adicionar um serviço Mestre do Scale Out à função do SQL Server no cluster de failover do Windows
No Gerenciador de Cluster de Failover, conecte-se ao cluster do Scale Out. Selecione Funções no gerenciador, clique com o botão direito do mouse na função do SQL Server e selecione Adicionar Recurso, Serviço Genérico. 

![Serviço genérico](media/generic-service.PNG)

No Assistente para Novo Recurso, selecione o serviço Mestre do Scale Out e conclua o assistente. 

Coloque o serviço Mestre do Scale Out online.

![Colocar online](media/bring-online.PNG)

> [!NOTE]
> Se desejar fazer failover do SSISDB e do serviço Mestre do Scale Out separadamente, siga [7. Configurar a função de serviço Mestre do Scale Out do cluster de failover do Windows](scale-out-support-for-high-availability.md#7-configure-the-scale-out-master-service-role-of-the-windows-server-failover-cluster)

## <a name="7-install-scale-out-workers"></a>7. Instalar Trabalhos do Scale Out
Instale o Trabalho do Scale Out nos nós de trabalho. Durante a instalação, especifique https://[Sql Server network name]:[master port] para o ponto de extremidade mestre. 

> [!NOTE]
> Se desejar fazer failover do SSISDB e do serviço Mestre do Scale Out separadamente, especifique o nome do host DNS do serviço Mestre do Scale Out em vez do nome da rede do SQL Server.

## <a name="8-install-scale-out-worker-client-certificate"></a>8. Instalar o certificado do cliente do Trabalho do Scale Out
Instale o certificado do trabalho em todos os nós no cluster de failover do SQL Server. Consulte [Instalar certificado do cliente do Trabalho do Scale Out](walkthrough-set-up-integration-services-scale-out.md#InstallCert).

> [!NOTE]
> O Gerenciador do Scale Out não dá suporte ao cluster de failover do SQL Server. Se você usar o Gerenciador do Scale Out para adicionar o Trabalho do Scale Out, você ainda precisará instalar o certificado do trabalho em todos os nós mestres manualmente.

## <a name="next-steps"></a>Próximas etapas
Para obter mais informações, confira os seguintes artigos:
-   [Mestre do SSIS (Integration Services) Scale Out](integration-services-ssis-scale-out-master.md)
-   [Trabalho do SSIS (Integration Services) Scale Out](integration-services-ssis-scale-out-worker.md)
