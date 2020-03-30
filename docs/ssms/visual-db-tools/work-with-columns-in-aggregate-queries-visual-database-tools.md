---
title: Trabalhar com colunas em consultas de agregação
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- HAVING clause, query summary results
- GROUP BY clause, query summary results
- aggregate queries [SQL Server]
- WHERE clause, query summary results
ms.assetid: 1b82681f-3d4f-4b9a-bb1d-2060e44f2577
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
ms.openlocfilehash: 427f367eac38f2c5899f06c022e614bde80f37fb
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "75246240"
---
# <a name="work-with-columns-in-aggregate-queries-visual-database-tools"></a>Trabalhar com colunas em consultas de agregação (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Quando você cria consultas de agregação, o [Designer de Consulta e Exibição](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md) faz determinadas suposições para poder criar uma consulta válida. Por exemplo, se você estiver criando uma consulta de agregação e marcar uma coluna de dados para saída, o Designer de Consulta e Exibição fará com que a coluna automaticamente faça parte da cláusula GROUP BY para que você não tente exibir inadvertidamente o conteúdo de uma linha individual em um resumo.  
  
## <a name="using-group-by"></a>Usando Agrupar por  
O Designer de Consulta e Exibição usa as seguintes diretrizes para trabalhar com colunas:  
  
-   Quando você escolhe a opção Agrupar por ou adiciona uma função de agregação a uma consulta, todas as colunas marcadas para saída ou usadas para classificação são adicionadas automaticamente à cláusula GROUP BY. As colunas não serão adicionadas automaticamente à cláusula GROUP BY se já fizerem parte de uma função de agregação.  
  
    Se você não quiser que uma determinada coluna faça parte da cláusula GROUP BY, deverá alterar isso manualmente selecionando uma opção diferente na coluna Agrupar por do painel Critérios. Porém, o Designer de Consulta e Exibição não impedirá a escolha de uma opção que possa resultar em uma consulta que não será executada.  
  
-   Se você adicionar uma coluna de saída de consulta manualmente a uma função de agregação no painel Critérios ou SQL, o Designer de Consulta e Exibição não removerá automaticamente outras colunas de saída da consulta. Portanto, você deve remover as colunas restantes da saída da consulta ou torná-las parte da cláusula GROUP BY ou de uma função de agregação.  
  
Quando você insere um critério de pesquisa na coluna Filtrar do painel Critérios, o Designer de Consulta e Exibição segue estas regras:  
  
-   Se a coluna **Agrupar por** da grade não for exibida (porque você ainda não especificou uma consulta de agregação), os critérios de pesquisa serão colocados na cláusula WHERE.  
  
-   Se você já estiver em uma consulta de agregação e tiver selecionado a opção **Where** na coluna **Agrupar por** , os critérios de pesquisa serão colocados na cláusula WHERE.  
  
-   Se a coluna **Agrupar por** contiver qualquer valor diferente de **Where**, os critérios de pesquisa serão colocados na cláusula HAVING.  
  
## <a name="using-the-having-and-where-clauses"></a>Usando as cláusulas HAVING e WHERE  
Os seguintes princípios descrevem como você pode fazer referência a colunas em uma consulta de agregação nos critérios de pesquisa. Em geral, você pode usar uma coluna em um critério de pesquisa para filtrar as linhas que devem ser resumidas (uma cláusula WHERE) ou determinar quais resultados agrupados serão exibidos na saída final (uma cláusula HAVING).  
  
-   As colunas de dados individuais podem ser exibidas na cláusula WHERE ou HAVING, dependendo de como elas estão sendo usadas em outra consulta.  
  
-   As cláusulas WHERE são usadas para selecionar um subconjunto de linhas para resumo e agrupamento e, depois, são aplicadas antes que qualquer agrupamento seja feito. Portanto, você poderá usar uma coluna de dados em uma cláusula WHERE mesmo se ela não fizer parte da cláusula GROUP BY ou estiver contida em uma função de agregação. Por exemplo, a instrução seguinte seleciona todos os títulos que custam mais de R$ 10,00 e calcula a média do preço:  
  
    ```  
    SELECT AVG(price)  
    FROM titles  
    WHERE price > 10  
    ```  
  
-   Se você criar uma condição de pesquisa que envolva uma coluna também usada em uma cláusula GROUP BY ou em uma função de agregação, a condição de pesquisa poderá ser exibida como uma cláusula WHERE ou como uma cláusula HAVING; você decide quando você criar a condição. Por exemplo, a seguinte instrução cria um preço médio para os títulos de cada editor, depois exibe a média para as publicações nas quais o preço médio é maior que R$ 10,00:  
  
    ```  
    SELECT pub_id, AVG(price)  
    FROM titles  
    GROUP BY pub_id  
    HAVING (AVG(price) > 10)  
    ```  
  
-   Se você usar uma função de agregação em um critério de pesquisa, o critério envolverá um resumo e deverá, portanto, fazer parte da cláusula HAVING.  
  
## <a name="see-also"></a>Consulte Também  
[Resumir resultados da consulta &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/summarize-query-results-visual-database-tools.md)  
[Classificar e agrupar resultados da consulta &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/sort-and-group-query-results-visual-database-tools.md)  
  
