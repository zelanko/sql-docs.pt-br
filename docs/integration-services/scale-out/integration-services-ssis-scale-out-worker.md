---
title: Trabalho do SSIS (SQL Server Integration Services) Scale Out | Microsoft Docs
ms.description: This article describes the Scale Out Master component of SSIS Scale Out
ms.custom: ''
ms.date: 12/19/2017
ms.prod: sql
ms.prod_service: integration-services
ms.component: scale-out
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
caps.latest.revision: 1
author: haoqian
ms.author: haoqian
manager: craigg
ms.openlocfilehash: 5b19aee11489551b3f06fb58cb0242b495929213
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="integration-services-ssis-scale-out-worker"></a>Trabalho de Expansão de Integration Services (SSIS)

O Trabalho do Scale Out executa o serviço Trabalho do Scale Out para efetuar pull de tarefas de execução no Mestre do Scale Out. Em seguida, o trabalho executa os pacotes localmente com `ISServerExec.exe`.

## <a name="configure-the-scale-out-worker-service"></a>Configurar o serviço Trabalho do Scale Out
Configure o serviço Trabalho do Scale Out usando o arquivo ` \<drive\>:\Program Files\Microsoft SQL Server\140\DTS\Binn\WorkerSettings.config`. É necessário reiniciar o serviço depois de atualizar o arquivo de configuração.

Configuração  |Description  |Valor padrão  
---------|---------|---------
DisplayName|O nome de exibição do Trabalho de Expansão. **NÃO em uso no [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 2017.**|Nome do computador         
Description|A descrição do Trabalho de Expansão. **NÃO em uso no [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 2017.**|Empty (vazio)         
MasterEndpoint|O ponto de extremidade para se conectar ao Mestre de Expansão.|O ponto de extremidade definido durante a instalação do Trabalho de Expansão         
MasterHttpsCertThumbprint|A impressão digital do certificado SSL de cliente usada para autenticar o Mestre de Expansão|A impressão digital do certificado do cliente especificada durante a instalação do Trabalho de Expansão.          
WorkerHttpsCertThumbprint|A impressão digital do certificado do Mestre de Expansão usada para autenticar o Trabalho de Expansão.|A impressão digital do certificado criado e instalado automaticamente durante a instalação do Trabalho de Expansão          
StoreLocation|O local de repositório de certificado do trabalho.|LocalMachine       
StoreName|O nome do repositório no qual está o certificado do trabalho.|Meu         
AgentHeartbeatInterval|O intervalo de pulsação do Trabalho de Expansão.|00:01:00         
TaskHeartbeatInterval|O intervalo no qual o Trabalho de Expansão relata o estado da tarefa.|00:00:10         
HeartbeatErrorTollerance|Após esse período de tempo, na última pulsação de tarefa com êxito, a tarefa será terminada se for recebida uma resposta de erro da pulsação.|00:10:00      
TaskRequestMaxCPU|O limite superior de CPU para tarefas de solicitação do Trabalho de Expansão.|70.0         
TaskRequestMinMemory|O limite inferior de memória, em MB, para tarefas de solicitação do Trabalho de Expansão.|100.0         
MaxTaskCount|O número máximo de tarefas que o Trabalho de Expansão pode conter.|10         
LeaseInternval|O intervalo de concessão de uma tarefa contida pelo Trabalho de Expansão.|00:01:00         
TasksRootFolder|A pasta de logs de tarefas. Se o valor estiver vazio, o caminho de pasta `\<drive\>:\Users\[account]\AppData\Local\SSIS\Cluster\Tasks` será usado. [account] é a conta que executa o serviço Trabalho de Expansão. Por padrão, a conta é SSISScaleOutWorker140.|Empty (vazio)         
TaskLogLevel|O nível de log de tarefas do Trabalho de Expansão. (Verbose 0x01, Information 0x02, Warning 0x04, Error 0x08, Progress 0x10, CriticalError 0x20, Audit 0x40)|126 (Information, Warning, Error, Progress, CriticalError, Audit)     
TaskLogSegment|O período de tempo de um arquivo de log de tarefas.|00:00:00         
TaskLogEnabled|Especifica se o log de tarefas está habilitado.|true         
ExecutionLogCacheFolder|A pasta usada para armazenar em cache o log de execução de pacote. Se o valor estiver vazio, o caminho de pasta ` \<drive\>:\Users\[account]\AppData\Local\SSIS\Cluster\Agent\ELogCache` será usado. [account] é a conta que executa o serviço Trabalho de Expansão. Por padrão, a conta é SSISScaleOutWorker140.|Empty (vazio)         
ExecutionLogMaxBufferLogCount|O número máximo de logs de execução armazenados em cache em um buffer de log de execução na memória.|10000        
ExecutionLogMaxInMemoryBufferCount|O número máximo de buffers de log de execução na memória de logs de execução.|10         
ExecutionLogRetryCount|O número de repetições se o log de execução falhar.|3
ExecutionLogRetryTimeout|A repetição atinge o tempo limite se o log de execução falha. Se ExecutionLogRetryTimeout for atingido, ExecutionLogRetryCount será ignorada. |7.00:00:00 (7 dias)        
AgentId|ID do agente de Trabalho do Trabalho do Scale Out|Gerado automaticamente    
||||    

## <a name="view-the-scale-out-worker-log"></a>Exibir o log do Trabalho do Scale Out
O arquivo de log do serviço Trabalho do Scale Out está na pasta `\<drive\>:\Users\\[account]\AppData\Local\SSIS\ScaleOut\Agent`.

O local do log de cada tarefa individual é configurado no arquivo `WorkerSettings.config` na `TasksRootFolder`. Se um valor não for especificado, o log estará na pasta `\<drive\>:\Users\\[account]\AppData\Local\SSIS\ScaleOut\Tasks`. 

O parâmetro *[account]* é a conta que executa o serviço Trabalho do Scale Out. Por padrão, a conta é `SSISScaleOutWorker140`.

## <a name="next-steps"></a>Próximas etapas
[Mestre do SSIS (Integration Services) Scale Out](integration-services-ssis-scale-out-master.md)
