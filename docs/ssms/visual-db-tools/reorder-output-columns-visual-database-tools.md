---
title: Reordenar colunas de saída
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- reordering output columns [SQL Server]
- output columns [SQL Server]
ms.assetid: 76462885-de4a-4290-a26b-90696d3671f4
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: f168b16ef5407b8ebf47e55f7062b1b7c8c7b180
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86008872"
---
# <a name="reorder-output-columns-visual-database-tools"></a>Reordenar colunas de saída (Visual Database Tools)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
A ordem na qual as colunas de dados são adicionadas a uma consulta Selecionar determina a ordem em que elas aparecerão nos resultados. A primeira coluna que você adicionar à consulta aparecerá na extremidade esquerda dos resultados, a segunda coluna ao lado, e assim por diante.  
  
Caso consultas Atualizar ou Consultar estejam sendo criadas, a ordem em que as colunas serão adicionadas afeta a ordem de processamento dos dados.  
  
Para controlar onde uma coluna de dados aparecerá no conjunto de resultados ou em que ordem será utlizada, reordene as colunas.  
  
### <a name="to-reorder-columns-for-output"></a>Par reordenar colunas para saída  
  
1.  No [Painel Critérios](../../ssms/visual-db-tools/criteria-pane-visual-database-tools.md), selecione a linha que contém a coluna clicando no botão de seletor de linha à esquerda da linha.  
  
2.  Aponte para o botão seletor de linha e arraste a linha para o novo local.  
  
    -ou-  
  
    Edite a ordem dos nomes da coluna no [Painel SQL](../../ssms/visual-db-tools/sql-pane-visual-database-tools.md).  
  
> [!TIP]  
> Você pode adicionar uma linha de dados a um local específico do Painel de Critérios, inserindo uma linha em branco no Painel de Critérios e especificando, em seguida, a coluna de dados a ser inserida. Para obter detalhes, veja [Adicionar colunas a consultas &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/add-columns-to-queries-visual-database-tools.md).  
  
## <a name="see-also"></a>Consulte Também  
[Classificar e agrupar resultados da consulta &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/sort-and-group-query-results-visual-database-tools.md)  
[Resumir resultados da consulta &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/summarize-query-results-visual-database-tools.md)  
[Executar operações básicas com consultas &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/perform-basic-operations-with-queries-visual-database-tools.md)  
  
