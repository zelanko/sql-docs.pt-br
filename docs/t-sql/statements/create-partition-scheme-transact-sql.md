---
title: "CRIAR o esquema de partição (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 04/10/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CREATE PARTITION SCHEME
- SCHEME
- PARTITION SCHEME
- CREATE_PARTITION_SCHEME_TSQL
- SCHEME_TSQL
- PARTITION_SCHEME_TSQL
dev_langs: TSQL
helpviewer_keywords:
- partitioned indexes [SQL Server], schemes
- partitioned tables [SQL Server], schemes
- CREATE PARTITION SCHEME statement
- partition schemes [SQL Server], creating
- filegroups [SQL Server], partitions
- partitioned indexes [SQL Server], filegroups
- partitioned tables [SQL Server], filegroups
- mapping partitions [SQL Server]
ms.assetid: 5b21c53a-b4f4-4988-89a2-801f512126e4
caps.latest.revision: "39"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 5c97264457e575aa076e6b10f3454f0d8cf6e2d7
ms.sourcegitcommit: 50e54dda407f362262b86941f68b7d80516db7fb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/06/2017
---
# <a name="create-partition-scheme-transact-sql"></a>CREATE PARTITION SCHEME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Cria um esquema no banco de dados atual que mapeia as partições de uma tabela particionada ou índice para grupos de arquivos. O número e o domínio das partições de uma tabela particionada ou índice são determinados em uma função de partição. Uma função de partição deve ser criada pela primeira vez em um [CREATE PARTITION FUNCTION](../../t-sql/statements/create-partition-function-transact-sql.md) instrução antes de criar um esquema de partição.  

[!NOTE]
Banco de dados do SQL Azure têm suporte apenas grupos de arquivos primários.  

 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
CREATE PARTITION SCHEME partition_scheme_name  
AS PARTITION partition_function_name  
[ ALL ] TO ( { file_group_name | [ PRIMARY ] } [ ,...n ] )  
[ ; ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *partition_scheme_name*  
 É o nome do esquema de partição. Os nomes de esquema de partição devem ser exclusivo no banco de dados e estar em conformidade com as regras de [identificadores](../../relational-databases/databases/database-identifiers.md).  
  
 *partition_function_name*  
 É o nome da função de partição que usa o esquema de partição. As partições criadas pela função de partição são mapeadas para os grupos de arquivos especificados no esquema de partição. *partition_function_name* já deve existir no banco de dados. Uma única partição não pode conter FILESTREAM e grupos de arquivos não FILESTREAM.  
  
 ALL  
 Especifica que todas as partições são mapeadas para o grupo de arquivos fornecido no *file_group_name*, ou o grupo de arquivos primário se **[**primário**]** for especificado. Se ALL for especificado, somente um *file_group_name* pode ser especificado.  
  
 *file_group_name* | **[** primário **]** [ **,***... n*]  
 Especifica os nomes dos grupos de arquivos para manter as partições especificadas por *partition_function_name*. *file_group_name* já deve existir no banco de dados.  
  
 Se **[**primário**]** for especificado, a partição será armazenada no grupo de arquivos primário. Se ALL for especificado, somente um *file_group_name* pode ser especificado. As partições são atribuídas a grupos de arquivos, começando com a partição 1, na ordem em que os grupos de arquivos são listados em [**,***... n*]. O mesmo *file_group_name* pode ser especificado mais de uma vez em [**,***... n*]. Se  *n*  não é suficiente para manter o número de partições especificadas em *partition_function_name*, CREATE PARTITION SCHEME falhará com um erro.  
  
 Se *partition_function_name* gera menos partições que grupos de arquivos, o primeiro grupo de arquivos não atribuído é marcado como NEXT USED e uma mensagem informativa exibida, nomeando o grupo de arquivos NEXT USED. Se ALL for especificado, a única *file_group_name* mantém sua propriedade NEXT USED para este *partition_function_name*. O grupo de arquivos NEXT USED receberá uma partição adicional se uma for criada em uma instrução ALTER PARTITION FUNCTION. Para criar grupos de arquivos não atribuídos adicionais para conter novas partições, use ALTER PARTITION SCHEME.  
  
 Quando você especifica o grupo de arquivos primário *file_group_name* [1**,***... n*], PRIMARY deverá ser delimitado, como em **[**primário**]** , porque é uma palavra-chave.  
  
 Para [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)], há suporte somente para PRIMARY. Consulte o exemplo E abaixo. 
  
## <a name="permissions"></a>Permissões  
 As seguintes permissões podem ser usadas para executar CRETE PARTITION SCHEME:  
  
-   Permissão ALTER ANY DATASPACE. Essa permissão tem como padrão os membros da função de servidor fixa **sysadmin** e das funções de banco de dados fixas **db_owner** e **db_ddladmin** .  
  
-   Permissão CONTROL ou ALTER no banco de dados no qual o esquema de partição está sendo criado.  
  
-   Permissão CONTROL SERVER ou ALTER ANY DATABASE no servidor do banco de dados no qual o esquema de partição está sendo criado.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-creating-a-partition-scheme-that-maps-each-partition-to-a-different-filegroup"></a>A. Criando um esquema de partição que mapeia cada partição para um grupo de arquivos diferente  
 O exemplo a seguir cria uma função de partição para dividir uma tabela ou índice em quatro partições. Então, será criado um esquema de partição que especifica os grupos de arquivos que conterão cada uma das quatro partições. Este exemplo supõe que os grupos de arquivos já existam no banco de dados.  
  
```  
CREATE PARTITION FUNCTION myRangePF1 (int)  
AS RANGE LEFT FOR VALUES (1, 100, 1000);  
GO  
CREATE PARTITION SCHEME myRangePS1  
AS PARTITION myRangePF1  
TO (test1fg, test2fg, test3fg, test4fg);  
```  
  
 As partições de uma tabela que usa a função de partição `myRangePF1` na coluna de particionamento **col1** seriam atribuídas como mostrado na tabela a seguir.  
  
||||||  
|-|-|-|-|-|  
|**Grupo de arquivos**|`test1fg`|`test2fg`|`test3fg`|`test4fg`|  
|**Partição**|1|2|3|4|  
|**Valores**|**Col1** <= `1`|**Col1**  >  `1` AND **col1** <= `100`|**Col1**  >  `100` AND **col1** <= `1000`|**Col1** > `1000`|  
  
### <a name="b-creating-a-partition-scheme-that-maps-multiple-partitions-to-the-same-filegroup"></a>B. Criando um esquema de partição que mapeia várias partições para o mesmo grupo de arquivos  
 Se todas as partições forem mapeadas para o mesmo grupo de arquivos, use a palavra-chave ALL. Porém, se várias, mas nem todas as partições forem mapeadas para o mesmo grupo de arquivos, o nome do grupo de arquivos deverá ser repetido, como mostrado no exemplo a seguir.  
  
```  
CREATE PARTITION FUNCTION myRangePF2 (int)  
AS RANGE LEFT FOR VALUES (1, 100, 1000);  
GO  
CREATE PARTITION SCHEME myRangePS2  
AS PARTITION myRangePF2  
TO ( test1fg, test1fg, test1fg, test2fg );  
```  
  
 As partições de uma tabela que usa a função de partição `myRangePF2` na coluna de particionamento **col1** seriam atribuídas como mostrado na tabela a seguir.  
  
||||||  
|-|-|-|-|-|  
|**Grupo de arquivos**|`test1fg`|`test1fg`|`test1fg`|`test2fg`|  
|**Partição**|1|2|3|4|  
|**Valores**|**Col1** <= `1`|**Col1** > 1 AND **col1** <= `100`|**Col1**  >  `100` AND **col1** <= `1000`|**Col1** > `1000`|  
  
### <a name="c-creating-a-partition-scheme-that-maps-all-partitions-to-the-same-filegroup"></a>C. Criando um esquema de partição que mapeia todas as partições para o mesmo grupo de arquivos  
 O exemplo a seguir cria a mesma função de partição que nos exemplos anteriores e será criado um esquema de partição que mapeia todas as partições para o mesmo grupo de arquivos.  
  
```  
CREATE PARTITION FUNCTION myRangePF3 (int)  
AS RANGE LEFT FOR VALUES (1, 100, 1000);  
GO  
CREATE PARTITION SCHEME myRangePS3  
AS PARTITION myRangePF3  
ALL TO ( test1fg );  
```  
  
### <a name="d-creating-a-partition-scheme-that-specifies-a-next-used-filegroup"></a>D. Criando um esquema de partição que especifica um grupo de arquivos 'NEXT USED'  
 O exemplo a seguir cria a mesma função de partição que nos exemplos anteriores e será criado um esquema de partição que lista mais grupos de arquivos do que há partições criadas pela função de partição associada.  
  
```  
CREATE PARTITION FUNCTION myRangePF4 (int)  
AS RANGE LEFT FOR VALUES (1, 100, 1000);  
GO  
CREATE PARTITION SCHEME myRangePS4  
AS PARTITION myRangePF4  
TO (test1fg, test2fg, test3fg, test4fg, test5fg)  
```  
  
 A execução da instrução retorna a seguinte mensagem.  
  
Esquema de partição 'myRangePS4' foi criado com êxito. 'test5fg' está marcado como o próximo grupo de arquivos usado no esquema de partição 'myRangePS4'.  
  
  
 Se a função de partição `myRangePF4` for alterada para adicionar uma partição, o grupo de arquivos `test5fg` receberá a partição recém-criada.  

### <a name="e-creating-a-partition-schema-only-on-primary---only-primary-is-supported-for-includesqldbesaincludessqldbesa-mdmd"></a>E. Criando um esquema de partição apenas no primário - primário só há suporte para[!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]

 O exemplo a seguir cria uma função de partição para dividir uma tabela ou índice em quatro partições. Um esquema de partição é criado que especifica que todas as partições são criadas no grupo de arquivos primário.  
  
```  
CREATE PARTITION FUNCTION myRangePF1 (int)  
AS RANGE LEFT FOR VALUES (1, 100, 1000);  
GO  
CREATE PARTITION SCHEME myRangePS1  
AS PARTITION myRangePF1  
ALL TO ( [PRIMARY] );  
```
   
## <a name="see-also"></a>Consulte também  
 [CREATE PARTITION FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-partition-function-transact-sql.md)   
 [ALTER PARTITION SCHEME &#40; Transact-SQL &#41;](../../t-sql/statements/alter-partition-scheme-transact-sql.md)   
 [REMOVER o esquema de partição &#40; Transact-SQL &#41;](../../t-sql/statements/drop-partition-scheme-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [Criar tabelas e índices particionados](../../relational-databases/partitions/create-partitioned-tables-and-indexes.md)   
 [sys. partition_schemes &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-partition-schemes-transact-sql.md)   
 [data_spaces &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-data-spaces-transact-sql.md)   
 [sys.destination_data_spaces &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-destination-data-spaces-transact-sql.md)   
 [sys. Partitions &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-partitions-transact-sql.md)   
 [sys.tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-tables-transact-sql.md)   
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)  
  
  
