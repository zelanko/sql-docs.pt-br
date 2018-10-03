---
title: Acessando tabelas com otimização de memória usando Transact-SQL interpretado | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 92a44d4d-0e53-4fb0-b890-de264c65c95a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c81ac6c0c8dcf7e24c80b426654164c668fcf3a7
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48124016"
---
# <a name="accessing-memory-optimized-tables-using-interpreted-transact-sql"></a>Acessando tabelas com otimização de memória usando Transact-SQL interpretado
  Com raras exceções, você pode acessar tabelas com otimização de memória usando qualquer consulta de [!INCLUDE[tsql](../../includes/tsql-md.md)] ou operação DML (SELEÇÃO, INSERÇÃO, ATUALIZAÇÃO ou EXCLUSÃO), lotes ad hoc e os módulos SQL, como procedimentos armazenados, funções com valor de tabela, gatilhos e exibições.  
  
 O [!INCLUDE[tsql](../../includes/tsql-md.md)] interpretado se refere a lotes ou a procedimentos armazenados do [!INCLUDE[tsql](../../includes/tsql-md.md)] , que não sejam um procedimento armazenado nativamente compilado. O acesso do [!INCLUDE[tsql](../../includes/tsql-md.md)] interpretado às tabelas com otimização de memória é conhecido como acesso de interoperabilidade.  
  
 As tabelas com otimização de memória também podem ser acessadas usando um procedimento armazenado compilado nativamente. Os procedimentos armazenados nativamente compilados são recomendados para operações OLTP de desempenho crítico.  
  
 O acesso do [!INCLUDE[tsql](../../includes/tsql-md.md)] interpretado é recomendado para estes cenários:  
  
-   Consultas ad hoc e tarefas administrativas.  
  
-   As consultas de relatórios, que tipicamente usam construções não disponíveis em procedimentos armazenados nativamente compilados (como funções de janela).  
  
-   Para migrar partes críticas de desempenho do aplicativo para as tabelas com otimização de memória, com alterações mínimas (ou não) do código do aplicativo. Potencialmente, você pode ver aprimoramentos de desempenho de tabelas de migração. Se então você migrar procedimentos armazenados para procedimentos armazenados nativamente compilados, talvez veja mais aprimoramento de desempenho.  
  
-   Quando uma declaração do [!INCLUDE[tsql](../../includes/tsql-md.md)] não estiver disponível para procedimentos armazenados nativamente compilados.  
  
 As seguintes construções do [!INCLUDE[tsql](../../includes/tsql-md.md)] não têm suporte em procedimentos armazenados do [!INCLUDE[tsql](../../includes/tsql-md.md)] interpretado que acessam dados em uma tabela com otimização de memória.  
  
|Área|Sem suporte|  
|----------|-----------------|  
|Acesso a tabelas|TRUNCATE TABLE<br /><br /> MERGE (tabela com otimização de memória como destino).<br /><br /> Cursores de conjunto de chaves e dinâmicos (degradados automaticamente para estáticos).<br /><br /> Acesso dos módulos CLR, usando a conexão de contexto.<br /><br /> Referenciando uma tabela com otimização de memória de uma exibição indexada.|  
|Entre bancos de dados|Consultas de bancos de dados<br /><br /> Transações entre bancos de dados<br /><br /> Servidores vinculados|  
  
## <a name="table-hints"></a>Dicas de tabela  
 Para obter mais informações sobre dicas de tabela, consulte. [Dicas de tabela &#40;Transact-SQL&#41;](/sql/t-sql/queries/hints-transact-sql-table). O isolamento de SNAPSHOT foi adicionado para suportar [!INCLUDE[hek_2](../../includes/hek-2-md.md)].  
  
 As dicas de tabela a seguir não têm suporte para acessar uma tabela com otimização de memória usando o [!INCLUDE[tsql](../../includes/tsql-md.md)]interpretado.  
  
|||||  
|-|-|-|-|  
|HOLDLOCK|IGNORE_CONSTRAINTS|IGNORE_TRIGGERS|NOWAIT|  
|PAGLOCK|READCOMMITTED|READCOMMITTEDLOCK|READPAST|  
|READUNCOMMITTED|ROWLOCK|SPATIAL_WINDOW_MAX_CELLS = *integer*|TABLOCK|  
|TABLOCKXX|UPDLOCK|XLOCK||  
  
 Ao acessar uma tabela com otimização de memória em uma transação explícita ou implícita, usando o [!INCLUDE[tsql](../../includes/tsql-md.md)] interpretado, você deve incluir uma dica de tabela em nível de isolamento como SNAPSHOT, REPEATABLEREAD ou SERIALIZABLE, ou então você pode usar MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT. Para obter mais informações, consulte [diretrizes para níveis de isolamento da transação com tabelas com otimização de memória](memory-optimized-tables.md) e [opções ALTER DATABASE SET &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-options).  
  
> [!NOTE]  
>  Uma dica de tabela de nível de isolamento não é necessária para tabelas com otimização de memória acessadas por consultas executadas no modo de confirmação automática.  
  
## <a name="see-also"></a>Consulte também  
 [Suporte ao Transact-SQL para OLTP na memória](transact-sql-support-for-in-memory-oltp.md)   
 [Migrando para OLTP na memória](migrating-to-in-memory-oltp.md)  
  
  
