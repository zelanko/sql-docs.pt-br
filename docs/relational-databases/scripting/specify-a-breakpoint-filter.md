---
title: "Especificar um filtro de ponto de interrupção | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- vs.debug.breakpt.contraints
helpviewer_keywords:
- Transact-SQL debugger, breakpoint filter
ms.assetid: 7bf1dddd-7b0b-4c47-8a7b-28a5569b4fa5
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a209cf9781830ae75a1a726a002ba4077cd8b96d
ms.sourcegitcommit: a0aa5e611a0e6ebb74ac1e2f613e8916dc7a7617
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/24/2018
---
# <a name="specify-a-breakpoint-filter"></a>Especificar um filtro de ponto de interrupção
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] Um filtro de ponto de interrupção limita o ponto de interrupção para atuar somente em computadores, sistemas operacionais, processos e threads especificados. Filtros de ponto de interrupção são normalmente usados ao depurar aplicativos paralelos.  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [Especificar uma condição de ponto de interrupção](../../relational-databases/scripting/specify-a-breakpoint-condition.md)   
 [Especificar uma contagem de ocorrências](../../relational-databases/scripting/specify-a-hit-count.md)   
 [Especificar uma ação de ponto de interrupção](../../relational-databases/scripting/specify-a-breakpoint-action.md)  
  
  
