---
title: Mestre do Scale Out do SSIS (SQL Server Integration Services) | Microsoft Docs
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
ms.openlocfilehash: 07cd19a5e7a53e824d2bed3a2e2943efd7ef867b
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="integration-services-ssis-scale-out-master"></a>Mestre de Expansão de Integration Services (SSIS)
O Mestre de Expansão gerencia o sistema de Expansão por meio do Catálogo do SSISDB e do serviço Mestre de Expansão. 

O catálogo SSISDB armazena todas as informações de pacotes, execuções e dos Trabalhos de Expansão. Ele fornece a interface para habilitar um Trabalho de Expansão e executar pacotes em Expansão. Para obter mais informações, consulte [Passo a passo: configurar a Expansão do Integration Services](walkthrough-set-up-integration-services-scale-out.md) e [Executar Pacotes no Integration Services](run-packages-in-integration-services-ssis-scale-out.md).

O serviço Mestre de Expansão é um serviço Windows que é responsável pela comunicação com os Trabalhos de Expansão. Ele troca o status das execuções de pacote com os Trabalhos de Expansão através de HTTPS e opera nos dados de SSISDB. 

## <a name="scale-out-related-sql-views-and-stored-procedures-in-ssisdb"></a>Procedimentos armazenados e exibições SQL relacionados a Scale Out no SSISDB

#### <a name="views"></a>Exibições:
[[catalog].[master_properties]](../../integration-services/system-views/catalog-master-properties-ssisdb-database.md), [[catalog].[worker_agents]](../../integration-services/system-views/catalog-worker-agents-ssisdb-database.md).

#### <a name="stored-procedures"></a>Procedimentos armazenados:

- Para o gerenciamento de Trabalho de Expansão:  
 [[catalog].[disable_worker_agent]](../../integration-services/system-stored-procedures/catalog-disable-worker-agent-ssisdb-database.md), [[catalog].[enable_worker_agent]](../../integration-services/system-stored-procedures/catalog-enable-worker-agent-ssisdb-database.md).
- Para executar pacotes em Expansão:   
[[catalog].[create_execution]](../../integration-services/system-stored-procedures/catalog-create-execution-ssisdb-database.md), [[catalog].[add_execution_worker]](../../integration-services/system-stored-procedures/catalog-add-execution-worker-ssisdb-database.md), [[catalog].[start_execution]](../../integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database.md).   

## <a name="configure-sql-server-integration-services-scale-out-master-service"></a>Configurar o serviço Mestre de Expansão do SQL Server Integration Services
O serviço Mestre de Expansão pode ser configurado usando o arquivo \<driver\>:\Program Files\Microsoft SQL Server\140\DTS\Binn\MasterSettings.config. O serviço deve ser reiniciado depois de atualizar o arquivo de configuração.


Configuração  |Description  |Valor Padrão  
---------|---------|---------
PortNumber|O número da porta de rede usado para se comunicar com um Trabalho de Expansão.|8391         
SSLCertThumbprint|A impressão digital do certificado SSL usado para proteger a comunicação com um Trabalho de Expansão.|A impressão digital do certificado SSL especificado durante a instalação do Mestre de Expansão         
SqlServerName|O nome do [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] que contém o catálogo SSISDB. Por ex.: ServerName\\\\InstanceName.|O nome do SQL Server que é instalada com o Mestre do Scale Out.         
CleanupCompletedJobsIntervalInMs|O intervalo de limpeza de trabalhos de execução concluídos, em milissegundos.|43200000         
DealWithExpiredTasksIntervalInMs|O intervalo para lidar com trabalhos de execução expirados, em milissegundos.|300000
MasterHeartbeatIntervalInMs|O intervalo de pulsação do Mestre de Expansão, em milissegundos. Especifica o intervalo no qual o Mestre de Expansão atualiza seu status online no catálogo do SSISDB.|30000
SqlConnectionTimeoutInSecs|O tempo de limite de conexão SQL em segundos ao se conectar ao SSISDB.|15        

## <a name="view-scale-out-master-service-log"></a>Exibir log de serviço do Mestre de Expansão
O arquivo de log do Mestre de Scale Out está localizado no caminho da pasta \<unidade\>:\Users\\*[conta]*\AppData\Local\SSIS\ScaleOut\Master. 

A pasta *[conta]* refere-se à conta que executa o serviço Mestre do Scale Out. Por padrão, essa conta é SSISScaleOutMaster140.
