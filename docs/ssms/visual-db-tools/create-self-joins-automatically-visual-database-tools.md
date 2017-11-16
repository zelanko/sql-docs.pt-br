---
title: "Criar autojunções automaticamente (Visual Database Tools) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- automatic joins
- self-joins
- joins [SQL Server], self
ms.assetid: f9ec90e8-3aad-415c-a5c4-8dfa9540e37f
caps.latest.revision: "4"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 32bf78f4039967e3ecd9aa08084325edffc81104
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="create-self-joins-automatically-visual-database-tools"></a>Criar autojunções automaticamente (Visual Database Tools)
Se uma tabela tiver uma relação reflexiva no banco de dados, a autojunção poderá ocorrer automaticamente.  
  
### <a name="to-create-a-self-join-automatically"></a>Para criar uma autojunção automaticamente  
  
1.  Adicione ao [painel Diagrama](../../ssms/visual-db-tools/diagram-pane-visual-database-tools.md) a tabela com a qual deseja trabalhar.  
  
2.  Adicione a mesma tabela novamente, de forma que seja exibida a mesma tabela duas vezes no painel Diagrama.  
  
    O [Designer de Consulta e Exibição](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md) atribui um alias à segunda instância adicionando um número sequencial ao nome da tabela. Além disso, o Designer de Consulta e Exibição cria uma linha de junção entre os dois retângulos representando dois modos diferentes de participação da tabela na consulta.  
  
## <a name="see-also"></a>Consulte também  
[Consultar com junções &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/query-with-joins-visual-database-tools.md)  
  
