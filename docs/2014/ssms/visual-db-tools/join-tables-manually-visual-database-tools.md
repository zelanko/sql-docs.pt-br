---
title: Unir tabelas manualmente (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- manual joins [SQL Server]
- joins [SQL Server], manual
- joins [SQL Server], creating
ms.assetid: 9c785356-646b-4c87-82d4-25efd6051d9d
author: stevestein
ms.author: sstein
ms.openlocfilehash: fe3dcd7f2affdbeb2e2fa5769f1aa6d02d27d5ac
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85064950"
---
# <a name="join-tables-manually-visual-database-tools"></a>Unir tabelas manualmente (Visual Database Tools)
  Quando você adiciona duas (ou mais) tabelas a uma consulta, o [Designer de Consulta e Exibição](visual-database-tools.md) tenta uni-las com base em dados comuns ou em informações armazenadas no banco de dados sobre como as tabelas estão relacionadas. Para obter detalhes, consulte [Unir tabelas automaticamente &#40;Visual Database Tools&#41;](join-tables-automatically-visual-database-tools.md). Entretanto, se o Designer de Consulta e Exibição não uniu as tabelas automaticamente, ou se você quiser criar outras condições de junção entre tabelas, será possível unir as tabelas manualmente.  
  
 Você pode criar junções com base em comparações entre duas colunas, não apenas colunas que contêm a mesma informação. Por exemplo, se seu banco de dados contiver duas tabelas, `titles` e `roysched`, você poderá comparar valores na coluna `ytd_sales` da tabela `titles` com as colunas `lorange` e `hirange` na tabela `roysched` . A criação dessa junção lhe permitiria encontrar títulos para pagamentos de royalty referentes a quedas de vendas acumuladas no ano entre os intervalos altos e baixos.  
  
> [!TIP]  
>  A junção funciona de forma rápida quando as colunas na condição de junção são indexadas. Em alguns casos, a união de colunas não indexadas pode resultar em uma consulta lenta.  
  
### <a name="to-manually-join-tables-or-table-structured-objects"></a>Para unir manualmente tabelas ou objetos estruturados por tabela  
  
1.  Adicione ao [painel Diagrama](diagram-pane-visual-database-tools.md) os objetos que deseja unir.  
  
2.  Arraste o nome da coluna de junção para a primeira tabela ou objeto estruturado por tabela e solte-o sobre a coluna relacionada na segunda tabela ou objeto estruturado por tabela. Você não pode basear uma junção em colunas `text`, `ntext`ou i`mage`.  
  
    > [!NOTE]  
    >  As colunas de junção devem ter os mesmos tipos de dados (ou compatíveis). Por exemplo, se a coluna de junção na primeira tabela for uma data, você deve relacionar isto a uma coluna de data na segunda tabela. Por outro lado, se a primeira coluna de junção for um inteiro, a coluna de junção relacionada também deverá ser do tipo de dados inteiro, mas poderá ser de um tamanho diferente. O Designer de Consulta e Exibição não verificará os tipos de dados das colunas que você usa para criar uma junção, mas quando você executar a consulta, o banco de dados exibirá um erro se os tipos de dados não forem compatíveis.  
  
3.  Se necessário, altere o operador de junção; por padrão, o operador é um sinal de igual (=). Para obter detalhes, consulte [Modificar operadores de junção &#40;Visual Database Tools&#41;](modify-join-operators-visual-database-tools.md).  
  
 O Designer de Consulta e Exibição adiciona uma cláusula INNER JOIN à instrução SQL no [painel SQL](sql-pane-visual-database-tools.md). Você pode alterar o tipo por uma junção externa. Para obter detalhes, veja [Criar junções externas &#40;Visual Database Tools&#41;](create-outer-joins-visual-database-tools.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Consultar com junções &#40;Visual Database Tools&#41;](query-with-joins-visual-database-tools.md)  
  
  
