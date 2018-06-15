---
title: sp_statistics (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_statistics_TSQL
- sp_statistics
dev_langs:
- TSQL
helpviewer_keywords:
- sp_statistics
ms.assetid: 0bb6495f-258a-47ec-9f74-fd16671d23b8
caps.latest.revision: 32
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 0b4a24cce24a94fdd6c4f901974d0f4accf7ff1b
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
ms.locfileid: "33263049"
---
# <a name="spstatistics-transact-sql"></a>sp_statistics (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Retorna uma lista de todos os índices e estatísticas em uma tabela especificada ou exibição indexada.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
-- Syntax for SQL Server, Azure SQL Database, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
sp_statistics [ @table_name = ] 'table_name'    
     [ , [ @table_owner = ] 'owner' ]   
     [ , [ @table_qualifier = ] 'qualifier' ]   
     [ , [ @index_name = ] 'index_name' ]   
     [ , [ @is_unique = ] 'is_unique' ]  
     [ , [ @accuracy = ] 'accuracy' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@table_name=** ] **'***table_name***'**  
 Especifica a tabela usada para retornar informações do catálogo. *table_name* é **sysname**, sem padrão. Não há suporte para a correspondência de padrão curinga.  
  
 [  **@table_owner=** ] **'***proprietário***'**  
 É o nome do proprietário da tabela usada para retornar informações do catálogo. *table_owner* é **sysname**, com um padrão NULL. Não há suporte para a correspondência de padrão curinga. Se *proprietário* não for especificado, serão aplicadas as regras de visibilidade de tabela padrão do DBMS subjacente.  
  
 No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], se o usuário atual possuir uma tabela com o nome especificado, os índices dessa tabela serão retornados. Se *proprietário* não for especificado e o usuário atual não possuir uma tabela com especificado *nome*, esse procedimento procurará uma tabela com especificado *nome* pertencentes a proprietário do banco de dados. Caso exista, os índices da tabela serão retornados.  
  
 [  **@table_qualifier=** ] **'***qualificador***'**  
 É o nome do qualificador da tabela. *qualificador* é **sysname**, com um padrão NULL. Vários produtos DBMS dão suporte à nomenclatura de três partes para tabelas (*qualificador ***.*** proprietário ***.*** nome*). No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], esse parâmetro representa o nome do banco de dados. Em alguns produtos, representa o nome do servidor do ambiente de banco de dados da tabela.  
  
 [  **@index_name=** ] **'***index_name***'**  
 É o nome do índice. *index_name* é **sysname**, com um padrão de %. Há suporte para a correspondência do padrão curinga.  
  
 [  **@is_unique=** ] **'***is_unique***'**  
 É se apenas índices exclusivos (se **Y**) devem ser retornadas. *is_unique* é **char (1)**, com um padrão de **N**.  
  
 [  **@accuracy=** ] **'***precisão***'**  
 É o nível de cardinalidade e exatidão de página para estatísticas. *precisão* é **char (1)**, com um padrão de **p**. Especifique **E** para certificar-se de que as estatísticas são atualizadas para que a cardinalidade e as páginas são precisas.  
  
 O valor **E** (SQL_ENSURE) solicita ao driver recupere as estatísticas incondicionalmente.  
  
 O valor **p** (SQL_QUICK) solicita ao driver para recuperar a cardinalidade e as páginas somente se elas estiverem prontamente disponíveis do servidor. Nesse caso, o driver não assegura que os valores são atuais. Aplicativos escritos em padrão Open Group sempre obterão o comportamento SQL_QUICK de drivers ODBC compatíveis com 3.x.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**TABLE_QUALIFIER**|**sysname**|Nome do qualificador de tabela. Esta coluna pode ser NULL.|  
|**TABLE_OWNER**|**sysname**|Nome do proprietário de tabela. Esta coluna sempre retorna um valor.|  
|**TABLE_NAME**|**sysname**|Nome da tabela. Esta coluna sempre retorna um valor.|  
|**NON_UNIQUE**|**smallint**|NOT NULL.<br /><br /> 0 = Exclusivo<br /><br /> 1 = Não exclusivo|  
|**INDEX_QUALIFIER**|**sysname**|Nome do proprietário do índice. Alguns produtos DBMS permitem que outros usuários, que não o proprietário da tabela, criam índices. Em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], essa coluna é sempre o mesmo que **TABLE_NAME**.|  
|**INDEX_NAME**|**sysname**|É o nome do índice. Esta coluna sempre retorna um valor.|  
|**TYPE**|**smallint**|Esta coluna sempre retorna um valor:<br /><br /> 0 = Estatísticas de uma tabela<br /><br /> 1 = Clusterizado<br /><br /> 2 = Com hash<br /><br /> 3 = não clusterizado|  
|**SEQ_IN_INDEX**|**smallint**|Posição da coluna dentro do índice.|  
|**COLUMN_NAME**|**sysname**|Nome de coluna para cada coluna do **TABLE_NAME** retornado. Esta coluna sempre retorna um valor.|  
|**COLLATION**|**char(1)**|Ordem usada no agrupamento. Pode ser:<br /><br /> A = Crescente<br /><br /> D = Decrescente<br /><br /> NULL = Não aplicável|  
|**CARDINALIDADE**|**Int**|Número de linhas na tabela ou valores exclusivos no índice.|  
|**PÁGINAS**|**Int**|Número de páginas para armazenar o índice ou a tabela.|  
|**FILTER_CONDITION**|**varchar(128)**|O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não retorna um valor.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 Nenhuma  
  
## <a name="remarks"></a>Remarks  
 Os índices no conjunto de resultados aparecem em ordem crescente pelas colunas **NON_UNIQUE**, **tipo**, **INDEX_NAME**, e **SEQ_IN_INDEX**.  
  
 O tipo de índice clusterizado se refere a um índice no qual são armazenados dados de tabela na ordem do índice. Isso corresponde à [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] índices clusterizados.  
  
 O tipo de índice em hash aceita pesquisas de correspondência e de intervalo exatas, mas pesquisas de correspondência padrão não usam o índice.  
  
 **sp_statistics** é equivalente a **SQLStatistics** no ODBC. Os resultados retornados são ordenados por **NON_UNIQUE**, **tipo**, **INDEX_QUALIFIER**, **INDEX_NAME**, e **SEQ_IN_ ÍNDICE**. Para obter mais informações, consulte o [referência da API ODBC](http://go.microsoft.com/fwlink/?LinkId=68323).  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão SELECT no esquema.  
  
## <a name="example-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Exemplo: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 O exemplo a seguir retorna informações sobre o `DimEmployee` tabela.  
  
```  
-- Uses AdventureWorks  
  
EXEC sp_statistics DimEmployee;  
```  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/catalog-stored-procedures-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

