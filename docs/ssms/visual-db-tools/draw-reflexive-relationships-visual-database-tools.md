---
title: "Desenhar relações reflexivas (Ferramentas de Banco de Dados Visual) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- drawing reflexive relationships
- reflexive relationships
- database diagrams [SQL Server], relationships
ms.assetid: e218363f-faec-46d5-9904-a537fbcc994d
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: b3f92a8f199bf03ff3a9c0cff4aedfb8a138ebec
ms.contentlocale: pt-br
ms.lasthandoff: 04/11/2017

---
# <a name="draw-reflexive-relationships-visual-database-tools"></a>Desenhar relações reflexivas (Visual Database Tools)
Você cria uma relação reflexiva para vincular uma coluna ou colunas em uma tabela com outra coluna ou colunas na mesma tabela. Por exemplo, suponha que a tabela `employee` tenha uma coluna `emp_id` e uma coluna `mgr_id` . Em razão de  cada administrador também ser um funcionário, você relaciona estas duas colunas desenhando uma relação da tabela para si mesmo. Esta relação garante que cada ID de gerente ID acrescentada à tabela corresponda a uma ID de funcionário existente.  
  
Antes de criar uma relação, você deve primeiro definir uma chave primária ou restrição exclusiva para sua tabela. Você então relaciona a coluna de chave primária a uma coluna correspondente. Quando você cria a relação, a coluna correspondente se torna uma chave estrangeira da tabela.  
  
### <a name="to-draw-a-reflexive-relationship"></a>Para desenhar uma relação reflexiva  
  
1.  Em seu diagrama de banco de dados, clique no seletor de linhas para a coluna de banco de dados que você quer relacionar a outra coluna e arraste o ponteiro para fora da tabela até que uma linha apareça.  
  
2.  Arraste a linha de volta à tabela selecionada.  
  
3.  Solte o botão do mouse. A caixa de diálogo **Tabelas e Colunas** aparece.  
  
4.  Selecione a coluna de chave estrangeira e a tabela de chave primária e a coluna com a qual você quer formar uma relação.  
  
5.  Clique em **OK** duas vezes para criar a relação.  
  
Quando você executar consultas em uma tabela, você pode usar uma relação reflexiva para criar uma autojunção. Para obter informações sobre como consultar tabelas com junções, veja [Query with Joins &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/query-with-joins-visual-database-tools.md).  
  
## <a name="see-also"></a>Consulte também  
[Consultar com junções &amp;#40;Visual Database Tools&amp;#41;](../../ssms/visual-db-tools/query-with-joins-visual-database-tools.md)  
  

