---
title: "Trabalho de Expans&#227;o de Integration Services (SSIS) | Microsoft Docs"
ms.custom: ""
ms.date: "12/16/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 480a3f3d-9a79-4a02-81e5-7d27afd756c4
caps.latest.revision: 7
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 7
---
# Trabalho de Expans&#227;o de Integration Services (SSIS)
O Trabalho de Expansão executa um [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion_md](../includes/ssisnoversion-md.md)] serviço de Trabalho de Expansão para efetuar pull de tarefas de execução do Mestre de Expansão, e executa os pacotes localmente com o ISServerExec.exe.

## <a name="configure-sql-server-integration-services-scale-out-worker-service"></a>Configurar o serviço Trabalho de Expansão do SQL Server Integration Services
O serviço Trabalho de Expansão pode ser configurado usando o arquivo \<driver\>:\Program Files\Microsoft SQL Server\140\DTS\Binn\WorkerSettings.config. O serviço deve ser reiniciado depois de atualizar o arquivo de configuração.
    


Configuração  |Description  |Valor padrão  
---------|---------|---------
DisplayName|O nome de exibição do Trabalho de Expansão. **NÃO está em uso no [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] vNext CTP1.**|Nome do computador         
Description|A descrição do Trabalho de Expansão. **NÃO está em uso no [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] vNext CTP1.**|Empty (vazio)         
MasterEndpoint|O ponto de extremidade para se conectar ao Mestre de Expansão.|O ponto de extremidade definido durante a instalação do Trabalho de Expansão         
MasterHttpsCertThumbprint|A impressão digital do certificado SSL de cliente usada para autenticar o Mestre de Expansão|A impressão digital do certificado do cliente especificada durante a instalação do Trabalho de Expansão.          
WorkerHttpsCertThumbprint|A impressão digital do certificado do Mestre de Expansão usada para autenticar o Trabalho de Expansão.|A impressão digital do certificado criado e instalado automaticamente durante a instalação do Trabalho de Expansão          
StoreLocation|O local de repositório de certificado do trabalho.|LocalMachine       
StoreName|O nome do repositório no qual está o certificado do trabalho.|Meu         
AgentHeartbeatInterval|O intervalo de pulsação do Trabalho de Expansão.|00:01:00         
TaskHeartbeatInterval|O intervalo no qual o Trabalho de Expansão relata o estado da tarefa.|00:00:10         
HeartbeatErrorTollerance|Após esse período de tempo, na última pulsação de tarefa com êxito, a tarefa será terminada se for recebida uma resposta de erro da pulsação.|00:10:00      
TaskRequestMaxCPU|O limite superior de CPU para tarefas de solicitação do Trabalho de Expansão. **NÃO está em uso no [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] vNext CTP1.**|70.0         
TaskRequestMinMemory|O limite inferior de memória, em MB, para tarefas de solicitação do Trabalho de Expansão. **NÃO está em uso no [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] vNext CTP1.**|100.0         
MaxTaskCount|O número máximo de tarefas que o Trabalho de Expansão pode conter.|10         
LeaseInternval|O intervalo de concessão de uma tarefa contida pelo Trabalho de Expansão.|00:01:00         
TasksRootFolder|A pasta de logs de tarefas. O caminho de pasta \<driver\>:\Users\\*[account]*\AppData\Local\SSIS\Cluster\Tasks será usado se o valor estiver vazio. [account] é a conta que executa o serviço Trabalho de Expansão. Por padrão, a conta é SSISScaleOutWorker140.|Empty (vazio)         
TaskLogLevel|O nível de log de tarefas do Trabalho de Expansão. (Verbose 0x01, Information 0x02, Warning 0x04, Error 0x08, Progress 0x10, CriticalError 0x20, Audit 0x40)|126 (Information,Warning,Error,Progress,CriticalError,Audit)     
TaskLogSegment|O período de tempo de um arquivo de log de tarefas.|00:00:00         
TaskLogEnabled|Especifica se o log de tarefas está habilitado.|true         
ExecutionLogCacheFolder|A pasta usada para armazenar em cache o log de execução de pacote. O caminho de pasta \<driver\>:\Users\\*[account]*\AppData\Local\SSIS\Cluster\Agent\ELogCache será usado se o valor estiver vazio. [account] é a conta que executa o serviço Trabalho de Expansão. Por padrão, a conta é SSISScaleOutWorker140.|Empty (vazio)         
ExecutionLogMaxBufferLogCount|O número máximo de logs de execução armazenados em cache em um buffer de log de execução na memória.|10000        
ExecutionLogMaxInMemoryBufferCount|O número máximo de buffers de log de execução na memória de logs de execução.|10         
ExecutionLogRetryCount|O número de repetições se o log de execução falhar.|3         
AgentId|ID do agente de trabalho do Trabalho de Expansão|Gerado automaticamente        



## <a name="view-scale-out-worker-log"></a>Exibir o log do Trabalho de Expansão
O arquivo de log do Trabalho de Expansão está no caminho da pasta \<driver\>:\Users\\*[account]*\AppData\Local\SSIS\Cluster\Agent.

O local do log de cada tarefa individual é configurado no arquivo WorkerSettings.config por TasksRootFolder. Se não for especificado, o log estará no caminho de pasta \<driver\>:\Users\\*[account]*\AppData\Local\SSIS\Cluster\Tasks. 

A pasta *[account]* é a conta que executa o serviço Trabalho de Expansão. Por padrão, a conta é SSISScaleOutWorker140.
    