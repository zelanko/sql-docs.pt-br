---
title: "MSSQL_ENG014152 | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "erro MSSQL_ENG014152"
ms.assetid: 4215e2b1-cd30-441f-9671-9afc742adf6e
caps.latest.revision: 11
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 11
---
# MSSQL_ENG014152
    
## Detalhes da mensagem  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|14152|  
|Origem do evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nome simbólico||  
|Texto da mensagem|Replicação-%s: agente %s agendado para tentar novamente. %s|  
  
## Explicação  
 O agente de replicação especificado foi programado para repetir a operação solicitada. O processo continua repetindo até alcançar o número máximo configurado de tentativas de repetição para a etapa de trabalho.  
  
 Normalmente, uma repetição ocorre devido a um dos seguintes motivos:  
  
-   O valor **QueryTimeout** é excedido.  
  
-   O valor **LoginTimeout** é excedido.  
  
-   O processo de replicação foi escolhido como uma vítima de deadlock.  
  
## Ação do usuário  
 Se a mensagem de repetição não for frequente, nenhuma ação é exigida do usuário.  
  
 Use [sp_help_jobstep](../../relational-databases/system-stored-procedures/sp-help-jobstep-transact-sql.md) para exibir a configuração atual para o número máximo de vezes que o **Executar Agente** etapa o agente de replicação especificada será repetida. Você pode usar o **@retry_attempts** parâmetro o [sp_update_jobstep](../../relational-databases/system-stored-procedures/sp-update-jobstep-transact-sql.md) procedimento armazenado para ajustar o número de vezes de tentativas de uma etapa de trabalho.  
  
 Se a mensagem de repetição ocorrer com frequência, você deverá solucionar o problema com base na mensagem que está causando a repetição. Verifique o histórico do agente para mensagens que indicam por que a nova tentativa teve que ser programada. Em alguns casos, talvez seja necessário habilitar o log mais detalhado do agente de replicação. Para obter mais informações sobre como configurar o log para replicação, consulte o artigo [312292](http://support.microsoft.com/kb/312292)na Base de Dados de Conhecimento Microsoft.  
  
## Consulte também  
 [Erros e eventos referência & #40. Replicação e 41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  