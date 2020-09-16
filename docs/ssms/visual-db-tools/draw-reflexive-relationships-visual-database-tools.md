---
description: Desenhar relações reflexivas (Visual Database Tools)
title: Traçar relacionamentos reflexivos
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- drawing reflexive relationships
- reflexive relationships
- database diagrams [SQL Server], relationships
ms.assetid: e218363f-faec-46d5-9904-a537fbcc994d
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: 2472266ae29470b19f93518676e75f8ff17d86ed
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88480038"
---
# <a name="draw-reflexive-relationships-visual-database-tools"></a>Desenhar relações reflexivas (Visual Database Tools)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
Você cria uma relação reflexiva para vincular uma coluna ou colunas em uma tabela com outra coluna ou colunas na mesma tabela. Por exemplo, suponha que a tabela `employee` tenha uma coluna `emp_id` e uma coluna `mgr_id` . Em razão de  cada administrador também ser um funcionário, você relaciona estas duas colunas desenhando uma relação da tabela para si mesmo. Esta relação garante que cada ID de gerente ID acrescentada à tabela corresponda a uma ID de funcionário existente.  
  
Antes de criar uma relação, você deve primeiro definir uma chave primária ou restrição exclusiva para sua tabela. Você então relaciona a coluna de chave primária a uma coluna correspondente. Quando você cria a relação, a coluna correspondente se torna uma chave estrangeira da tabela.  
  
### <a name="to-draw-a-reflexive-relationship"></a>Para desenhar uma relação reflexiva  
  
1.  Em seu diagrama de banco de dados, clique no seletor de linhas para a coluna de banco de dados que você quer relacionar a outra coluna e arraste o ponteiro para fora da tabela até que uma linha apareça.  
  
2.  Arraste a linha de volta à tabela selecionada.  
  
3.  Solte o botão do mouse. A caixa de diálogo **Tabelas e Colunas** aparece.  
  
4.  Selecione a coluna de chave estrangeira e a tabela de chave primária e a coluna com a qual você quer formar uma relação.  
  
5.  Clique em **OK** duas vezes para criar a relação.  
  
Quando você executar consultas em uma tabela, você pode usar uma relação reflexiva para criar uma autojunção. Para obter informações sobre como consultar tabelas com junções, veja [Consultar com junções &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/query-with-joins-visual-database-tools.md).  
  
## <a name="see-also"></a>Consulte Também  
[Consultar com junções &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/query-with-joins-visual-database-tools.md)  
  
