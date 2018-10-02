---
title: MSSQLSERVER_14420 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 14420 (Database Engine error)
ms.assetid: 4a1d72b1-ab1b-4119-a11b-a8a05c6fdb45
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 66ffbd16db1cf5c044d057e7dfd3c70087771b4e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47688715"
---
# <a name="mssqlserver14420"></a>MSSQLSERVER_14420
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|14420|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|SQLErrorNum14420|  
|Texto da mensagem|O banco de dados primário de envio de logs %s.%s tem um limite de backup de %d minutos e não executou uma operação de log de backup há %d minutos. Verifique as informações de monitoração de log do agente e de envio de logs.|  
  
## <a name="explanation"></a>Explicação  
O envio de logs está fora de sincronia além do limite de backup. O limite de backup é o número de minutos entre os trabalhos de backup de envio de logs antes de um alerta ser gerado. Essa mensagem não indica necessariamente um problema com o envio de logs. Em vez disso, ela pode indicar um dos seguintes problemas:  
  
-   O trabalho de backup não está sendo executado. Causas possíveis: o serviço SQL Server Agent na instância do servidor primário não está sendo executado, o trabalho está desabilitado ou a agenda do trabalho foi alterada.  
  
-   O trabalho de backup está apresentando falhas. Causas possíveis: o caminho de pasta de backup não é válido, o disco está cheio ou qualquer outro motivo pelo qual a instrução BACKUP possa apresentar falha.  
  
## <a name="user-action"></a>Ação do usuário  
Para solucionar o problema dessa mensagem:  
  
-   Verifique se o serviço SQL Server Agent está sendo executado para a instância do servidor primário e se o trabalho de backup para esse banco de dados primário está habilitado e agendado para ser executado na frequência apropriada.  
  
-   O trabalho de backup no servidor primário pode estar apresentando falhas. Nesse caso, examine o histórico de trabalhos do trabalho de backup para procurar a causa.  
  
-   É possível que o trabalho de backup de envio de logs, executado na instância do servidor primário, não consiga se conectar à instância do servidor monitor para atualizar a tabela **log_shipping_monitor_primary**. Isso pode ser causado por um problema de autenticação entre a instância do servidor monitor e a instância do servidor primário.  
  
-   O limite de alerta de backup pode ter um valor incorreto. De modo ideal, esse valor é definido para pelo menos três vezes a frequência do trabalho de backup. Se você alterar a frequência do trabalho de backup depois que o envio de logs estiver configurado e funcionando, também deverá atualizar o valor do limite de alerta de backup.  
  
-   Quando a instância do servidor monitor fica offline e, depois, volta a ficar online, a tabela **log_shipping_monitor_primary** não é atualizada com os valores atuais antes da execução do trabalho de mensagem de alerta. Para atualizar as tabelas do monitor com os últimos dados do banco de dados primário, execute **sp_refresh_log_shipping_monitor** na instância do servidor primário.  
  
-   Na instância do servidor monitor ou primário, a data ou a hora está incorreta. Isso também pode gerar mensagens de alerta. É possível que a data ou a hora do sistema tenha sido modificada em um deles.  
  
    > [!NOTE]  
    > Fusos horários diferentes para as duas instâncias de servidor não deveriam causar um problema.  
  
## <a name="see-also"></a>Consulte Também  
[log_shipping_monitor_primary &#40;Transact-SQL&#41;](~/relational-databases/system-tables/log-shipping-monitor-primary-transact-sql.md)  
[Sobre o envio de logs &#40;SQL Server&#41;](~/database-engine/log-shipping/about-log-shipping-sql-server.md)  
[sp_help_log_shipping_monitor_primary &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-help-log-shipping-monitor-primary-transact-sql.md)  
[sp_refresh_log_shipping_monitor &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-help-log-shipping-monitor-transact-sql.md)  
[Sobre o envio de logs &#40;SQL Server&#41;](~/database-engine/log-shipping/about-log-shipping-sql-server.md)  
  
