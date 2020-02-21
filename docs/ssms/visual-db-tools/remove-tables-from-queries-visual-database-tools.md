---
title: Remover tabelas de consultas
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- deleting tables
- removing tables
- dropping tables
- queries [SQL Server], tables
ms.assetid: 8fea0b4f-99b7-4050-8d6f-a97ffb839619
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
ms.openlocfilehash: 32c25c3ded07e84e436b69af5baac5634909998c
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "75255247"
---
# <a name="remove-tables-from-queries-visual-database-tools"></a>Remover tabelas de consultas (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Você pode remover uma tabela ou qualquer objeto com valor de tabela da consulta.  
  
> [!NOTE]  
> Removendo uma tabela ou objeto com valor de tabela não exclui nada do banco de dados; só remove isto da consulta atual. Para obter detalhes sobre como remover uma tabela de um banco de dados, confira [Como: excluir tabelas de um banco de dados(https://msdn.microsoft.com/ca6aa3e9-9885-44c3-bafc-aec441fd97ec).  
  
### <a name="to-remove-a-table-or-table-structured-object"></a>Para remover uma tabela ou objeto estruturado por tabela  
  
-   No **Painel de Diagrama**, selecione a tabela, a exibição, a função definida pelo usuário, o sinônimo ou a consulta e, depois, pressione DELETE ou clique com o botão direito do mouse no objeto e escolha **Remover** na caixa de diálogo resultante. Você pode selecionar e remover vários objetos de uma vez.  
  
    -ou-  
  
-   Remova todas as referências ao objeto no **Painel SQL**.  
  
Quando você remover uma tabela ou objeto com valor de tabela, o Designer de Consulta e Exibição removerá automaticamente as junções que envolvem aquela tabela ou objeto com valor de tabela e removerá as referências às colunas do objeto no **Painel SQL** e no **Painel de Critérios**. Porém, se a consulta contiver expressões complexas que envolvam o objeto, o objeto não será removido automaticamente até que todas as referências a ele sejam removidas.  
  
## <a name="see-also"></a>Consulte Também  
[Adicionar tabelas a consultas](../../ssms/visual-db-tools/add-tables-to-queries-visual-database-tools.md)  
[Criar aliases de tabela](../../ssms/visual-db-tools/create-table-aliases-visual-database-tools.md)  
[Especificar critérios de pesquisa](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md)  
[Resumir resultados da consulta](../../ssms/visual-db-tools/summarize-query-results-visual-database-tools.md)  
[Executar operações básicas com consultas](../../ssms/visual-db-tools/perform-basic-operations-with-queries-visual-database-tools.md)  
  
