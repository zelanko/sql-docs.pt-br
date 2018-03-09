---
title: Filtrar IDs de processo do servidor (SPIDs) em um rastreamento (SQL Server Profiler) | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: sql-server-profiler
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- filters [SQL Server], traces
- filters [SQL Server], SPIDs
- traces [SQL Server], filters
ms.assetid: f5945c39-be6b-4632-91cb-92066c80e188
caps.latest.revision: "25"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 67926fa0506f797c4f39988061c4d1b7b731e5fa
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/17/2018
---
# <a name="filter-server-process-ids-spids-in-a-trace-sql-server-profiler"></a>Filtrar IDs de processo de servidor em um rastreamento (SQL Server Profiler)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]Este tópico descreve como filtrar identificadores de processo do servidor (SPIDs) em um rastreamento usando [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)].  
  
### <a name="to-filter-system-ids-in-a-trace"></a>Para filtrar IDs de sistema em um rastreamento  
  
1.  No menu **Arquivo** , clique em **Novo Rastreamento**e conecte a uma instância do SQL Server.  
  
     É exibida a caixa de diálogo **Propriedades do Rastreamento** .  
  
    > [!NOTE]  
    >  Se **Iniciar rastreamento imediatamente após estabelecer a conexão** for selecionada, o **propriedades do rastreamento** caixa de diálogo não será exibida e o rastreamento será iniciado. Para desabilitar essa configuração, no **ferramentas** menu, clique em **opções**e desmarque o **Iniciar rastreamento imediatamente após estabelecer a conexão** caixa de seleção.  
  
2.  Na caixa **Nome do rastreamento** , digite um nome para o rastreamento.  
  
3.  No **usar o modelo** lista de nomes, selecione um modelo de rastreamento.  
  
4.  Opcionalmente, especifique um arquivo ou tabela de destino onde os resultados do rastreamento serão salvos.  
  
5.  No **seleção de eventos** , clique no **SPID** cabeçalho da coluna para iniciar o **Editar filtro** caixa de diálogo. Você também pode clicar com o botão direito do mouse no título de coluna e selecionar **Editar Filtro de Coluna**. Se a coluna **SPID** não aparecer, marque a caixa **Mostrar todas as colunas** .  
  
6.  Na caixa de diálogo **Editar Filtro** , expanda o operador de comparação apropriado e insira um SPID como valor de comparação.  
  
## <a name="see-also"></a>Consulte também  
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
