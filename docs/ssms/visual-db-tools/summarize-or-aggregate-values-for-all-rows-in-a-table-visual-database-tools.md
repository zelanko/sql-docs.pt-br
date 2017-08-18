---
title: Resumir ou agregar valores para todas as linhas em uma tabela | Microsoft Docs
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
- summarizing query results
- aggregate functions [SQL Server], summarizing query results
ms.assetid: f5af876e-f937-4110-ba09-07999c35a699
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 734063422cddceb9ac5fb3b1b44b0d64d07f7d6b
ms.contentlocale: pt-br
ms.lasthandoff: 08/18/2017

---
# <a name="summarize-or-aggregate-values-for-all-rows-in-a-table-visual-database-tools"></a>Resumir ou agregar valores para todas as linhas em uma tabela (Visual Database Tools)
## <a name="aggregate-function"></a>Função de agregação
Usando uma função de agregação, você pode criar um resumo para obter todos os valores em uma tabela. Por exemplo, é possível criar uma consulta, como a seguinte, para exibir o preço total de todos os livros da tabela `titles` :  
  
```  
SELECT SUM(price)  
FROM titles  
```  
  
Crie várias agregações na mesma consulta usando funções de agregação com mais de uma coluna. Por exemplo, é possível criar uma consulta que calcule o total da coluna `price` e a média da coluna `discount` .  
  
Você pode agregar a mesma coluna de modos diferentes (como totalizar, contar e calcular a média) na mesma consulta. Por exemplo, a consulta seguinte calcula a média e resume a coluna `price` da tabela `titles` :  
  
```  
SELECT AVG(price), SUM(price)  
FROM titles  
```  
  
Se você adicionar um critério de pesquisa, será possível agregar o subconjunto de linhas que atendam àquela condição.  

**Observação:** Você também pode contar todas as linhas na tabela ou aquelas que atendam uma condição específica. Para obter detalhes, veja [Como contar linhas em uma tabela &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/count-rows-in-a-table-visual-database-tools.md).  
  
  
Quando você cria um valor de agregação único para todas as linhas em uma tabela, somente os valores de agregação são exibidos. Por exemplo, se você estivesse totalizando o valor da coluna `price` da tabela `titles` , você também não exibiria títulos individuais, nomes de publicador, e assim por diante.  
 
 **!** Se você estiver subtotalizando – isto é, durante a criação de grupos – será possível exibir valores de coluna para cada grupo. Para obter detalhes, veja [Agrupar linhas em resultados da consulta &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/group-rows-in-query-results-visual-database-tools.md).  

## <a name="aggregate-values-for-all-rows"></a>Agregar valores para todas as linhas  
  
1.  Verifique se a tabela que você quer agregar já está presente no painel Diagrama.  
  
2.  Clique com o botão direito do mouse na tela de fundo do painel Diagrama e escolha **Agrupar por** no menu de atalho. O [Designer de Consulta e Exibição](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md) adicionará a coluna **Agrupar por** à grade do painel Critérios.  
  
3.  Some a coluna que você quer agregar ao painel Critérios. Verifique se a coluna esteja marcada para saída.  
  
    O Designer de Consulta e Exibição atribui automaticamente um alias de coluna à coluna que você está resumindo. Você pode substituir este alias por um mais significativo. Para obter detalhes, veja [Criar aliases de coluna &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/create-column-aliases-visual-database-tools.md).  
  
4.  Na coluna de grade **Agrupar por**, selecione a função de agregação apropriada, como: **Soma**, **Média**, **Mín**, **Máx** e **Contar**. Se você quiser agregar somente linhas exclusivas no conjunto de resultados, escolha uma função de agregação com as opções DISTINCT, como **Min Distinct**. Não escolha **Agrupar por**, **Expressão**nem **Onde**, porque essas opções não se aplicam quando você agrega todas as linhas.  
  
    O Designer de Consulta e Exibição substitui o nome de coluna da instrução no [Painel SQL](../../ssms/visual-db-tools/sql-pane-visual-database-tools.md) com a função de agregação que você especificar. Por exemplo, a instrução SQL poderia se parecer com:  
  
    ```  
    SELECT SUM(price)  
    FROM titles  
    ```  
  
5.  Se você quiser criar mais de uma agregação na consulta, repita os passos 3 e 4.  
  
    Quando você adiciona outra coluna à lista de saída da consulta ou faz a classificação por lista, o Designer de Consulta e Exibição preenche automaticamente o termo **Agrupar por** na coluna **Agrupar por** da grade. Selecione a função de agregação apropriada.  
  
6.  Adicione critérios de pesquisa, se existir, para especificar o subconjunto de linhas que deseja resumir.  
  
Quando você executar a consulta, o painel Resultados exibirá as agregações por você especificadas.  
  
> [!NOTE]  
> O Designer de Consulta e Exibição mantém funções de agregação como parte da instrução SQL no painel SQL até que você desative o modo Agrupar por. Portanto, se você modificar sua consulta alterando o tipo, as tabelas ou os objetos com valor de tabela presentes no painel Diagrama, a consulta resultante poderá incluir funções de agregação inválidas.  
  
## <a name="see-also"></a>Consulte também  
[Classificar e agrupar resultados da consulta &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/sort-and-group-query-results-visual-database-tools.md)  
[Resumir resultados da consulta &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/summarize-query-results-visual-database-tools.md)  
  

