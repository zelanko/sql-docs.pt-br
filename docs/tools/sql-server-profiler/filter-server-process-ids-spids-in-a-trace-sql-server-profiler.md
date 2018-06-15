---
title: Filtrar SPIDs (IDs de processo do servidor) em um rastreamento (SQL Server Profiler) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.suite: sql
ms.technology: profiler
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- filters [SQL Server], traces
- filters [SQL Server], SPIDs
- traces [SQL Server], filters
ms.assetid: f5945c39-be6b-4632-91cb-92066c80e188
caps.latest.revision: 25
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 5f70625ce37e2409e3a885e9c62ff4be227b3707
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33072505"
---
# <a name="filter-server-process-ids-spids-in-a-trace-sql-server-profiler"></a>Filtrar IDs de processo de servidor em um rastreamento (SQL Server Profiler)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Este tópico descreve como filtrar identificadores de processo de servidor (SPIDs) em um rastreamento, usando o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)].  
  
### <a name="to-filter-system-ids-in-a-trace"></a>Para filtrar IDs de sistema em um rastreamento  
  
1.  No menu **Arquivo** , clique em **Novo Rastreamento**e conecte a uma instância do SQL Server.  
  
     É exibida a caixa de diálogo **Propriedades do Rastreamento** .  
  
    > [!NOTE]  
    >  Se a opção **Iniciar rastreamento imediatamente depois de estabelecer a conexão** estiver selecionada, a caixa de diálogo **Propriedades do Rastreamento** não será exibida e o rastreamento será iniciado. Para desabilitar essa configuração, no menu **Ferramentas**, clique em **Opções** e desmarque a caixa de seleção **Iniciar rastreamento imediatamente depois de estabelecer a conexão**.  
  
2.  Na caixa **Nome do rastreamento** , digite um nome para o rastreamento.  
  
3.  Na lista de nomes **Usar o modelo**, selecione um modelo de rastreamento.  
  
4.  Opcionalmente, especifique um arquivo ou tabela de destino onde os resultados do rastreamento serão salvos.  
  
5.  Na guia **Seleção de Eventos**, clique no título de coluna **SPID** para iniciar a caixa de diálogo **Editar Filtro**. Você também pode clicar com o botão direito do mouse no título de coluna e selecionar **Editar Filtro de Coluna**. Se a coluna **SPID** não aparecer, marque a caixa **Mostrar todas as colunas** .  
  
6.  Na caixa de diálogo **Editar Filtro** , expanda o operador de comparação apropriado e insira um SPID como valor de comparação.  
  
## <a name="see-also"></a>Consulte Também  
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
