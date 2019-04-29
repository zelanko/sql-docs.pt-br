---
title: Criar consultas Inserir Resultados (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- queries [SQL Server], types
- result sets [SQL Server], queries
- results [SQL Server], query
- Insert Results query
- queries [SQL Server], results
ms.assetid: 8770d630-09cc-47ec-a0e9-e9de2d7bbc89
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ebffc2246f0940c4643af2267086e727882a0633
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63031961"
---
# <a name="create-insert-results-queries-visual-database-tools"></a>Criar consultas Inserir Resultados (Visual Database Tools)
  Você pode copiar linhas de uma tabela para outra ou em uma tabela utilizando uma consulta Inserir Resultados. Por exemplo, em uma tabela `titles` , é possível utilizar uma consulta Inserir Resultados para copiar informações sobre todos os títulos de um publicador para uma segunda tabela que você pode disponibilizar para esse publicador. Uma consulta Inserir Resultados é semelhante às Consultas de Criar Tabela, mas copia linhas para uma tabela existente.  
  
> [!TIP]  
>  Você também pode copiar linhas de uma tabela para outra utilizando recortar e colar. Crie uma consulta para cada tabela e execute as consultas. Copie as linhas que você deseja de uma grade de resultados para outra.  
  
 Ao criar uma consulta Inserir Resultados, você especifica:  
  
-   A tabela de banco de dados para a qual copiar linhas (a tabela de destino).  
  
-   A tabela ou as tabelas de banco de dados de onde copiar as linhas (a tabela de origem). A tabela ou as tabelas de origem se tornam parte de uma subconsulta. Se você estiver copiando em uma tabela, a tabela de origem será a mesma que a tabela de destino.  
  
-   As colunas da tabela de origem cujo conteúdo você deseja copiar.  
  
-   As colunas de destino na tabela de destino para onde copiar os dados.  
  
-   Os critérios de pesquisa para definir as linhas que você deseja copiar.  
  
-   A ordem de classificação, se você desejar copiar as linhas em uma ordem específica.  
  
-   As opções Agrupar por, se você quiser copiar somente resumos informativos.  
  
 Por exemplo, a consulta a seguir copia informações de título da tabela `titles` para uma tabela de arquivo morto chamada `archivetitles`. A consulta copia o conteúdo de quatro colunas para todos os títulos que pertencem a um publicador específico:  
  
```  
INSERT INTO archivetitles   
   (title_id, title, type, pub_id)  
SELECT title_id, title, type, pub_id  
FROM titles  
WHERE (pub_id = '0766')  
```  
  
> [!NOTE]  
>  Para inserir valores em uma linha nova, utilize uma consulta Insert Values.  
  
 Você pode copiar o conteúdo das colunas selecionadas ou de todas as colunas em uma linha. Em ambos os casos, os dados que estão sendo copiados devem ser compatíveis com as colunas nas linhas para as quais você está copiando. Por exemplo, se você copiar o conteúdo de uma coluna como `price`, a coluna da linha que você estiver copiando deverá aceitar dados numéricos com casas decimais. Se você estiver copiando uma linha inteira, a tabela de destino deverá ter colunas compatíveis na mesma posição física da tabela de origem.  
  
 Quando você cria uma consulta Inserir Resultados, o painel Critérios é alterado para refletir as opções disponíveis para cópia de dados. Uma coluna Anexar é adicionada para permitir que você especifique as colunas nas quais os dados devem ser copiados.  
  
> [!CAUTION]  
>  Você não pode desfazer a ação de executar uma consulta Inserir Resultados. Como precaução, faça backup de seus dados antes de executar a consulta.  
  
### <a name="to-create-an-insert-results-query"></a>Para criar uma consulta Inserir Resultados  
  
1.  Crie uma nova consulta e adicione a tabela da qual você quer copiar linhas (a tabela de origem). Se você estiver copiando linhas em uma tabela, poderá adicionar a tabela de origem como tabela de destino.  
  
2.  No menu **Designer de Consulta** , aponte para **Alterar Tipo**e clique em **Inserir Resultados**.  
  
3.  Na caixa de diálogo [Escolher Tabela de Destino para Inserir Resultados](visual-database-tools.md), selecione a tabela para copiar linhas (tabela de destino).  
  
    > [!NOTE]  
    >  O Designer de Consulta e Exibição não pode determinar antecipadamente quais tabelas e exibições podem ser atualizadas. Portanto, a lista **Nome de Tabela** na caixa de diálogo **Escolher Tabela para Inserir a Partir da Consulta** mostra todas as tabelas e exibições disponíveis na conexão de dados que você estiver consultando, mesmo aquelas para as quais não é possível copiar linhas.  
  
4.  No retângulo que representa a tabela ou o objeto com valor de tabela, escolha os nomes das colunas cujo conteúdo você quer copiar. Para copiar linhas inteiras, escolha  **\* (todas as colunas)**.  
  
     O Designer de Consulta e Exibição adiciona as colunas escolhidas à coluna **Coluna** do painel Critérios.  
  
5.  Na coluna **Acrescentar** do painel Critérios, selecione uma coluna de destino na tabela de destino para cada coluna que você está copiando. Escolher *tablename.\**  se você estiver copiando linhas inteiras. As colunas na tabela de destino devem ter os mesmos tipos de dados (ou compatíveis) que as colunas na tabela de origem.  
  
6.  Se você quiser copiar as linhas em uma ordem específica, selecione a ordem de classificação. Para obter detalhes, consulte [Classificar e agrupar resultados da consulta &#40;Visual Database Tools&#41;](sort-and-group-query-results-visual-database-tools.md).  
  
7.  Especifique as linhas a serem copiadas inserindo critérios de pesquisa na coluna **Filtro**. Para obter detalhes, consulte [Especificar critérios de pesquisa &#40;Visual Database Tools&#41;](specify-search-criteria-visual-database-tools.md).  
  
     Se você não especificar um critério de pesquisa, todas as linhas da tabela de origem serão copiadas na tabela de destino.  
  
    > [!NOTE]  
    >  Quando você insere uma coluna para ser pesquisada no painel Critérios, o Designer de Consulta e Exibição também a adiciona à lista de colunas a serem copiadas. Se você quiser utilizar uma coluna para pesquisar mas não quiser copiá-la, desmarque a caixa de seleção próxima ao nome da coluna no retângulo que representa a tabela ou objeto com valor de tabela.  
  
8.  Para copiar resumos informativos, especifique as opções Agrupar por. Para obter detalhes, consulte [Resumir resultados da consulta &#40;Visual Database Tools&#41;](summarize-query-results-visual-database-tools.md).  
  
 Quando você executa uma consulta Inserir Resultados, nenhum resultado é relatado no [Painel de Resultados](results-pane-visual-database-tools.md). Em vez disso, será exibida uma mensagem indicando o total de linhas copiadas.  
  
## <a name="see-also"></a>Consulte também  
 [Tipos de consultas &#40;Visual Database Tools&#41;](types-of-queries-visual-database-tools.md)   
 [Tópicos de instruções de como criar consultas e exibições &#40;Visual Database Tools&#41;](design-queries-and-views-how-to-topics-visual-database-tools.md)  
  
  
