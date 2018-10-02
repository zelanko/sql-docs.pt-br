---
title: ALTER PARTITION SCHEME (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ALTER PARTITION SCHEME
- ALTER_PARTITION_SCHEME_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER PARTITION SCHEME statement
- partition schemes [SQL Server], modifying
- modifying partition schemes
- adding filegroups
- NEXT USED filegroups
ms.assetid: f01d6880-9800-4cfb-8d11-d4be21efc8ca
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: b184b04c2f1535aed86d0eb2dc1fd33a840f0e0c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47611515"
---
# <a name="alter-partition-scheme-transact-sql"></a>ALTER PARTITION SCHEME (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Adiciona um grupo de arquivos a um esquema de partição ou altera a designação do grupo de arquivos NEXT USED para o esquema de partição. 

>[!NOTE]
>No Banco de Dados SQL do Azure, há suporte apenas para grupos de arquivos primários.  
  
 ![Ícone de link do artigo](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do artigo") [Convenções de sintaxe do Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
ALTER PARTITION SCHEME partition_scheme_name   
NEXT USED [ filegroup_name ] [ ; ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *partition_scheme_name*  
 É o nome do esquema de partição a ser alterado.  
  
 *filegroup_name*  
 Especifica o grupo de arquivos a ser marcado pelo esquema de partição como NEXT USED. Isso significa que o grupo de arquivos aceitará uma nova partição que for criada usando uma instrução [ALTER PARTITION FUNCTION](../../t-sql/statements/alter-partition-function-transact-sql.md).  
  
 Em um esquema de partição, somente um grupo de arquivos pode ser designado como NEXT USED. Um grupo de arquivos que não está vazio pode ser especificado. Se *filegroup_name* for especificado e atualmente não houver nenhum grupo de arquivos marcado como NEXT USED *filegroup_name* será marcado como NEXT USED. Se *filegroup_name* for especificado, e um grupo de arquivos com a propriedade NEXT USED já existir, a propriedade NEXT USED será transferida do grupo de arquivos existente para *filegroup_name*.  
  
 Se *filegroup_name* não for especificado e um grupo de arquivos com a propriedade NEXT USED já existir, o grupo de arquivos perderá seu estado NEXT USED para que não haja nenhum grupo de arquivos NEXT USED em *partition_scheme_name*.  
  
 Se *filegroup_name* não for especificado e houver nenhum grupo de arquivos marcado como NEXT USED, ALTER PARTITION SCHEME retornará um aviso.  
  
## <a name="remarks"></a>Remarks  
 Qualquer grupo de arquivos afetado por ALTER PARTITION SCHEME deve estar online.  
  
## <a name="permissions"></a>Permissões  
 As seguintes permissões podem ser usadas para executar ALTER PARTITION SCHEME:  
  
-   Permissão ALTER ANY DATASPACE. Essa permissão tem como padrão os membros da função de servidor fixa **sysadmin** e das funções de banco de dados fixas **db_owner** e **db_ddladmin** .  
  
-   Permissão CONTROL ou ALTER no banco de dados no qual o esquema de partição foi criado.  
  
-   Permissão CONTROL SERVER ou ALTER ANY DATABASE no servidor do banco de dados no qual o esquema de partição foi criado.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir assume o esquema de partição `MyRangePS1` e o grupo de arquivos `test5fg` existe no banco de dados atual.  
  
```  
ALTER PARTITION SCHEME MyRangePS1  
NEXT USED test5fg;  
```  
  
 O grupo de arquivos `test5fg` receberá qualquer partição adicional de uma tabela ou índice particionado como resultado de uma instrução ALTER PARTITION FUNCTION.  
  
## <a name="see-also"></a>Consulte Também  
 [CREATE PARTITION SCHEME &#40;Transact-SQL&#41;](../../t-sql/statements/create-partition-scheme-transact-sql.md)   
 [DROP PARTITION SCHEME &#40;Transact-SQL&#41;](../../t-sql/statements/drop-partition-scheme-transact-sql.md)   
 [CREATE PARTITION FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-partition-function-transact-sql.md)   
 [ALTER PARTITION FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-partition-function-transact-sql.md)   
 [DROP PARTITION FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/drop-partition-function-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sys.partition_schemes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-partition-schemes-transact-sql.md)   
 [sys.data_spaces &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-data-spaces-transact-sql.md)   
 [sys.destination_data_spaces &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-destination-data-spaces-transact-sql.md)   
 [sys.partitions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-partitions-transact-sql.md)   
 [sys.tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-tables-transact-sql.md)   
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)  
  
  
