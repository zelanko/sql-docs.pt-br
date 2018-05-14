---
title: Excluir linhas duplicadas (Ferramentas de Banco de Dados Visual) | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 3353bcc208de8fb73a135bb7370e24cbec135ba1
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="exclude-duplicate-rows-visual-database-tools"></a>Excluir linhas duplicadas (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Para exibir apenas os valores exclusivos de um conjunto de resultados, você poderá especificar que deseja excluir duplicatas do conjunto de resultados.  
  
### <a name="to-exclude-duplicate-rows-from-the-result-set"></a>Para excluir linhas duplicadas do conjunto de resultados  
  
1.  Clique com o botão direito do mouse na tela de fundo do Painel de Diagrama e escolha **Propriedades** no menu de atalho.  
  
2.  Na janela Propriedades, clique em **Valores Distintos** e defina o valor como **Sim**.  
  
    O Designer de Consulta e Exibição insere a palavra-chave DISTINCT diante da lista de colunas exibidas da instrução SQL.  
  
    > [!NOTE]  
    > Usar a palavra-chave DISTINCT talvez o impeça de modificar o conjunto de resultados no painel de resultados.  
  
## <a name="see-also"></a>Consulte Também  
[Especificar critérios de pesquisa &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md)  
[Classificar e agrupar resultados da consulta &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/sort-and-group-query-results-visual-database-tools.md)  
  
