---
title: Visão geral do SQL Server Monitor | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- sql13.swb.sqlservermonitor.main.f1
helpviewer_keywords:
- SQL Server Monitor [SQL Server]
ms.assetid: 048ae16d-31c3-489a-9f1e-1400a3bacd39
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: a6f5e2b2bcd92c0a17ccada2ca755cbc14b9d647
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68032493"
---
# <a name="sql-server-monitor-overview"></a>Visão geral do SQL Server Monitor
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  O SQL Server Monitor não realiza funções de monitoramento, mas hospeda módulos que as realizam. Os módulos do SQL Server Monitor incluem o Replication Monitor e o Monitor de Espelhamento de Banco de Dados.  
  
 Para usar um desses módulos, selecione o módulo no menu **Ir** . O módulo presentemente selecionado possui o conteúdo de navegação e os painéis de detalhes, interação de usuário nos painéis de detalhes e as consultas de conteúdo e status.  
  
> [!NOTE]  
>  Para obter mais informações sobre esses monitores, consulte [Replicação de monitoramento](../../relational-databases/replication/monitor/monitoring-replication.md) e [Monitorando o espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/monitoring-database-mirroring-sql-server.md).  
  
## <a name="permissions"></a>Permissões  
  
-   Replication Monitor  
  
     Para monitorar a replicação é preciso ser membro da função de servidor fixa **sysadmin** no Distribuido ou membro da função de banco de dados fixa **replmonitor** no banco de dados de distribuição. Um administrador de sistema pode adicionar qualquer usuário à função **replmonitor** , o que permite que o usuário exiba a atividade de replicação no Replication Monitor. No entanto, o usuário não pode administrar a replicação.  
  
-   Monitor de Espelhamento de Banco de Dados  
  
     Para monitorar um espelhamento de banco de dados, é preciso ser membro da função de servidor fixa **sysadmin** ou da função de banco de dados fixa **dbm_monitor** na instância do servidor. Se você for um membro do **sysadmin** ou do **dbm_monitor** em apenas uma das instâncias do servidor parceiro, o monitor poderá se conectar apenas àquele parceiro e não poderá recuperar as informações do outro parceiro. Para obter mais informações, consulte [Database Mirroring Monitor Overview](../../database-engine/database-mirroring/database-mirroring-monitor-overview.md).  
  
## <a name="menu-options"></a>Menu Opções  
 O SQL Server Monitor possui um menu que contém comandos que pertencem ao SQL Server Monitor. Esse menu pode igualmente conter comandos do módulo selecionado.  
  
 As opções de menu a seguir pertencem ao SQL Server Monitor.  
  
 **File**  
 Esse menu contém o comando **Sair** .  
  
 **Ação**  
 Contém o menu de contexto do nó selecionado na árvore de navegação.  
  
 **Ir**  
 Contém uma lista de componentes de monitoramento:  
  
-   Espelhamento de banco de dados  
  
-   Replicação  
  
 **Para usar o SQL Server Management Studio para monitorar o espelhamento de banco de dados**  
  
-   [Iniciar o Monitor de Espelhamento de Banco de Dados &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/start-database-mirroring-monitor-sql-server-management-studio.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Monitorando o espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/monitoring-database-mirroring-sql-server.md)  
  
  
