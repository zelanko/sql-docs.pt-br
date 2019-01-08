---
title: Adicionar colunas a consultas (Ferramentas de Banco de Dados Visual) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- inserting columns
- columns [SQL Server], adding
- queries [SQL Server], columns
- adding columns
ms.assetid: 82f3ba72-3d72-4fb1-8179-2a953a782787
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: aef64ed8031664dcbefa7d0e30bf9f63435b292c
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52778938"
---
# <a name="add-columns-to-queries-visual-database-tools"></a>Adicionar colunas a consultas (Visual Database Tools)
  Para usar uma coluna em uma consulta, você deve adicioná-la à consulta. Você pode adicionar uma coluna para exibi-la na saída da consulta, usá-la para ordenar, pesquisar os conteúdos da coluna, ou para resumir seus conteúdos. Você pode decidir qual das colunas usadas na consulta será incluída no painel de resultados quando a consulta for executada. Para obter mais informações, veja [Remover colunas de resultados da consulta &#40;Visual Database Tools&#41;](visual-database-tools.md).  
  
> [!NOTE]  
>  Para exibir o tipo de dados de uma coluna no Designer de Consulta e Exibição, selecione a tabela ou objeto avaliado pela tabela no **Painel de Diagrama** e na janela de propriedades clique em Lista de Colunas. Em seguida, clique nas **reticências (...)** para abrir a caixa de diálogo **Lista de Colunas**.  
  
 Sempre que você usar uma coluna em uma consulta, você pode também usar uma expressão que consiste em qualquer combinação de colunas, literais, operadores e funções.  
  
### <a name="to-add-an-individual-column"></a>Para adicionar uma coluna individual  
  
-   No **Painel de Diagrama**, marque a caixa de seleção próxima à coluna que você quer incluir.  
  
     -ou-  
  
-   No **Painel Critérios**, mova para a primeira linha de grade em branco, clique no campo da coluna **Coluna** e selecione um nome de coluna na lista suspensa.  
  
### <a name="to-add-all-columns-for-one-table-or-table-valued-object"></a>Para adicionar todas as colunas de uma tabela ou objeto avaliado por tabela  
  
-   No **painel de diagrama**, marque a caixa de seleção ao lado  **\*(todas as colunas)**.  
  
### <a name="to-add-all-columns-for-all-tables-and-table-structured-objects"></a>Para adicionar todas as colunas para todas as tabelas e objetos estruturados por tabela  
  
1.  Verifique se nenhuma linha de junção está selecionada no **Painel de Operações de Tabela** .  
  
2.  Clique com o botão direito do mouse no espaço em branco da janela Design e escolha **Propriedades** no menu de atalho.  
  
3.  Na janela Propriedades, clique em **Todas as colunas de saída** e escolha **Sim** ou **Não** na lista suspensa.  
  
## <a name="see-also"></a>Consulte também  
 [Remover colunas de resultados da consulta &#40;Visual Database Tools&#41;](visual-database-tools.md)   
 [Remover colunas de consultas &#40;Visual Database Tools&#41;](remove-columns-from-queries-visual-database-tools.md)   
 [Especificar critérios de pesquisa &#40;Visual Database Tools&#41;](specify-search-criteria-visual-database-tools.md)   
 [Resumir resultados da consulta &#40;Visual Database Tools&#41;](summarize-query-results-visual-database-tools.md)   
 [Executar operações básicas com consultas &#40;Visual Database Tools&#41;](perform-basic-operations-with-queries-visual-database-tools.md)  
  
  
