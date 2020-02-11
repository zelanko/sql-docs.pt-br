---
title: Especificar um filtro de ponto de interrupção
ms.custom: seo-lt-2019
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Transact-SQL debugger, breakpoint filter
ms.assetid: 7bf1dddd-7b0b-4c47-8a7b-28a5569b4fa5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a9759134504c7b55f5008783a2e6c3bd9ebf1755
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "75243219"
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
  
    -   
  `MachineName` é o computador que está executando a instância do Mecanismo de Banco de Dados.  
  
    -   
  `ProcessID` e `ProcessName` são o processo do sistema operacional que executa a instância do Mecanismo de Banco de Dados.  
  
    -   
  `ThreadID` e `ThreadName` são o thread do sistema operacional que executa o lote [!INCLUDE[tsql](../../includes/tsql-md.md)], procedimento ou função na instância do Mecanismo de Banco de Dados.  
  
3.  Clique em **OK** para implementar as alterações ou em **Cancelar** para sair sem aplicar as alterações.  
  
## <a name="see-also"></a>Consulte Também  
 [Especificar uma condição de ponto de interrupção](specify-a-breakpoint-condition.md)   
 [Especificar uma contagem de ocorrências](specify-a-hit-count.md)   
 [Especificar uma ação de ponto de interrupção](specify-a-breakpoint-action.md)  
