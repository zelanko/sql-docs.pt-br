---
description: Painel de Critérios (Visual Database Tools)
title: Painel de Critérios
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- Query Designer [SQL Server], Criteria pane
- View Designer, Criteria pane
- entering query options into grid [SQL Server]
- Criteria pane
- inserting query options into grid
- grid showing query options [SQL Server]
- adding query options into grid
ms.assetid: 6291affe-580e-482f-a7ff-45ce3837956a
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: 4738edd7c0db3522547bba26cd637a132f6630bb
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88314752"
---
# <a name="criteria-pane-visual-database-tools"></a>Painel de Critérios (Visual Database Tools)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
O painel Critérios permite que sejam especificadas as opções de consulta – como colunas de dados a serem exibidas, como ordenar os resultados e quais linhas selecionar – inserindo as seleções em uma grade tipo planilha. No painel Critérios você pode especificar o seguinte:  
  
-   Colunas a serem exibidas e aliases de nome de coluna.  
  
-   A tabela à qual pertence uma coluna.  
  
-   Expressões para colunas calculadas.  
  
-   A ordem de classificação da consulta.  
  
-   Critérios de pesquisa  
  
-   Critérios de agrupamento, incluindo funções de agregação a serem utilizadas em relatórios resumidos.  
  
-   Novos valores para consultas UPDATE ou INSERT INTO.  
  
-   Nomes de coluna de destino para consultas INSERT FROM.  
  
As alterações feitas no painel Critérios são refletidas automaticamente no painel Diagrama e no painel SQL. Da mesma forma, o painel Critérios é atualizado automaticamente para refletir as mudanças feitas nos outros painéis.  
  
## <a name="about-the-criteria-pane"></a>Sobre o painel Critérios  
As linhas no painel Critérios exibem as colunas de dados utilizadas em sua consulta; as colunas no painel Critérios exibem as opções de consulta.  
  
As informações específicas exibidas no painel Critérios dependem do tipo de consulta que você está criando.  
  
Se o painel Critérios não estiver visível, clique com o botão direito do mouse em Designer, aponte para **Painel**e clique em **Critérios**.  
  
## <a name="options"></a>Opções  
  
|**Coluna**|**Tipo de consulta**|**Descrição**|  
|--------------|------------------|-------------------|  
|Coluna|Todos|Exibe o nome de uma coluna de dados utilizada para a consulta ou a expressão para uma coluna computada. Essa coluna está bloqueada, portanto, está sempre visível à medida que você rola horizontalmente.|  
|Alias|SELECT, INSERT FROM, UPDATE, MAKE TABLE|Especifica um nome alternativo para uma coluna ou o nome que você pode utilizar para uma coluna computada.|  
|Tabela|SELECT, INSERT FROM, UPDATE, MAKE TABLE|Especifica o nome da tabela ou objeto estruturado por tabela para a coluna de dados associada. Essa coluna está vazia para colunas computadas.|  
|Saída|SELECT, INSERT FROM, MAKE TABLE|Especifica se uma coluna de dados é exibida na saída da consulta.<br /><br />Observação: se o banco de dados permitir, você poderá utilizar uma coluna de dados para classificar ou pesquisar cláusulas sem exibi-las no conjunto de resultados.|  
|Tipo de Classificação|SELECT, INSERT FROM|Especifica que a coluna de dados associada é utilizada para classificar os resultados da consulta e se a classificação é crescente ou decrescente.|  
|Ordem de classificação|SELECT, INSERT FROM|Especifica a prioridade de classificação das colunas de dados utilizadas para classificar o conjunto de resultados. Quando você altera a ordem de classificação de uma coluna de dados, a ordem de classificação de todas as outras colunas também é atualizada.|  
|Group By|SELECT, INSERT FROM, MAKE TABLE|Especifica que a coluna de dados associada está sendo utilizada para criar uma consulta de agregação. Essa coluna de grade será exibida somente se você tiver escolhido **Group By** no menu **Ferramentas** ou tiver adicionado uma cláusula GROUP BY no painel SQL.<br /><br />Por padrão, o valor dessa coluna é definido como **Group By**e a coluna se torna parte da cláusula GROUP BY.<br /><br />Quando você se move para uma célula nessa coluna e seleciona uma função de agregação para ser aplicada à coluna de dados associada, por padrão, a expressão resultante é adicionada como uma coluna de saída para o conjunto de resultados.|  
|Critérios|Todos|Especifica um critério de pesquisa (filtro) para a coluna de dados associada. Insira um operador (o padrão é “=”) e o valor a ser pesquisado. Insira os valores de texto entre aspas simples.<br /><br />Se a coluna de dados associada fizer parte de uma cláusula GROUP BY, a expressão inserida será utilizada para uma cláusula HAVING.<br /><br />Se você inserir valores para mais de uma célula na coluna da grade **Criteria**, os critérios de pesquisa resultantes serão vinculados automaticamente a um AND lógico.<br /><br />Para especificar várias expressões de critério de pesquisa para uma única coluna de banco de dados, por exemplo, (fname > 'A') AND (fname < 'M'), adicione a coluna de dados duas vezes ao painel Critérios e insira valores separados na coluna da grade **Criteria** para cada instância da coluna de dados.|  
|Ou...|Todos|Especifica uma expressão de critério de pesquisa adicional para a coluna de dados, vinculada a expressões anteriores com um OR lógico. Você pode adicionar mais colunas de grade **Or...** pressionando a tecla TAB na coluna **Or...** mais à direita.|  
|Acrescentar|INSERT FROM|Especifica o nome da coluna de dados de destino da coluna de dados associada. Quando você cria uma consulta Insert From, o Designer de Consulta e Exibição tenta corresponder a origem a uma coluna de dados de destino apropriada. Se o Designer de Consulta e Exibição não puder escolher uma correspondência, você deverá fornecer o nome da coluna.|  
|Novo valor|UPDATE, INSERT INTO|Especifica o valor a ser colocado na coluna associada. Insira um valor literal ou uma expressão.|  
  
## <a name="see-also"></a>Consulte Também  
[Tópicos de instruções de como criar consultas e exibições &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
[Painel Diagrama &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/diagram-pane-visual-database-tools.md)  
[Regras para inserção de valores de pesquisa &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/rules-for-entering-search-values-visual-database-tools.md)  
[Classificar e agrupar resultados da consulta &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/sort-and-group-query-results-visual-database-tools.md)  
[Painel de Resultados &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/results-pane-visual-database-tools.md)  
[Painel SQL &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/sql-pane-visual-database-tools.md)  
  
