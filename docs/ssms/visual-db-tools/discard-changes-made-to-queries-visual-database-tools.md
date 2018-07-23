---
title: Descartar alterações feitas em consultas (Ferramentas de Banco de Dados Visual) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssms-visual-db
ms.reviewer: ''
ms.suite: sql
ms.technology: ssms
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- reverting queries
- queries [SQL Server], discarding changes
- discarding query changes
ms.assetid: 7bb17ece-1222-4622-b476-5789d7641c64
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 4a328d434b06f785fd5d2e3816c635dc7c039e78
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38053216"
---
# <a name="discard-changes-made-to-queries-visual-database-tools"></a>Descartar alterações feitas em consultas (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Você pode descartar alterações feitas em definições de consulta antes de salvá-las. Depois de salvas, as alterações não podem ser retornadas ao estado anterior.  
  
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
  
