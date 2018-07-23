---
title: Renomear tabelas de consultas (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssms-visual-db
ms.reviewer: ''
ms.suite: sql
ms.technology: ssms
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- deleting tables
- removing tables
- dropping tables
- queries [SQL Server], tables
ms.assetid: 8fea0b4f-99b7-4050-8d6f-a97ffb839619
caps.latest.revision: 6
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0e0c7ef00a4ccd8a2c5299760b34ff348da689f3
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/12/2018
ms.locfileid: "38983998"
---
# <a name="remove-tables-from-queries-visual-database-tools"></a>Remover tabelas de consultas (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Você pode remover uma tabela — ou qualquer objeto com valor de tabela — da consulta  
  
> [!NOTE]  
> Removendo uma tabela ou objeto com valor de tabela não exclui nada do banco de dados; só remove isto da consulta atual. Para obter detalhes sobre como remover uma tabela de um banco de dados, consulte [Como excluir tabelas de um banco de dados (Visual Database Tools)](http://msdn.microsoft.com/ca6aa3e9-9885-44c3-bafc-aec441fd97ec).  
  
### <a name="to-remove-a-table-or-table-structured-object"></a>Para remover uma tabela ou objeto estruturado por tabela  
  
-   No **Painel de Diagrama**, selecione a tabela, a exibição, a função definida pelo usuário, o sinônimo ou a consulta e, depois, pressione DELETE ou clique com o botão direito do mouse no objeto e escolha **Remover** na caixa de diálogo resultante. Você pode selecionar e remover vários objetos de uma vez.  
  
    –ou–  
  
-   Remova todas as referências ao objeto no **Painel SQL**.  
  
Quando você remover uma tabela ou objeto com valor de tabela, o Designer de Consulta e Exibição removerá automaticamente as junções que envolvem aquela tabela ou objeto com valor de tabela e removerá as referências às colunas do objeto no **Painel SQL** e no **Painel de Critérios**. Porém, se a consulta contiver expressões complexas que envolvam o objeto, o objeto não será removido automaticamente até que todas as referências a ele sejam removidas.  
  
## <a name="see-also"></a>Consulte Também  
[Adicionar tabelas a consultas (Visual Database Tools)](../../ssms/visual-db-tools/add-tables-to-queries-visual-database-tools.md)  
[Criar aliases de tabelas (Visual Database Tools)](../../ssms/visual-db-tools/create-table-aliases-visual-database-tools.md)  
[Especificar critérios de pesquisa (Ferramentas de Banco de Dados Visual)](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md)  
[Resumir resultados da consulta (Visual Database Tools)](../../ssms/visual-db-tools/summarize-query-results-visual-database-tools.md)  
[Realizar operações básicas com consultas (Ferramentas de Banco de Dados Visual)](../../ssms/visual-db-tools/perform-basic-operations-with-queries-visual-database-tools.md)  
  
