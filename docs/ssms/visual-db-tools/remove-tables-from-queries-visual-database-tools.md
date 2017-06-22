---
title: Renomear tabelas de consultas (Visual Database Tools) | Microsoft Docs
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
- deleting tables
- removing tables
- dropping tables
- queries [SQL Server], tables
ms.assetid: 8fea0b4f-99b7-4050-8d6f-a97ffb839619
caps.latest.revision: 6
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 726f169be56f64484d505b91ca5d93a6426cbf7c
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="remove-tables-from-queries-visual-database-tools"></a>Remover tabelas de consultas (Visual Database Tools)
Você pode remover uma tabela — ou qualquer objeto com valor de tabela — da consulta  
  
> [!NOTE]  
> Removendo uma tabela ou objeto com valor de tabela não exclui nada do banco de dados; só remove isto da consulta atual. Para obter detalhes sobre como remover uma tabela de um banco de dados, consulte [Como excluir tabelas de um banco de dados (Visual Database Tools)](http://msdn.microsoft.com/en-us/ca6aa3e9-9885-44c3-bafc-aec441fd97ec).  
  
### <a name="to-remove-a-table-or-table-structured-object"></a>Para remover uma tabela ou objeto estruturado por tabela  
  
-   No **Painel de Diagrama**, selecione a tabela, a exibição, a função definida pelo usuário, o sinônimo ou a consulta e, depois, pressione DELETE ou clique com o botão direito do mouse no objeto e escolha **Remover** na caixa de diálogo resultante. Você pode selecionar e remover vários objetos de uma vez.  
  
    –ou–  
  
-   Remova todas as referências ao objeto no **Painel SQL**.  
  
Quando você remover uma tabela ou objeto com valor de tabela, o Designer de Consulta e Exibição removerá automaticamente as junções que envolvem aquela tabela ou objeto com valor de tabela e removerá as referências às colunas do objeto no **Painel SQL** e no **Painel de Critérios**. Porém, se a consulta contiver expressões complexas que envolvam o objeto, o objeto não será removido automaticamente até que todas as referências a ele sejam removidas.  
  
## <a name="see-also"></a>Consulte também  
[Adicionar tabelas a consultas (Visual Database Tools)](../../ssms/visual-db-tools/add-tables-to-queries-visual-database-tools.md)  
[Criar aliases de tabelas (Visual Database Tools)](../../ssms/visual-db-tools/create-table-aliases-visual-database-tools.md)  
[Especificar critérios de pesquisa (Visual Database Tools)](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md)  
[Resumir resultados da consulta (Visual Database Tools)](../../ssms/visual-db-tools/summarize-query-results-visual-database-tools.md)  
[Executar operações básicas com consultas (Visual Database Tools)](../../ssms/visual-db-tools/perform-basic-operations-with-queries-visual-database-tools.md)  
  

