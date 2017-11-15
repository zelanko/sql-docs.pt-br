---
title: Painel de Diagrama (Visual Database Tools) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Query Designer [SQL Server], Diagram pane
- View Designer, Diagram pane
- joins [SQL Server], Query and View Designer
- Diagram pane [Visual Database Tools]
ms.assetid: 399dfc7b-e2e7-47d3-bd11-163cbe0ce13c
caps.latest.revision: "4"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d6808554aad795fcda134687dfaf071487217f63
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="diagram-pane-visual-database-tools"></a>Painel de Diagrama (Visual Database Tools)
O painel Diagrama apresenta uma exibição gráfica das tabelas ou objetos com valor de tabela selecionados na conexão de dados. Mostra também todas as relações de junção entre eles.  
  
No painel Diagrama você pode:  
  
-   Adicionar ou remover tabelas e objetos com valor de tabela e especificar colunas de dados para saída.  
  
-   Criar ou modificar junções entre tabelas e objetos com valor de tabela.  
  
Quando você faz uma alteração no painel Diagrama, o painel Critérios e o painel SQL são atualizados para refletir a sua alteração. Por exemplo, se você selecionar uma coluna para saída em uma tabela ou janela de objeto com valor de tabela no painel Diagrama, o Designer de Consulta e Exibição adicionará a coluna de dados ao painel Critérios e à instrução SQL no painel SQL.  
  
Cada tabela ou objeto com valor de tabela é exibido como uma janela separada no painel Diagrama. O ícone na barra de título de cada retângulo indica qual tipo de objeto o retângulo representa, conforme ilustrado na tabela a seguir.  
  
## <a name="options"></a>Opções  
**Tabelas**  
Lista as tabelas que você pode adicionar ao painel Diagrama. Para adicionar uma tabela, selecione-a e clique em **Adicionar**. Para adicionar várias tabelas de uma vez, selecione-as e clique em **Adicionar**.  
  
**Exibições**  
Lista as exibições que você pode adicionar ao painel Diagrama. Para adicionar um modo de exibição, selecione-o e clique em **Adicionar**. Para adicionar vários modos de exibição de uma vez, selecione-os e clique em **Adicionar**.  
  
**Funções**  
Lista as funções definidas pelo usuário que você pode adicionar ao painel Diagrama. Para adicionar uma função, selecione-a e clique em **Adicionar**. Para adicionar várias funções de uma vez, selecione-as em clique em **Adicionar**.  
  
**Tabelas Locais**  
Lista as tabelas criadas por consultas em vez daquelas que pertencem ao banco de dados.  
  
**Sinônimos**  
Lista os sinônimos que você pode adicionar ao painel Diagrama. Para adicionar um sinônimo, selecione-o e clique em **Adicionar**. Para adicionar vários sinônimos de uma vez, selecione-os em clique em **Adicionar**.  
  
|Ícone|Tipo de objeto|  
|--------|---------------|  
|![Ícone das Ferramentas de Banco de Dados Visual](../../ssms/visual-db-tools/media/dv3wbi1.gif "Ícone das Ferramentas de Banco de Dados Visual")|Table|  
|![Ícone das Ferramentas de Banco de Dados Visual](../../ssms/visual-db-tools/media/dv3wbi2.gif "Ícone das Ferramentas de Banco de Dados Visual")|Consulta ou Exibição|  
|![Ícone das Ferramentas de Banco de Dados Visual](../../ssms/visual-db-tools/media/dv3wbi3.gif "Ícone das Ferramentas de Banco de Dados Visual")|Tabela vinculada|  
|![Ícone das Ferramentas de Banco de Dados Visual](../../ssms/visual-db-tools/media/dvudficon.gif "Ícone das Ferramentas de Banco de Dados Visual")|Função definida pelo usuário|  
|![Ícone das Ferramentas de Banco de Dados Visual](../../ssms/visual-db-tools/media/dv3wbi5.gif "Ícone das Ferramentas de Banco de Dados Visual")|Exibição vinculada|  
  
Cada retângulo mostra as colunas de dados da tabela ou objeto com valor de tabela. As caixas de seleção e os símbolos são exibidos ao lado dos nomes das colunas para indicar como as colunas são usadas na consulta. As dicas de ferramentas exibem informações como tipo de dados e tamanho das colunas.  
  
A tabela a seguir lista as caixas de seleção e os símbolos usados no retângulo para cada tabela ou objeto com valor de tabela.  
  
|Caixa de seleção ou símbolo|Description|  
|-----------------------|---------------|  
|![Ícone das Ferramentas de Banco de Dados Visual](../../ssms/visual-db-tools/media/dv3wbi7.gif "Ícone das Ferramentas de Banco de Dados Visual")<br /><br />![Ícone das Ferramentas de Banco de Dados Visual](../../ssms/visual-db-tools/media/dv3wbi8.gif "Ícone das Ferramentas de Banco de Dados Visual")<br /><br />![Ícone das Ferramentas de Banco de Dados Visual](../../ssms/visual-db-tools/media/dv3wbi9.gif "Ícone das Ferramentas de Banco de Dados Visual")<br /><br />![Ícone das Ferramentas de Banco de Dados Visual](../../ssms/visual-db-tools/media/dv3wbia.gif "Ícone das Ferramentas de Banco de Dados Visual")|Especifica se uma coluna de dados é exibida no conjunto de resultados da consulta (consulta  Select) ou se é usada em uma consulta Update, Insert From, Make Table ou Insert Into. Selecione a coluna a ser adicionada aos resultados. Se **(Todas as Colunas)** for selecionado, todas as colunas de dados serão exibidas na saída.<br /><br />O ícone usado com a caixa de seleção é alterado de acordo com o tipo de consulta que você está criando. Ao criar uma consulta Excluir, não podem ser selecionadas colunas individuais.|  
|![Ícone das Ferramentas de Banco de Dados Visual](../../ssms/visual-db-tools/media/dv3wbib.gif "Ícone das Ferramentas de Banco de Dados Visual")<br /><br />![Ícone das Ferramentas de Banco de Dados Visual](../../ssms/visual-db-tools/media/dv3wbic.gif "Ícone das Ferramentas de Banco de Dados Visual")|Indica que a coluna de dados está sendo usada para ordenar os resultados da consulta (faz parte de uma cláusula ORDER BY). O ícone é exibido como A-Z se a ordem de classificação for crescente ou Z-A se ordem de classificação for decrescente.|  
|![Ícone das Ferramentas de Banco de Dados Visual](../../ssms/visual-db-tools/media/dv3wbid.gif "Ícone das Ferramentas de Banco de Dados Visual")|Indica que a coluna de dados está sendo usada para criar um conjunto de resultados agrupado (faz parte de uma cláusula GROUP BY) em uma consulta de agregação.|  
|![Ícone das Ferramentas de Banco de Dados Visual](../../ssms/visual-db-tools/media/dv3wbie.gif "Ícone das Ferramentas de Banco de Dados Visual")|Indica que a coluna de dados está incluída em um critério de pesquisa da consulta (faz parte de um cláusula WHERE ou HAVING).|  
|![Ícone das Ferramentas de Banco de Dados Visual](../../ssms/visual-db-tools/media/dv3wbif.gif "Ícone das Ferramentas de Banco de Dados Visual")|Indica que os conteúdos da coluna de dados estão sendo resumidos para saída (são incluídos em uma função de agregação SUM, AVG ou outra função de agregação).|  
  
> [!NOTE]  
> O Designer de Consulta e Exibição não exibirá colunas de dados para uma tabela ou objeto com valor de tabela se você não tiver direitos de acesso suficientes às mesmas ou se o driver do banco de dados não puder retornar informações sobre as mesmas. Nesses casos, o Designer de Consulta e Exibição exibirá somente uma barra de título para a tabela ou objeto com estrutura de tabela.  
  
## <a name="joined-tables-on-the-diagram-pane"></a>Tabelas unidas no painel Diagrama  
Se a consulta envolver uma junção, uma linha de junção é exibida entre as colunas de dados envolvidas na junção. Se as colunas de dados unidas não forem exibidas (por exemplo, a janela da tabela ou do objeto com valor de tabela está minimizada ou a junção envolve uma expressão), o Designer de Consulta e Exibição colocará a linha de junção na barra de título do retângulo que representa a tabela ou o objeto com valor de tabela. O Designer de Consulta e Exibição exibe uma linha de junção para cada condição de junção.  
  
A forma do ícone no meio da linha de junção indica como são unidas as tabelas ou objetos com estrutura de tabela. Se a cláusula de junção usar um operador diferente de igual (=), o operador será exibido no ícone da linha de junção. A tabela a seguir lista os ícones que podem ser exibidos em uma linha de junção.  
  
|Ícone de linha de junção|Description|  
|------------------|---------------|  
|![Ícone das Ferramentas de Banco de Dados Visual](../../ssms/visual-db-tools/media/dv3wbih.gif "Ícone das Ferramentas de Banco de Dados Visual")|Junção interna (criada usando o sinal de igual).|  
|![Ícone das Ferramentas de Banco de Dados Visual](../../ssms/visual-db-tools/media/dv3wbii.gif "Ícone das Ferramentas de Banco de Dados Visual")|Junção interna baseada no operador "maior que". (O operador exibido no ícone da linha de junção reflete o operador usado na junção.)|  
|![Ícone das Ferramentas de Banco de Dados Visual](../../ssms/visual-db-tools/media/dv3wbij.gif "Ícone das Ferramentas de Banco de Dados Visual")|A junção externa em que todas as linhas da tabela representada à esquerda serão incluídas, mesmo se não tiverem correspondências na tabela relacionada.|  
|![Ícone das Ferramentas de Banco de Dados Visual](../../ssms/visual-db-tools/media/dv3wbik.gif "Ícone das Ferramentas de Banco de Dados Visual")|A junção externa em que todas as linhas da tabela representada à direita serão incluídas, mesmo se não tiverem correspondências na tabela relacionada.|  
|![Ícone das Ferramentas de Banco de Dados Visual](../../ssms/visual-db-tools/media/dv3wbil.gif "Ícone das Ferramentas de Banco de Dados Visual")|A junção externa completa em que todas as linhas de ambas as tabelas serão incluídas, mesmo se não tiverem correspondências na tabela relacionada.|  
  
Os ícones nas extremidades da linha de junção indicam o tipo de junção. A tabela a seguir lista os tipos de junções e os ícones que podem ser exibidos nas extremidades da linha de junção.  
  
|Ícone nas extremidades da linha de junção|Description|  
|-----------------------------|---------------|  
|![Ícone das Ferramentas de Banco de Dados Visual](../../ssms/visual-db-tools/media/dv3wbim.gif "Ícone das Ferramentas de Banco de Dados Visual")|Junção uma para uma|  
|![Ícone das Ferramentas de Banco de Dados Visual](../../ssms/visual-db-tools/media/dv3wbin.gif "Ícone das Ferramentas de Banco de Dados Visual")|Junção uma para muitas|  
|![Ícone das Ferramentas de Banco de Dados Visual](../../ssms/visual-db-tools/media/dv3wbio.gif "Ícone das Ferramentas de Banco de Dados Visual")|O Designer de Consulta e Exibição não pode determinar o tipo de junção|  
  
## <a name="see-also"></a>Consulte também  
[Tópicos de instruções de como criar consultas e exibições &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
[Painel Critérios &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/criteria-pane-visual-database-tools.md)  
[Classificar e agrupar resultados da consulta &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/sort-and-group-query-results-visual-database-tools.md)  
  
