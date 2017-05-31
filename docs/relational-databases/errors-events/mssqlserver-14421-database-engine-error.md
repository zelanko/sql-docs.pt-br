---
title: MSSQLSERVER_14421 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 14421 (Database Engine error)
ms.assetid: 03e76d4a-d463-4673-8843-08e4ecaefe27
caps.latest.revision: 23
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: cc4a06f7b9b27884ac0a5998d43ef056368dcc73
ms.contentlocale: pt-br
ms.lasthandoff: 04/11/2017

---
# <a name="mssqlserver14421"></a>MSSQLSERVER_14421
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|14421|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|SQLErrorNum14421|  
|Texto da mensagem|O banco de dados secundário de envio de logs %s.%s tem um limite de restauração de %d minutos e está fora de sincronização. Nenhuma restauração foi executada há %d minutos. A latência restaurada é de %d minutos. Verifique as informações de monitoração de log do agente e de envio de logs.|  
  
## <a name="explanation"></a>Explicação  
Essa mensagem indica que o envio de logs está fora de sincronia além do limite de restauração. O limite de restauração é o número de minutos entre as operações de restauração antes de uma mensagem ser gerada.  
  
### <a name="possible-causes"></a>Causas possíveis  
Essa mensagem não indica necessariamente um problema com o envio de logs. Em vez disso, ela pode indicar um dos seguintes problemas:  
  
-   O trabalho de restauração não está sendo executado.  
  
    É possível que o trabalho não esteja sendo executando pelas seguintes causas: o serviço SQL Server Agent na instância do servidor secundário não está sendo executado, o trabalho está desabilitado ou a agenda do trabalho foi alterada.  
  
-   O trabalho de restauração está apresentando falhas.  
  
    É possível que o trabalho esteja apresentando falhas pelas seguintes causas: o caminho da pasta de restauração não é válido, o disco está cheio ou qualquer outro motivo pelo qual a instrução RESTORE possa apresentar falha.  
  
## <a name="user-action"></a>Ação do usuário  
Para solucionar o problema dessa mensagem:  
  
-   Verifique se o serviço SQL Server Agent está sendo executado para a instância do servidor secundário e se o trabalho de restauração para esse banco de dados secundário está habilitado e agendado para ser executado na frequência apropriada.  
  
-   O trabalho de restauração no servidor secundário pode estar apresentando falha. Nesse caso, verifique o histórico de trabalhos do trabalho de restauração para procurar a causa.  
  
-   É possível que o trabalho de restauração de envio de logs, executado na instância do servidor secundário, não consiga se conectar à instância do servidor monitor para atualizar a tabela **log_shipping_monitor_secondary**. Isso pode ser causado por um problema de autenticação entre a instância do servidor monitor e a instância do servidor secundário.  
  
-   O limite de alerta de backup pode ter um valor incorreto. De modo ideal, esse valor é definido para pelo menos três vezes a frequência do trabalho de restauração. Se você alterar a frequência do trabalho de restauração depois que o envio de logs estiver configurado e funcionando, também deverá atualizar o valor do limite de alerta de backup.  
  
-   Quando a instância do servidor monitor fica offline e, depois, volta a ficar online, a tabela **log_shipping_monitor_secondary** não é atualizada com os valores atuais antes da execução do trabalho de mensagem de alerta. O erro 14421 pode surgir quando um trabalho de restauração resulta em "Não foi possível localizar um arquivo de backup de log que pudesse ser aplicado ao banco de dados secundário". Quando isso acontece, a hora da restauração não é atualizada. Nesse caso, a causa do erro pode ser um problema com o trabalho de cópia.  
  
    Para atualizar as tabelas do monitor com os últimos dados do banco de dados secundário, execute **sp_refresh_log_shipping_monitor** na instância do servidor secundário.  
  
-   Na instância do servidor monitor ou secundário, a data ou a hora está incorreta. Isso também pode gerar mensagens de alerta. É possível que a data ou a hora do sistema tenha sido modificada em um deles.  
  
    > [!NOTE]  
    > Fusos horários diferentes para as duas instâncias de servidor não deveriam causar um problema.  
  
## <a name="see-also"></a>Consulte também  
[log_shipping_monitor_secondary &#40;Transact-SQL&#41;](~/relational-databases/system-tables/log-shipping-monitor-secondary-transact-sql.md)  
[Sobre o envio de logs &#40;SQL Server&#41;](~/database-engine/log-shipping/about-log-shipping-sql-server.md)  
[sp_help_log_shipping_monitor_secondary &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-help-log-shipping-monitor-secondary-transact-sql.md)  
[sp_refresh_log_shipping_monitor &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-help-log-shipping-monitor-transact-sql.md)  
[Sobre o envio de logs &#40;SQL Server&#41;](~/database-engine/log-shipping/about-log-shipping-sql-server.md)  
  

