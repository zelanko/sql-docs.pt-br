---
title: Visão geral do SQL Server Monitor | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.swb.sqlservermonitor.main.f1
helpviewer_keywords:
- SQL Server Monitor [SQL Server]
ms.assetid: 048ae16d-31c3-489a-9f1e-1400a3bacd39
caps.latest.revision: 21
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: cb4f90846fa3f51906815a7bff54a29d21fa86d6
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36010745"
---
# <a name="sql-server-monitor-overview"></a>Visão geral do SQL Server Monitor
  O SQL Server Monitor não realiza funções de monitoramento, mas hospeda módulos que as realizam. Os módulos do SQL Server Monitor incluem o Replication Monitor e o Monitor de Espelhamento de Banco de Dados.  
  
 Para usar um desses módulos, selecione o módulo no menu **Ir** . O módulo presentemente selecionado possui o conteúdo de navegação e os painéis de detalhes, interação de usuário nos painéis de detalhes e as consultas de conteúdo e status.  
  
> [!NOTE]  
>  Para obter mais informações sobre esses monitores, consulte [Replicação de monitoramento](../../relational-databases/replication/monitoring-replication.md) e [Monitorando o espelhamento de banco de dados &#40;SQL Server&#41;](../database-mirroring/database-mirroring-sql-server.md).  
  
## <a name="permissions"></a>Permissões  
  
-   Replication Monitor  
  
     Para monitorar a replicação é preciso ser membro da função de servidor fixa **sysadmin** no Distribuido ou membro da função de banco de dados fixa **replmonitor** no banco de dados de distribuição. Um administrador de sistema pode adicionar qualquer usuário à função **replmonitor** , o que permite que o usuário exiba a atividade de replicação no Replication Monitor. No entanto, o usuário não pode administrar a replicação.  
  
-   Monitor de Espelhamento de Banco de Dados  
  
     Para monitorar um espelhamento de banco de dados, é preciso ser membro da função de servidor fixa **sysadmin** ou da função de banco de dados fixa **dbm_monitor** na instância do servidor. Se você for um membro do **sysadmin** ou do **dbm_monitor** em apenas uma das instâncias do servidor parceiro, o monitor poderá se conectar apenas àquele parceiro e não poderá recuperar as informações do outro parceiro. Para obter mais informações, consulte [Database Mirroring Monitor Overview](../database-mirroring/database-mirroring-monitor-overview.md).  
  
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
  
-   [Iniciar o Monitor de Espelhamento de Banco de Dados &#40;SQL Server Management Studio&#41;](../database-mirroring/start-database-mirroring-monitor-sql-server-management-studio.md)  
  
## <a name="see-also"></a>Consulte também  
 [Monitorando o espelhamento de banco de dados &#40;SQL Server&#41;](../database-mirroring/database-mirroring-sql-server.md)  
  
  