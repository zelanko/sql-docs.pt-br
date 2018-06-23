---
title: Excluir linhas duplicadas (Ferramentas de Banco de Dados Visual) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- search criteria [SQL Server], excluding rows
- row duplicates [SQL Server]
- duplicate rows
- row excluded in search [SQL Server]
- result sets [SQL Server], duplicate values
- excluding rows
ms.assetid: ab35a363-421d-4665-946b-ae3f6397af50
caps.latest.revision: 10
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 017385370989983d37f045379de926d0ebbf333f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36130688"
---
# <a name="exclude-duplicate-rows-visual-database-tools"></a>Excluir linhas duplicadas (Visual Database Tools)
  Para exibir apenas os valores exclusivos de um conjunto de resultados, você poderá especificar que deseja excluir duplicatas do conjunto de resultados.  
  
### <a name="to-exclude-duplicate-rows-from-the-result-set"></a>Para excluir linhas duplicadas do conjunto de resultados  
  
1.  Clique com o botão direito do mouse na tela de fundo do Painel de Diagrama e escolha **Propriedades** no menu de atalho.  
  
2.  Na janela Propriedades, clique em **Valores Distintos** e defina o valor como **Sim**.  
  
     O Designer de Consulta e Exibição insere a palavra-chave DISTINCT diante da lista de colunas exibidas da instrução SQL.  
  
    > [!NOTE]  
    >  Usar a palavra-chave DISTINCT talvez o impeça de modificar o conjunto de resultados no painel de resultados.  
  
## <a name="see-also"></a>Consulte também  
 [Especificar critérios de pesquisa &#40;Visual Database Tools&#41;](visual-database-tools.md)   
 [Classificar e agrupar resultados da consulta &#40;Visual Database Tools&#41;](sort-and-group-query-results-visual-database-tools.md)  
  
  