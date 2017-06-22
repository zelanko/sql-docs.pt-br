---
title: Adicionar colunas a consultas (Ferramentas de Banco de Dados Visual) | Microsoft Docs
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
- inserting columns
- columns [SQL Server], adding
- queries [SQL Server], columns
- adding columns
ms.assetid: 82f3ba72-3d72-4fb1-8179-2a953a782787
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 7190609525c847d4a7ff62899e2e5879d41e04af
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="add-columns-to-queries-visual-database-tools"></a>Adicionar colunas a consultas (Visual Database Tools)
Para usar uma coluna em uma consulta, você deve adicioná-la à consulta. Você pode adicionar uma coluna para exibi-la na saída da consulta, usá-la para ordenar, pesquisar os conteúdos da coluna, ou para resumir seus conteúdos. Você pode decidir qual das colunas usadas na consulta será incluída no painel de resultados quando a consulta for executada. Para obter mais informações, veja [Remove Columns from Query Results &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/remove-columns-from-query-results-visual-database-tools.md).  
  
> [!NOTE]  
> Para exibir o tipo de dados de uma coluna no Designer de Consulta e Exibição, selecione a tabela ou objeto avaliado pela tabela no **Painel de Diagrama** e na janela de propriedades clique em Lista de Colunas. Em seguida, clique nas **reticências (...)** para abrir a caixa de diálogo **Lista de Colunas** .  
  
Sempre que você usar uma coluna em uma consulta, você pode também usar uma expressão que consiste em qualquer combinação de colunas, literais, operadores e funções.  
  
### <a name="to-add-an-individual-column"></a>Para adicionar uma coluna individual  
  
-   No **Painel de Diagrama**, marque a caixa de seleção próxima à coluna que você quer incluir.  
  
    -ou-  
  
-   No **Painel Critérios**, mova para a primeira linha de grade em branco, clique no campo da coluna **Coluna** e selecione um nome de coluna na lista suspensa.  
  
### <a name="to-add-all-columns-for-one-table-or-table-valued-object"></a>Para adicionar todas as colunas de uma tabela ou objeto avaliado por tabela  
  
-   No **Painel de Diagrama**, marque a caixa de seleção ao lado de **\&#42;(Todas as Colunas)**.  
  
### <a name="to-add-all-columns-for-all-tables-and-table-structured-objects"></a>Para adicionar todas as colunas para todas as tabelas e objetos estruturados por tabela  
  
1.  Verifique se nenhuma linha de junção está selecionada no **Painel de Operações de Tabela** .  
  
2.  Clique com o botão direito do mouse no espaço em branco da janela Design e escolha **Propriedades** no menu de atalho.  
  
3.  Na janela Propriedades, clique em **Todas as colunas de saída** e escolha **Sim** ou **Não** na lista suspensa.  
  
## <a name="see-also"></a>Consulte também  
[Remover colunas de resultados da consulta &amp;#40;Visual Database Tools&amp;#41;](../../ssms/visual-db-tools/remove-columns-from-query-results-visual-database-tools.md)  
[Remover colunas de consultas &amp;#40;Visual Database Tools&amp;#41;](../../ssms/visual-db-tools/remove-columns-from-queries-visual-database-tools.md)  
[Especificar critérios de pesquisa &amp;#40;Visual Database Tools&amp;#41;](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md)  
[Resumir resultados da consulta &amp;#40;Visual Database Tools&amp;#41;](../../ssms/visual-db-tools/summarize-query-results-visual-database-tools.md)  
[Executar operações básicas com consultas &amp;#40;Visual Database Tools&amp;#41;](../../ssms/visual-db-tools/perform-basic-operations-with-queries-visual-database-tools.md)  
  

