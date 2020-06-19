---
title: Excluir linhas duplicadas (Ferramentas de Banco de Dados Visual) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- search criteria [SQL Server], excluding rows
- row duplicates [SQL Server]
- duplicate rows
- row excluded in search [SQL Server]
- result sets [SQL Server], duplicate values
- excluding rows
ms.assetid: ab35a363-421d-4665-946b-ae3f6397af50
author: stevestein
ms.author: sstein
ms.openlocfilehash: 3b396f2738f6895684d828884d4822ea9165e0a9
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85054599"
---
# <a name="exclude-duplicate-rows-visual-database-tools"></a>Excluir linhas duplicadas (Visual Database Tools)
  Para exibir apenas os valores exclusivos de um conjunto de resultados, você poderá especificar que deseja excluir duplicatas do conjunto de resultados.  
  
### <a name="to-exclude-duplicate-rows-from-the-result-set"></a>Para excluir linhas duplicadas do conjunto de resultados  
  
1.  Clique com o botão direito do mouse na tela de fundo do Painel de Diagrama e escolha **Propriedades** no menu de atalho.  
  
2.  Na janela Propriedades, clique em **Valores Distintos** e defina o valor como **Sim**.  
  
     O Designer de Consulta e Exibição insere a palavra-chave DISTINCT diante da lista de colunas exibidas da instrução SQL.  
  
    > [!NOTE]  
    >  Usar a palavra-chave DISTINCT talvez o impeça de modificar o conjunto de resultados no painel de resultados.  
  
## <a name="see-also"></a>Consulte Também  
 [Especificar critérios de pesquisa &#40;Visual Database Tools&#41;](visual-database-tools.md)   
 [Classificar e agrupar resultados da consulta &#40;Visual Database Tools&#41;](sort-and-group-query-results-visual-database-tools.md)  
  
  
