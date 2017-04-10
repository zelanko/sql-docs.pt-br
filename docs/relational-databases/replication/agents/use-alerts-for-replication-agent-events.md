---
title: "Usar Alertas para eventos do agente de replica&#231;&#227;o | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "exibindo alertas"
  - "Queue Reader Agent, alertas"
  - "alertas [replicação do SQL Server]"
  - "alertas de replicação predefinidos [replicação do SQL Server]"
  - "Log Reader Agent, alertas"
  - "Agente de Distribuição, alertas"
  - "Merge Agent, alertas"
  - "agentes [replicação do SQL Server], alertas"
  - "exibindo alertas"
  - "Snapshot Agent, alertas"
ms.assetid: 8c42e523-7020-471d-8977-a0bd044b9471
caps.latest.revision: 39
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 39
---
# Usar Alertas para eventos do agente de replica&#231;&#227;o
  [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] e [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] agente fornecem uma forma de monitorar eventos, como eventos do agente de replicação, usando alertas. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agente monitora o log de aplicativo do Windows para eventos que são associados aos alertas. Se esse evento ocorrer, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent responderá automaticamente, executando uma tarefa que você definiu e/ou enviando uma mensagem de email ou pager a um operador especificado. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] inclui um conjunto de alertas predefinidos para agentes de replicação que podem ser configurados para executar uma tarefa e/ou notificar um operador. Para obter mais informações sobre como definir uma tarefa a executar, consulte a seção “Automatizando uma resposta para um alerta” neste tópico.  
  
 Os alertas a seguir são instalados quando um computador é configurado como um Distribuidor:  
  
|ID da mensagem|Alerta predefinido|Condição que aciona o alerta |Insere informações adicionais em msdb..sysreplicationalerts|  
|----------------|----------------------|-----------------------------------------|-----------------------------------------------------------------|  
|14150|**Replicação: êxito do agente**|Agente é encerrado com êxito.|Sim|  
|14151|**Replicação: falha do agente**|Agente é desligado com um erro.|Sim|  
|14152|**Replicação: repetição do agente**|O agente desliga após repetir uma operação sem-êxito (agente encontra erro, como servidor não disponível, deadlock, falha de conexão ou falha de tempo limite).|Sim|  
|14157|**Replicação: assinatura expirada cancelada**|A assinatura expirada foi descartada.|Não|  
|20572|**Replicação: assinatura reinicializada após falha de validação**|Trabalho de resposta 'Reinicializar assinatura em falha de validação de dados' reinicializa uma assinatura com êxito.|Não|  
|20574|**Replicação: falha na validação de dados do assinante**|O Agente de Distribuição ou Mesclagem falha na validação de dados.|Sim|  
|20575|**Replicação: êxito na validação de dados do assinante**|Distribution ou Merge Agent passa na validação de dados.|Sim|  
|20578|**Replicação: desligamento personalizado do agente**|||  
|22815|**Alerta de detecção de conflito ponto a ponto**|O Agente de Distribuição detectou um conflito ao tentar aplicar uma alteração a um nó ponto a ponto.|Sim|  
  
 Além desses alertas, o Replication Monitor fornece um conjunto de avisos e alertas relacionado ao status e ao desempenho. Para obter mais informações, consulte [definir limites e avisos no Replication Monitor](../../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md). Também é possível definir alertas para outros eventos de replicação por meio da infraestrutura de alerta do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Para obter mais informações, consulte [criar um evento definido pelo usuário](../../../ssms/agent/create-a-user-defined-event.md).  
  
 **Para configurar os alertas de replicação predefinidos**  
  
-   [! INCLUIR [ssManStudioFull] (... / Token/ssManStudioFull_md.md)]: [Configure Predefined Replication Alerts &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/administration/configure-predefined-replication-alerts-sql-server-management-studio.md)  
  
## Exibindo o log do aplicativo diretamente  
 Para exibir o log de aplicativo do Windows, use o [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visualizar eventos do Windows. O log do aplicativo contém mensagens de erro do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], assim como mensagens para muitas outras atividades no computador. Ao contrário do log de erros do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], um novo aplicativo não é criado a cada vez que se inicia o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (cada sessão do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] grava novos eventos a um log de aplicativos existente); entretanto, é possível especificar quanto tempo os eventos registrados serão retidos. Ao exibir o log do aplicativo do Windows, é possível filtrar o log para eventos específicos. Para obter mais informações, consulte a documentação do Windows.  
  
## Automatizando uma resposta para um alerta  
 A replicação fornece um trabalho de resposta para assinaturas que apresentam falhas na validação dos dados, e também fornece uma estrutura para criar respostas automáticas adicionais para alertas.  O trabalho de resposta é intitulado **reinicializar assinaturas em falha de validação de dados** e é armazenado na [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] agente **trabalhos** pasta [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]. Para obter informações sobre como habilitar esse trabalho de resposta, consulte [Configurar alertas de replicação predefinidos e 40; SQL Server Management Studio e 41;](../../../relational-databases/replication/administration/configure-predefined-replication-alerts-sql-server-management-studio.md). Se artigos em uma publicação transacional falharem na validação, o trabalho de resposta reinicializa apenas esses artigos que falharam. Se artigos em uma publicação de mesclagem apresentarem falha na validação, o trabalho de resposta reinicializa todos os artigos na publicação.  
  
### Estrutura para automatizar respostas  
 Normalmente, quando ocorre um alerta, a única informação se tem que o ajuda a entender o que causou o alerta e a ação apropriada a tomar está na própria mensagem de alerta. A análise dessas informações pode ser suscetível a erros e ser demorada. Replicação facilita as respostas automáticas, fornecendo informações adicionais sobre o alerta de **sysreplicationalerts** tabela do sistema; as informações fornecidas já são analisadas em um formato simples usado por programas personalizados.  
  
 Por exemplo, se os dados a **Sales. SalesOrderHeader** tabela no assinante A falha na validação, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] pode acionar a mensagem 20574, notificando essa falha. A mensagem recebida será: "O assinante 'A', assinatura para o artigo 'SalesOrderHeader' na publicação 'MyPublication' Falha na validação de dados."  
  
 Ao criar uma resposta baseada nessa mensagem, é necessário analisar manualmente o nome do Assinante, nome do artigo e nome da publicação e erro da mensagem. No entanto, porque o Distribution Agent e o agente de mesclagem gravam a mesma informação para **sysreplicationalerts** (juntamente com detalhes como o tipo de agente, hora do alerta, banco de dados de publicação, banco de dados do assinante e tipo de publicação) o trabalho de resposta pode consultar diretamente as informações relevantes da tabela. Embora a linha exata não pode ser associada uma instância específica do alerta, a tabela tem um **status** coluna, que pode ser usada para controlar as entradas atendidas. As entradas nessa tabela serão mantidas pelo período de retenção do histórico.  
  
 Por exemplo, se fosse criada uma resposta de trabalho no [!INCLUDE[tsql](../../../includes/tsql-md.md)] que atendesse à mensagem de alerta 20574, a seguinte lógica poderia ser usada:  
  
```  
declare @publisher sysname, @publisher_db sysname, @publication sysname, @publication_type int, @article sysname, @subscriber sysname, @subscriber_db sysname, @alert_id int  
declare hc cursor local for select publisher, publisher_db, publication, publication_type, article, subscriber,   
  subscriber_db, alert_id from   
  msdb..sysreplicationalerts where  
  alert_error_code = 20574 and status = 0  
  for read only  
open hc  
fetch hc into  @publisher, @publisher_db, @publication, @publication_type, @article, @subscriber, @subscriber_db, @alert_id  
while (@@fetch_status <> -1)  
begin  
/* Do custom work  */  
/* Update status to 1, which means the alert has been serviced. This prevents subsequent runs of this job from doing this again */  
update msdb..sysreplicationalerts set status = 1 where alert_id = @alert_id  
 fetch hc into  @publisher, @publisher_db, @publication, @publication_type, @article, @subscriber, @subscriber_db, @alert_id  
end  
close hc  
deallocate hc  
```  
  
## Consulte também  
 [Administração do agente de replicação](../../../relational-databases/replication/agents/replication-agent-administration.md)   
 [Práticas recomendadas para administração de replicação](../../../relational-databases/replication/administration/best-practices-for-replication-administration.md)   
 [Monitoramento e 40; Replicação e 41;](../../../relational-databases/replication/monitor/monitoring-replication.md)  
  
  