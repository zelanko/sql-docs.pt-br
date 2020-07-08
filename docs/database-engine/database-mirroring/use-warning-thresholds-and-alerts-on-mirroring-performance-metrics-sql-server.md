---
title: Configurar alertas para métricas de desempenho de espelhamento de banco de dados
description: 'Diretrizes para configurar limites de aviso e alertas para métricas de desempenho usadas pelo espelhamento de banco de dados. '
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- monitoring database mirroring [SQL Server]
- thresholds [SQL Server]
- database mirroring [SQL Server], managing in SQL Server Management Studio
- alerts [SQL Server], database mirroring
- database mirroring [SQL Server], monitoring
- warnings [database mirroring]
ms.assetid: 8cdd1515-0bd7-4f8c-a7fc-a33b575e20f6
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: a34829894a9d4a402749ffd167b8adbfc7951ba6
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85651025"
---
# <a name="use-warning-thresholds-and-alerts-on-mirroring-performance-metrics-sql-server"></a>Use os limites de aviso e alertas em métricas de desempenho de espelhamento (SQL Server)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Este tópico contém informações sobre os eventos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para os quais os limites de avisos podem ser configurados e gerenciados para espelhamento de banco de dados. Você pode usar o Monitor de Espelhamento de Banco de Dados ou os procedimentos armazenados **sp_dbmmonitorchangealert**, **sp_dbmmonitorhelpalert**e **sp_dbmmonitordropalert** . Este tópico também contém informações sobre como configurar alertas em eventos de espelhamento de banco de dados.  
  
 Depois que o monitoramento é definido para um banco de dados espelho, um administrador de sistema pode configurar limites de aviso em várias métricas chave de desempenho. Além disso, um administrador pode configurar alertas nesses e em outros eventos de espelhamento de banco de dados.  
  
  
##  <a name="performance-metrics-and-warning-thresholds"></a><a name="PerfMetricsAndWarningThresholds"></a> Métricas de desempenho e limites de aviso  
 A tabela a seguir lista as métricas de desempenho para as quais os avisos podem ser configurados, descreve o limite de aviso correspondente e lista os rótulos correspondentes do Monitor de Espelhamento de Banco de Dados.  
  
|Métrica de desempenho|Limite de aviso|Rótulo do monitor de espelhamento de banco de dados|  
|------------------------|-----------------------|--------------------------------------|  
|Log não enviado|Especifica quantos quilobytes (KB) de log não enviado geram um aviso na instância do servidor principal. Essa advertência ajuda a medir o potencial para perda de dados em termos de KB e é especialmente relevante para o modo de alto desempenho. No entanto, o aviso também é relevante para o modo de segurança alta, quando o espelhamento é pausado ou suspenso devido à desconexão dos parceiros.|**Avisar se o log não enviado exceder o limite**|  
|Log não restaurado|Especifica quantos KB de log não restaurado geram um aviso na instância do servidor espelho. Esse aviso ajuda a medir o tempo de failover. *Tempo de failover* consiste, essencialmente, no tempo necessário para que o servidor espelho anterior efetue o roll-forward de quaisquer logs restantes em sua fila de restauração, mais um pequeno tempo adicional.<br /><br /> Observação: em um failover automático, o tempo necessário para que o sistema observe o erro é independente do período do failover.<br /><br /> Para obter mais informações, veja [Estime a interrupção do serviço durante troca de função &#40;Espelhamento de Banco de Dados&#41;](../../database-engine/database-mirroring/estimate-the-interruption-of-service-during-role-switching-database-mirroring.md).|**Avisar se o log não restaurado exceder o limite**|  
|Transação não enviada mais antiga|Especifica o número de minutos de transações que podem ser acumuladas na fila de envio, antes da geração de um aviso na instância do servidor principal. Essa advertência ajuda a medir o potencial para perda de dados em termos de tempo e é especialmente relevante no modo de alto desempenho. No entanto, o aviso também é relevante para o modo de segurança alta, quando o espelhamento é pausado ou suspenso devido à desconexão dos parceiros.|**Avisar se a idade da transação não enviada mais antiga exceder o limite**|  
|Sobrecarga espelhada confirmada|Especifica o número de milissegundos de atraso médio por transação tolerado, antes que um aviso seja gerado no servidor principal. Esse atraso consiste na quantidade de sobrecarga incidente enquanto a instância do servidor principal aguarda que a instância do servidor espelho grave o registro do log da transação na fila de restauração. Esse valor é relevante somente no modo de alta segurança.|**Avisar se a sobrecarga espelhada confirmada exceder o limite**|  
  
 Para qualquer uma dessas métrica de desempenho, um administrador de sistema pode especificar um limite em um banco de dados espelho. Para obter mais informações, consulte [Configurando e gerenciando limites de aviso](#SetUpManageWarningThresholds), posteriormente neste tópico.  
  
##  <a name="setting-up-and-managing-warning-thresholds"></a><a name="SetUpManageWarningThresholds"></a> Configurando e gerenciando limites de aviso  
 Um administrador de sistema pode configurar um ou mais limites de aviso para as métricas de desempenho chave de espelhamento. Recomendamos a definição de um limite para um determinado aviso em ambos os parceiros para garantir que o aviso persista se o banco de dados cair. O limite apropriado de cada parceiro depende dos recursos de desempenho do sistema daquele parceiro.  
  
 Limites de aviso também podem ser configurados e gerenciados com uma das seguintes opções:  
  
-   Monitor de Espelhamento de Banco de Dados  
  
     No Monitor de Espelhamento de Banco de Dados, o administrador pode exibir a configuração atual de avisos para um banco de dados selecionado nas instâncias do servidor principal e espelho ao mesmo tempo, selecionando a página com guias **Avisos** . Dessa página, o administrador pode abrir a caixa de diálogo **Definir Limites de Aviso** para habilitar e configurar um ou mais limites de aviso.  
  
     Para uma introdução à interface do Monitor de Espelhamento de Banco de Dados, consulte [Database Mirroring Monitor Overview](../../database-engine/database-mirroring/database-mirroring-monitor-overview.md). Para obter informações sobre como iniciar o Monitor de Espelhamento de Banco de Dados, veja [Iniciar o Monitor de Espelhamento de Banco de Dados &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/start-database-mirroring-monitor-sql-server-management-studio.md).  
  
-   Procedimentos armazenados do sistema  
  
     O conjunto a seguir de procedimentos armazenados do sistema permite que um administrador configure e gerencie limites de aviso em bancos de dados espelhados, um parceiro por vez.  
  
    |Procedimento|DESCRIÇÃO|  
    |---------------|-----------------|  
    |[sp_dbmmonitorchangealert &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorchangealert-transact-sql.md)|Adiciona ou altera limites de aviso para uma métrica especificada de desempenho de espelhamento.|  
    |[sp_dbmmonitorhelpalert &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorhelpalert-transact-sql.md)|Retorna informações sobre limites de aviso em uma ou todas as várias métricas de desempenho do monitor de espelhamento de banco de dados principal.|  
    |[sp_dbmmonitordropalert &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitordropalert-transact-sql.md)|Descarta o aviso de uma métrica de desempenho especificada.|  
  
## <a name="performance-threshold-events-sent-to-the-windows-event-log"></a>Eventos de limite de desempenho enviados para o log de eventos do Windows  
 Se o limite de aviso for definido para uma métrica de desempenho, quando a tabela de status for atualizada, o valor mais recente será avaliado com relação ao limite. Se o limite tiver sido alcançado, o procedimento de atualização **sp_dbmmonitorupdate** gerará um evento informativo, um *evento do limite de desempenho*, para a métrica e gravará o evento no log de eventos do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows. A tabela a seguir lista as IDs de evento dos eventos de limite de desempenho.  
  
|Métrica de desempenho|ID do evento|  
|------------------------|--------------|  
|Log não enviado|32042|  
|Log não restaurado|32043|  
|Transação não enviada mais antiga|32040|  
|Sobrecarga espelhada confirmada|32044|  
  
> [!NOTE]  
>  Um administrador pode definir alertas em qualquer um ou mais desses eventos. Para obter mais informações, consulte [Usando alertas para um banco de dados espelhado](#UseAlerts), mais adiante neste  
>   
>  tópico.  
  
##  <a name="using-alerts-for-a-mirrored-database"></a><a name="UseAlerts"></a> Usando alertas para um banco de dados espelho  
 Uma parte importante do monitoramento de um banco de dados espelhado é a configuração de alertas sobre eventos importantes de espelhamento de banco de dados. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gera os seguintes tipos de eventos de espelhamento de banco de dados:  
  
-   Eventos de limite de desempenho  
  
     Para obter mais informações, consulte "Eventos de limite de desempenho enviados para o log de eventos do Windows", anteriormente neste tópico.  
  
-   Eventos de alteração de estado  
  
     Esses são eventos WMI (Windows Management Instrumentation) gerados quando ocorrem alterações no estado interno de uma sessão de espelhamento de banco de dados.  
  
    > [!NOTE]  
    >  Para obter mais informações, veja [Provedor WMI para conceitos de eventos de servidor](../../relational-databases/wmi-provider-server-events/wmi-provider-for-server-events-concepts.md).  
  
 Um administrador de sistema pode configurar alertas nesses eventos com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent ou outros aplicativos, como o [!INCLUDE[msCoName](../../includes/msconame-md.md)] Operations Manager.  
  
 Quando você define alertas em eventos de espelhamento de banco de dados, recomendamos que defina limites de aviso e alertas em ambas as instâncias do servidor parceiro. Eventos individuais são gerados no servidor principal ou no servidor espelho, mas cada parceiro pode executar qualquer uma dessas funções a qualquer momento. Para garantir que um alerta continue operando depois de um failover, o alerta deve ser definido em ambos os parceiros.  
  
> [!IMPORTANT]  
>  Para todas a sessões de espelhamento, é altamente recomendável que você configure o banco de dados para enviar um alerta em qualquer evento de alteração de estado. A menos que uma alteração de estado seja esperada como resultado de uma alteração de configuração manual, algo ocorreu que pode comprometer seus dados. Para ajudar a proteger seus dados, identifique e repare a causa de uma alteração de estado imprevista.  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> Tarefas relacionadas  
 **Para criar um alerta com o SQL Server Management Studio**  
  
-   [Criar um alerta usando um número de erro](../../ssms/agent/create-an-alert-using-an-error-number.md)  
  
-   [Criar um alerta de eventos WMI](../../ssms/agent/create-a-wmi-event-alert.md)  
  
 **Para monitorar o espelhamento de banco de dados**  
  
-   [Iniciar o Monitor de Espelhamento de Banco de Dados &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/start-database-mirroring-monitor-sql-server-management-studio.md)  
  
-   [sp_dbmmonitoraddmonitoring &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitoraddmonitoring-transact-sql.md)  
  
-   [sp_dbmmonitorchangealert &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorchangealert-transact-sql.md)  
  
-   [sp_dbmmonitorchangemonitoring &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorchangemonitoring-transact-sql.md)  
  
-   [sp_dbmmonitordropalert &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitordropalert-transact-sql.md)  
  
-   [sp_dbmmonitordropmonitoring &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitordropmonitoring-transact-sql.md)  
  
-   [sp_dbmmonitorhelpalert &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorhelpalert-transact-sql.md)  
  
-   [sp_dbmmonitorhelpmonitoring &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorhelpmonitoring-transact-sql.md)  
  
-   [sp_dbmmonitorresults &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorresults-transact-sql.md)  
  
-   [sp_dbmmonitorupdate &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorupdate-transact-sql.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)   
 [Monitorando o espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/monitoring-database-mirroring-sql-server.md)  
  
  
