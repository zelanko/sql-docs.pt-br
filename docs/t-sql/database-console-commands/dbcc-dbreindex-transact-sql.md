---
title: DBCC DBREINDEX (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/16/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DBCC DBREINDEX
- DBREINDEX_TSQL
- DBREINDEX
- DBCC_DBREINDEX_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- index rebuilding [SQL Server]
- rebuilding indexes
- dynamic index rebuilding [SQL Server]
- DBCC DBREINDEX statement
ms.assetid: 6e929d09-ccb5-4855-a6af-b616022bc8f6
author: pmasl
ms.author: umajay
ms.openlocfilehash: 9b063b6f02a63292d4d43d1f276aa887cf02c201
ms.sourcegitcommit: 8ffc23126609b1cbe2f6820f9a823c5850205372
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81635876"
---
# <a name="dbcc-dbreindex-transact-sql"></a>DBCC DBREINDEX (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
Recria um ou mais índices de uma tabela no banco de dados especificado.
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Use [ALTER INDEX](../../t-sql/statements/alter-index-transact-sql.md) nesse caso.  
  
**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] até a [versão atual](https://go.microsoft.com/fwlink/p/?LinkId=299658))
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
DBCC DBREINDEX   
(   
    table_name   
    [ , index_name [ , fillfactor ] ]  
)  
    [ WITH NO_INFOMSGS ]   
```  
  
## <a name="arguments"></a>Argumentos  
 *table_name*  
 É o nome da tabela que contém o índice ou índices especificados a serem recriados. Os nomes de tabela precisam seguir as regras para [identificadores](../../relational-databases/databases/database-identifiers.md) *.*  
  
 *index_name*  
 É o nome do índice a ser recriado. Os nomes de índice devem obedecer às regras para identificadores. Se *index_name* for especificado, *table_name* precisará ser especificado. Se *index_name* não for especificado ou for " ", todos os índices da tabela serão recriados.  
  
 *fillfactor*  
 É a porcentagem de espaço em cada página de índice para armazenamento de dados quando o índice é criado ou reconstruído. *fillfactor* substitui o fator de preenchimento de quando o índice foi criado, tornando-se o novo padrão do índice e de qualquer outro índice não clusterizado que foi recriado porque um índice clusterizado foi recriado.  
 Quando *fillfactor* for 0, o DBCC DBREINDEX usará o último valor do fator de preenchimento especificado para o índice. Esse valor é armazenado na exibição de catálogo **sys.indexes**.   
 Se *fillfactor* for especificado, *table_name* e *index_name* precisarão ser especificados. Se *fillfactor* não for especificado, o fator de preenchimento padrão 100 será usado. Para obter mais informações, veja [Especificar fator de preenchimento para um índice](../../relational-databases/indexes/specify-fill-factor-for-an-index.md).  
  
 WITH NO_INFOMSGS  
 Suprime todas as mensagens informativas com níveis de severidade de 0 a 10.  
  
## <a name="remarks"></a>Comentários  
DBCC DBREINDEX recria um índice de uma tabela ou todos os índices definidos para uma tabela. Quando você permite que um índice seja recriado dinamicamente, os índices que impõem a restrição PRIMARY KEY ou UNIQUE podem ser recriados sem a necessidade de descartar e recriar essas restrições. Isso significa que um índice pode ser recriado sem ter conhecimento da estrutura de uma tabela ou suas restrições. Isso pode ocorrer depois de uma cópia em massa de dados na tabela.

DBCC DBREINDEX pode recriar todos os índices de uma tabela em uma instrução. Isso é mais fácil do que codificar várias instruções DROP INDEX e CREATE INDEX. Como o trabalho é feito por uma instrução, DBCC DBREINDEX é automaticamente atômica, considerando que as instruções DROP INDEX e CREATE INDEX, individualmente, devem ser incluídas em uma transação que será atômica. Além disso, DBCC DBREINDEX oferece mais otimizações que as instruções individuais DROP INDEX e CREATE INDEX.

Ao contrário de DBCC INDEXDEFRAG ou ALTER INDEX com a opção REORGANIZE, DBCC DBREINDEX é uma operação offline. Se um índice não clusterizado estiver sendo recriado, um bloqueio compartilhado será mantido na tabela em questão enquanto durar a operação. Isso impede que sejam efetuadas modificações na tabela. Se o índice clusterizado estiver sendo recriado, um bloqueio de tabela exclusivo será mantido. Isso impede qualquer acesso à tabela, deixando-a, dessa forma, offline. Para executar uma recriação de índice online ou para controlar o grau de paralelismo durante a operação de recriação do índice, use a instrução ALTER INDEX REBUILD com a opção ONLINE.

Para obter mais informações de como selecionar um método para recompilar ou reorganizar um índice, confira [Reorganizar e recompilar índices](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md).
  
## <a name="restrictions"></a>Restrições  
Não há suporte para uso de DBCC DBREINDEX nos seguintes objetos:
-   Tabelas do sistema  
-   Índices espaciais  
-   Índices columnstore xVelocity com otimização de memória  
  
## <a name="result-sets"></a>Conjuntos de resultados  
A menos que NO_INFOMSGS seja especificado (o nome de tabela deve ser especificado), DBCC DBREINDEX sempre retornará:
  
```sql
DBCC execution completed. If DBCC printed error messages, contact your system administrator.  
```  
  
## <a name="permissions"></a>Permissões  
O chamador precisa ser o proprietário da tabela ou ser membro da função de servidor fixa **sysadmin**, da função de banco de dados fixa **db_owner** ou da função de banco de dados fixa **db_ddladmin**.
  
## <a name="examples"></a>Exemplos  
### <a name="a-rebuilding-an-index"></a>a. Recriando um índice  
O exemplo a seguir recria o índice clusterizado `Employee_EmployeeID` com um fator de preenchimento de `80` na tabela `Employee` no banco de dados `AdventureWorks`.
  
```sql  
USE AdventureWorks2012;   
GO  
DBCC DBREINDEX ('HumanResources.Employee', PK_Employee_BusinessEntityID,80);  
GO  
```  
  
### <a name="b-rebuilding-all-indexes"></a>B. Recriando todos os índices  
O exemplo a seguir recria todos os índices da tabela `Employee` no `AdventureWorks` usando um valor de fator de preenchimento de `70`.
  
```sql
USE AdventureWorks2012;   
GO  
DBCC DBREINDEX ('HumanResources.Employee', ' ', 70);  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
[ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)  
[sys.dm_db_index_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)  
[ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)  
  
  

