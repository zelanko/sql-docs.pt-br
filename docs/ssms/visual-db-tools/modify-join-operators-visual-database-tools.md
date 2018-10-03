---
title: Modificar operadores de junção (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- joins [SQL Server], operators
- modifying join operators
- join operators
ms.assetid: d1dcdcfd-166c-4147-85ab-43cadc63819b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0862cc4baffd68b42723ff4037e48613170d488d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47768204"
---
# <a name="modify-join-operators-visual-database-tools"></a>Modificar operadores de junção (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Por padrão, o [Designer de Consulta e Exibição](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md) une tabelas que usam um sinal de igual (um equijoin), o qual faz corresponder valores nas duas colunas de junção. Se desejar, você pode alterar o operador usado para comparar valores nas colunas de junção.  
  
### <a name="to-modify-join-operators"></a>Para modificar operadores de junção  
  
1.  No [painel de Diagrama](../../ssms/visual-db-tools/diagram-pane-visual-database-tools.md), clique com o botão direito do mouse na linha de junção que deseja modificar e escolha **Propriedades** no menu de atalho.  
  
2.  Na janela Propriedades, clique em **Condição e Tipo de Junção** e clique nas **reticências (...)** à direita da propriedade.  
  
3.  Na caixa de diálogo **Junção** , selecione um novo operador.  
  
## <a name="see-also"></a>Consulte Também  
[Unir tabelas automaticamente &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/join-tables-automatically-visual-database-tools.md)  
[Unir tabelas manualmente &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/join-tables-manually-visual-database-tools.md)  
[Consultar com junções &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/query-with-joins-visual-database-tools.md)  
  
