---
title: Excluir linhas duplicadas (Ferramentas de Banco de Dados Visual) | Microsoft Docs
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
- search criteria [SQL Server], excluding rows
- row duplicates [SQL Server]
- duplicate rows
- row excluded in search [SQL Server]
- result sets [SQL Server], duplicate values
- excluding rows
ms.assetid: ab35a363-421d-4665-946b-ae3f6397af50
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: bad0e2729b2a0bfa0728d9257194c4adb10a885e
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="exclude-duplicate-rows-visual-database-tools"></a>Excluir linhas duplicadas (Visual Database Tools)
Para exibir apenas os valores exclusivos de um conjunto de resultados, você poderá especificar que deseja excluir duplicatas do conjunto de resultados.  
  
### <a name="to-exclude-duplicate-rows-from-the-result-set"></a>Para excluir linhas duplicadas do conjunto de resultados  
  
1.  Clique com o botão direito do mouse na tela de fundo do Painel de Diagrama e escolha **Propriedades** no menu de atalho.  
  
2.  Na janela Propriedades, clique em **Valores Distintos** e defina o valor como **Sim**.  
  
    O Designer de Consulta e Exibição insere a palavra-chave DISTINCT diante da lista de colunas exibidas da instrução SQL.  
  
    > [!NOTE]  
    > Usar a palavra-chave DISTINCT talvez o impeça de modificar o conjunto de resultados no painel de resultados.  
  
## <a name="see-also"></a>Consulte também  
[Especificar critérios de pesquisa &amp;#40;Visual Database Tools&amp;#41;](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md)  
[Classificar e agrupar resultados da consulta &amp;#40;Visual Database Tools&amp;#41;](../../ssms/visual-db-tools/sort-and-group-query-results-visual-database-tools.md)  
  

