---
title: Contar linhas em uma tabela (Visual Database Tools) | Microsoft Docs
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
- totals [SQL Server], row counts
- row counts [SQL Server]
- column values [SQL Server]
- number of rows
- number of values
- counting rows
ms.assetid: dda4296a-1d16-4e77-8d6f-e295f6dd4e87
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: b1c6738ba292765a769cad8ae68cfae9a4503f8a
ms.contentlocale: pt-br
ms.lasthandoff: 04/11/2017

---
# <a name="count-rows-in-a-table-visual-database-tools"></a>Contar linhas em uma tabela (Visual Database Tools)
Você pode contar linhas em uma tabela para determinar:  
  
-   O número total de linhas em uma tabela, por exemplo, uma conta de todos os livros em uma tabela `titles` .  
  
-   O número de linhas em uma tabela que atenda uma condição específica, por exemplo, o número de livros publicados por um publicador em uma tabela `titles` .  
  
-   O número de valores em uma coluna particular.  
  
Quando você conta valores em uma coluna, nulos não são incluídos na conta. Por exemplo, você pode contar o número de livros em uma tabela `titles` que tenha valores na coluna `advance` . Por padrão, a conta inclui todos os valores, não apenas valores exclusivos.  
  
Os procedimentos para todos os três tipos de contas são semelhantes.  
  
### <a name="to-count-all-the-rows-in-a-table"></a>Para contar todas as linhas em uma tabela  
  
1.  Certifique-se de que a tabela que você quer resumir já está presente no painel Diagrama.  
  
2.  Clique com o botão direito do mouse na tela de fundo do painel Diagrama e escolha **Adicionar Grupo por** no menu de atalho. O [Designer de Consulta e Exibição](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md) adicionará a coluna **Agrupar por** à grade do painel Critérios.  
  
3.  Selecione **\&#42; (Todas as Colunas)** no retângulo que representa a tabela ou objeto avaliado por tabela.  
  
    O Designer de Consulta e Exibição preenche automaticamente o termo **Contagem** na coluna **Agrupar por** no painel de critérios e atribui um alias de coluna à coluna que você está resumindo. Você pode substituir esse alias gerado automaticamente por outro que tenha mais significado. Para obter mais detalhes, veja [Criar aliases de coluna &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/create-column-aliases-visual-database-tools.md).  
  
4.  Executa a consulta.  
  
### <a name="to-count-all-the-rows-that-meet-a-condition"></a>Para contar todas as linhas que atendam uma condição  
  
1.  Certifique-se de que a tabela que você quer resumir já está presente no painel Diagrama.  
  
2.  Clique com o botão direito do mouse na tela de fundo do painel Diagrama e escolha **Adicionar Grupo por** no menu de atalho. O Designer de Consulta e Exibição adicionará a coluna **Agrupar por** à grade do Painel de Critérios.  
  
3.  Selecione **\&#42;(Todas as Colunas)** no retângulo que representa a tabela ou o objeto estruturado por tabela.  
  
    O Designer de Consulta e Exibição preenche automaticamente o termo **Contagem** na coluna **Agrupar por** no painel de critérios e atribui um alias de coluna à coluna que você está resumindo. Para criar um título de coluna mais útil na saída da consulta, consulte [Criar aliases de coluna &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/create-column-aliases-visual-database-tools.md).  
  
4.  Adicione a coluna de dados que você quer pesquisar e desmarque a caixa de seleção na coluna **Saída**.  
  
    O Designer de Consulta e Exibição preenche automaticamente o termo **Agrupar por** na coluna **Agrupar por** da grade.  
  
5.  Altere **Agrupar por** na coluna **Agrupar por** para **Onde**.  
  
6.  Na coluna **Filtro** para a coluna de dados a ser pesquisada, insira o critério da pesquisa.  
  
7.  Executa a consulta.  
  
### <a name="to-count-the-values-in-a-column"></a>Para contar os valores em uma coluna.  
  
1.  Certifique-se de que a tabela que você quer resumir já está presente no painel Diagrama.  
  
2.  Clique com o botão direito do mouse na tela de fundo do painel Diagrama e escolha **Adicionar Grupo por** no menu de atalho. O Designer de Consulta e Exibição adicionará a coluna **Agrupar por** à grade do Painel de Critérios.  
  
3.  Acrescente a coluna que você quer contar ao painel Critérios.  
  
    O Designer de Consulta e Exibição preenche automaticamente o termo **Agrupar por** na coluna **Agrupar por** da grade.  
  
4.  Altere **Agrupar por** na coluna **Agrupar por** para **Contagem**.  
  
    > [!NOTE]  
    > Para contar apenas valores exclusivos, escolha **Distinção de Contagem**.  
  
5.  Executa a consulta.  
  
## <a name="see-also"></a>Consulte também  
[Classificar e agrupar resultados da consulta &amp;#40;Visual Database Tools&amp;#41;](../../ssms/visual-db-tools/sort-and-group-query-results-visual-database-tools.md)  
[Resumir resultados da consulta &amp;#40;Visual Database Tools&amp;#41;](../../ssms/visual-db-tools/summarize-query-results-visual-database-tools.md)  
  

