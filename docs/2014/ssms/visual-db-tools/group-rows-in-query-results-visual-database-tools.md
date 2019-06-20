---
title: Agrupar linhas em resultados da consulta (Ferramentas de Banco de Dados Visual) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- summarizing table subsets
- grouping rows
- grouping query results
ms.assetid: b07082d5-4d55-4903-9af9-4c470554c6d3
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 4cd80e7d999314c549df4ebb5e51aa2a0ca2d3f8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63154817"
---
# <a name="group-rows-in-query-results-visual-database-tools"></a>Agrupar linhas em resultados da consulta (Visual Database Tools)
  Para criar subtotais ou para mostrar outro resumo informativo de subconjuntos de uma tabela, crie grupos usando uma consulta de agregação. Cada grupo resume os dados de todas as linhas da tabela que possuem o mesmo valor.  
  
 Por exemplo, pode ser necessário exibir o preço médio de um livro na tabela `titles` , mas classifique os resultados por editora. Para isso, agrupe a consulta por publicador (por exemplo, `pub_id`). A saída da consulta resultante poderá ter a seguinte aparência:  
  
 ![Resultados da consulta: preço médio agrupado por publicador](../../database-engine/media//dv3w9e1.gif "Resultados da consulta: preço médio agrupado por publicador")  
  
 Quando se agrupam dados, só é possível exibir dados resumidos ou agrupados, como:  
  
-   Os valores das colunas agrupadas (os que aparecem na cláusula GROUP BY). No exemplo acima, `pub_id` é a coluna agrupada.  
  
-   Os valores produzidos por funções de agregação, como SUM( ) e AVG( ). No exemplo anterior, a segunda coluna é produzida usando a função AVG( ) com a coluna `price` .  
  
 Você não pode exibir valores de linhas individuais. Por exemplo, se o agrupamento for feito somente por publicador, não será possível exibir igualmente os títulos individuais da consulta. Portanto, se colunas forem adicionadas à saída da consulta, o [Designer de Consulta e Exibição](visual-database-tools.md) adicionará automaticamente essas colunas à cláusula GROUP BY da instrução no [Painel SQL](sql-pane-visual-database-tools.md). Em vez disso, para agregar uma coluna, especifique uma função de agregação para aquela coluna.  
  
 Se o agrupamento for feito por mais de uma coluna, cada grupo da consulta mostrará os valores de agregação de todas as colunas de agrupamento.  
  
 Por exemplo, a consulta a seguir, realizada nos grupos de tabela `titles` por publicador (`pub_id`) e também pelo tipo de livro (`type`). Os resultados de consulta são ordenados por publicador e mostram informações resumidas sobre todos os diferentes tipos de livros que o publicador produz:  
  
```  
SELECT pub_id, type, SUM(price) Total_price  
FROM titles  
GROUP BY pub_id, type  
```  
  
 A saída resultante pode ter a seguinte aparência:  
  
 ![Resultados da consulta: preço agrupado por publicador e tipo](../../database-engine/media//dv3w9e2.gif "Resultados da consulta: preço agrupado por publicador e tipo")  
  
### <a name="to-group-rows"></a>Para agrupar linhas  
  
1.  Inicie a consulta adicionando as tabelas a serem resumidas ao Painel Diagrama.  
  
2.  Clique com o botão direito do mouse na tela de fundo do painel Diagrama e escolha **Adicionar Grupo por** no menu de atalho. O Designer de Consulta e Exibição adicionará a coluna **Agrupar por** à grade do Painel de Critérios.  
  
3.  Adicione a coluna ou colunas que você deseja agrupar ao Painel de Critérios. Para que a coluna apareça na saída da consulta, certifique-se de que a coluna **Saída** seja selecionada para saída.  
  
     O Designer de Consulta e Exibição adicionará uma cláusula GROUP BY à instrução no Painel SQL. Por exemplo, a instrução SQL poderia se parecer com:  
  
    ```  
    SELECT pub_id  
    FROM titles  
    GROUP BY pub_id  
    ```  
  
4.  Adicione a coluna ou colunas que você deseja agregar ao Painel de Critérios. Verifique se a coluna esteja marcada para saída.  
  
5.  Na célula de grade **Agrupar por** da coluna que será agregada, selecione a função de agregação correta.  
  
     O Designer de Consulta e Exibição atribui automaticamente um alias de coluna à coluna que você está resumindo. Você pode substituir esse alias gerado automaticamente por outro que tenha mais significado. Para obter mais detalhes, veja [Criar aliases de coluna &#40;Visual Database Tools&#41;](create-column-aliases-visual-database-tools.md).  
  
     ![Adicionar um alias de coluna para o conjunto de resultados da consulta](../../database-engine/media//dv3w9e3.gif "Adicionar um alias de coluna para o conjunto de resultados da consulta")  
  
     A instrução correspondente no painel **SQL** pode ter esse formato:  
  
    ```  
    SELECT   pub_id, SUM(price) AS Totalprice  
    FROM     titles  
    GROUP BY pub_id  
    ```  
  
## <a name="see-also"></a>Consulte também  
 [Classificar e agrupar resultados da consulta &#40;Visual Database Tools&#41;](sort-and-group-query-results-visual-database-tools.md)  
  
  
