---
title: Mestre do Scale Out do SSIS (SQL Server Integration Services) | Microsoft Docs
ms.description: This article describes the Scale Out Master component of SSIS Scale Out
ms.custom: 
ms.date: 12/19/2017
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
ms.openlocfilehash: 2a2405606b0ce974c4067e8f7aa53fe9e9c841bf
ms.sourcegitcommit: 23433249be7ee3502c5b4d442179ea47305ceeea
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/20/2017
---
# <a name="integration-services-ssis-scale-out-master"></a>Mestre de Expansão de Integration Services (SSIS)
O Mestre do Scale Out gerencia o sistema do Scale Out por meio do Catálogo do SSISDB e do serviço Mestre do Scale Out. 

O Catálogo do SSISDB armazena todas as informações de Trabalhos do Scale Out, pacotes e execuções. Ele fornece a interface para habilitar um Trabalho de Expansão e executar pacotes em Expansão. Para obter mais informações, consulte [Passo a passo: Configurar o Integration Services Scale Out](walkthrough-set-up-integration-services-scale-out.md) e [Executar pacotes no Integration Services](run-packages-in-integration-services-ssis-scale-out.md).

O serviço Mestre do Scale Out é um serviço Windows responsável pela comunicação com os Trabalhos do Scale Out. Ele retorna o status das execuções de pacote nos Trabalhos do Scale Out por HTTPS e opera nos dados no SSISDB. 

## <a name="scale-out-views-and-stored-procedures-in-ssisdb"></a>Exibições e procedimentos armazenados do Scale Out no SSISDB

### <a name="views"></a>Exibições:
-   [[catalog].[master_properties(../../integration-services/system-views/catalog-master-properties-ssisdb-database.md)
-   [[catalog].[worker_agents]](../../integration-services/system-views/catalog-worker-agents-ssisdb-database.md).

####<a name="stored-procedures"></a>Procedimentos armazenados:

-   Para gerenciar Trabalhos do Scale Out:  
    -   [[catalog].[disable_worker_agent]](../../integration-services/system-stored-procedures/catalog-disable-worker-agent-ssisdb-database.md)
    -   [[catalog].[enable_worker_agent]](../../integration-services/system-stored-procedures/catalog-enable-worker-agent-ssisdb-database.md).

- Para executar pacotes no Scale Out:   
    -   [[catalog].[create_execution]](../../integration-services/system-stored-procedures/catalog-create-execution-ssisdb-database.md)
    -   [[catalog].[add_execution_worker]](../../integration-services/system-stored-procedures/catalog-add-execution-worker-ssisdb-database.md)
    -   [[catalog].[start_execution]](../../integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database.md).   

## <a name="configure-the-scale-out-master-service"></a>Configurar o serviço Mestre do Scale Out
Configure o serviço Mestre do Scale Out usando o arquivo `\<drive\>:\Program Files\Microsoft SQL Server\140\DTS\Binn\MasterSettings.config`. É necessário reiniciar o serviço depois de atualizar o arquivo de configuração.


Configuração  |Description  |Valor Padrão  
---------|---------|---------
PortNumber|O número da porta de rede usado para se comunicar com um Trabalho de Expansão.|8391         
SSLCertThumbprint|A impressão digital do certificado SSL usado para proteger a comunicação com um Trabalho de Expansão.|A impressão digital do certificado SSL especificado durante a instalação do Mestre de Expansão         
SqlServerName|O nome do [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] que contém o catálogo SSISDB. Por exemplo, ServerName\\\\InstanceName.|O nome do SQL Server que é instalada com o Mestre do Scale Out.         
CleanupCompletedJobsIntervalInMs|O intervalo de limpeza de trabalhos de execução concluídos, em milissegundos.|43200000         
DealWithExpiredTasksIntervalInMs|O intervalo para lidar com trabalhos de execução expirados, em milissegundos.|300000
MasterHeartbeatIntervalInMs|O intervalo de pulsação do Mestre de Expansão, em milissegundos. Essa propriedade especifica o intervalo no qual o Mestre do Scale Out atualiza seu status online no catálogo do SSISDB.|30000
SqlConnectionTimeoutInSecs|O tempo de limite de conexão SQL em segundos ao se conectar ao SSISDB.|15    
||||    

## <a name="view-the-scale-out-master-service-log"></a>Exibir o log do serviço do Mestre do Scale Out
O arquivo de log do serviço do Mestre do Scale Out está localizado na pasta `\<drive\>:\Users\\[account]\AppData\Local\SSIS\ScaleOut\Master`. 

O parâmetro *[account]* refere-se à conta que executa o serviço Mestre do Scale Out. Por padrão, essa conta é `SSISScaleOutMaster140`.

## <a name="next-steps"></a>Próximas etapas
[Trabalho do SSIS (Integration Services) Scale Out](integration-services-ssis-scale-out-worker.md)
