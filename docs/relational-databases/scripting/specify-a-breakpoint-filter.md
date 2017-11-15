---
title: "Especificar um filtro de ponto de interrupção | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: vs.debug.breakpt.contraints
helpviewer_keywords: Transact-SQL debugger, breakpoint filter
ms.assetid: 7bf1dddd-7b0b-4c47-8a7b-28a5569b4fa5
caps.latest.revision: "6"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 242653e9766535cb5282b3cabdf3850e5b0f96be
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="specify-a-breakpoint-filter"></a>Especificar um filtro de ponto de interrupção
  Um filtro de ponto de interrupção limita o ponto de interrupção para atuar somente em computadores, sistemas operacionais, processos e threads especificados. Filtros de ponto de interrupção são normalmente usados ao depurar aplicativos paralelos.  
  
##  <a name="BKMK_ActionConsiderations"></a> Considerações sobre filtros  
 Filtros de ponto de interrupção não são normalmente usados com o depurador [!INCLUDE[tsql](../../includes/tsql-md.md)] porque os scripts [!INCLUDE[tsql](../../includes/tsql-md.md)] e os procedimentos armazenados não são aplicativos paralelos.  
  
#### <a name="to-specify-a-breakpoint-filter"></a>Para especificar um filtro de ponto de interrupção  
  
1.  Na janela do editor, clique com o botão direito do mouse no glifo do ponto de interrupção e clique em **Filtro** no menu de atalho.  
  
     -ou-  
  
     Na janela **Pontos de Interrupção** , clique com o botão direito do mouse no glifo do ponto de interrupção e clique em **Filtro** no menu de atalho.  
  
2.  Na caixa de diálogo **Filtros de Ponto de Interrupção** , use a caixa **Filtro** para especificar computadores por nome ou processos e threads do sistema operacional por nome ou número da ID:  
  
    -   **MachineName** é o computador que está executando a instância do Mecanismo de Banco de Dados.  
  
    -   **ProcessID**e **ProcessName** são o processo do sistema operacional que executa a instância do Mecanismo de Banco de Dados.  
  
    -   **ThreadID** e **ThreadName** são o thread do sistema operacional que executa o lote [!INCLUDE[tsql](../../includes/tsql-md.md)] , procedimento ou função na instância do Mecanismo de Banco de Dados.  
  
3.  Clique em **OK** para implementar as alterações ou em **Cancelar** para sair sem aplicar as alterações.  
  
## <a name="see-also"></a>Consulte também  
 [Especificar uma condição de ponto de interrupção](../../relational-databases/scripting/specify-a-breakpoint-condition.md)   
 [Especificar uma contagem de ocorrências](../../relational-databases/scripting/specify-a-hit-count.md)   
 [Especificar uma ação de ponto de interrupção](../../relational-databases/scripting/specify-a-breakpoint-action.md)  
  
  
