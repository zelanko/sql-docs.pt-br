---
title: Sondar servidores | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- target servers [SQL Server], polling interval
- polling master servers [SQL Server]
- server polling [SQL Server]
- master servers [SQL Server], polling
- polling interval [SQL Server]
ms.assetid: 96f5fd43-3edd-4418-9dd0-4d34e618890e
author: markingmyname
ms.author: maghan
manager: jroth
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: fd5018d5e969ad40643e0767290d53a6ba40c8f4
ms.sourcegitcommit: 5d839dc63a5abb65508dc498d0a95027d530afb6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/09/2019
ms.locfileid: "67685479"
---
# <a name="poll-servers"></a>Sondar servidores
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> No momento, na [Instância Gerenciada do Banco de Dados SQL do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), a maioria dos recursos do SQL Server Agent é compatível, mas não todos. Consulte [Azure SQL Database Managed Instance T-SQL differences from SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) (Diferenças entre o T-SQL da Instância Gerenciada do Banco de Dados SQL do Azure e o SQL Server) para obter detalhes.

Quando é implementada administração multisservidor, os servidores de destino contatam periodicamente o servidor mestre para carregar informações sobre trabalhos executados e baixar novos trabalhos. O processo de contatar o servidor mestre é chamado de *sondagem de servidor* , que acontece em *intervalos de sondagem*regulares.  
  
## <a name="polling-intervals"></a>Intervalos de sondagem  
O intervalo de sondagem (um minuto, por padrão) controla a frequência com que o servidor de destino se conecta ao servidor mestre para baixar instruções e carregar os resultados da execução de trabalhos.  
  
Quando um servidor de destino sonda o servidor mestre, ele lê as operações atribuídas a si na tabela **sysdownloadlist** do banco de dados **msdb** . Essas operações controlam trabalhos multisservidor e diversos aspectos do comportamento de um servidor de destino. São exemplos dessas operações a exclusão, inserção ou início de um trabalho e a atualização do intervalo de sondagem de um servidor de destino.  
  
As operações são postadas na tabela **sysdownloadlist** , de um destes modos:  
  
-   Explicitamente, usando o procedimento armazenado **sp_post_msx_operation** .  
  
-   Implicitamente, usando outros procedimentos armazenados de trabalho.  
  
Se usar procedimentos armazenados de trabalho para modificar agendas ou etapas de trabalho multisservidor ou se usar o SQL Distributed Management Objects (SQL-DMO) para controlar trabalhos multisservidor, emita o seguinte comando após efetuar as modificações nas agendas ou etapas de trabalho:  
  
```  
EXECUTE msdb.dbo.sp_post_msx_operation 'INSERT', 'JOB', '<job id>'  
```  
  
Emitir este comando mantém os servidores de destino sincronizados com a definição de trabalho atual.  
  
Se você usar os seguintes itens, não será necessário postar operações explicitamente:  
  
-   O Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] , para controlar trabalhos multisservidor.  
  
-   Procedimentos armazenados de trabalho que não modificam agendas nem etapas de trabalho.  
  
**Para forçar um servidor de destino a sondar o servidor mestre**  
  
-   [SQL Server Management Studio](../../ssms/agent/force-a-target-server-to-poll-the-master-server.md)  
  
-   [Transact-SQL](https://msdn.microsoft.com/085deef8-2709-4da9-bb97-9ab32effdacf)  
  
## <a name="see-also"></a>Consulte Também  
[Gerenciar eventos](../../ssms/agent/manage-events.md)  
  
