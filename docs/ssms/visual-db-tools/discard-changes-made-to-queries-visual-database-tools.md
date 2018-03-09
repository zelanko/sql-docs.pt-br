---
title: "Descartar alterações feitas em consultas (Ferramentas de Banco de Dados Visual) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-visual-db
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- reverting queries
- queries [SQL Server], discarding changes
- discarding query changes
ms.assetid: 7bb17ece-1222-4622-b476-5789d7641c64
caps.latest.revision: "4"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5412ede653f8bd6eb67091dd4ebc532b1d7f1b19
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/17/2018
---
# <a name="discard-changes-made-to-queries-visual-database-tools"></a>Descartar alterações feitas em consultas (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] Você pode descartar alterações feitas a uma definição de consulta antes de salvá-la. Depois de salvas, as alterações não podem ser retornadas ao estado anterior.  
  
> [!NOTE]  
> Para desfazer uma alteração feita em valores no painel Resultados, pressione a tecla ESC antes de sair do registro. Se você sair de um registro e receber a notificação de que as mudanças não serão confirmadas no banco de dados, você também poderá pressionar a tecla ESC para reverter ao valor anterior.  
  
### <a name="to-discard-changes-made-to-a-query-definition"></a>Para descartar alterações feitas em uma definição de consulta  
  
1.  Com a consulta aberta no Designer de Consulta e Exibição, no menu **Arquivo** , clique em **Fechar**.  
  
2.  Na caixa de diálogo **Microsoft SQL Server Management Studio** , clique em **Não**.  
  
    A definição de consulta retornará ao estado em que se encontrava na última vez em que foi salva.  
  
## <a name="see-also"></a>Consulte Também  
[Salvar consultas (Visual Database Tools)](../../ssms/visual-db-tools/save-queries-visual-database-tools.md)  
[Tópicos de instruções de como criar consultas e exibições (Ferramentas de Banco de Dados Visual)](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
[Realizar operações básicas com consultas (Ferramentas de Banco de Dados Visual)](../../ssms/visual-db-tools/perform-basic-operations-with-queries-visual-database-tools.md)  
[Trabalhar com dados no painel de resultados (Visual Database Tools)](../../ssms/visual-db-tools/work-with-data-in-the-results-pane-visual-database-tools.md)  
  
