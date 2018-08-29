---
title: sp_special_columns (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_special_columns_TSQL
- sp_special_columns
dev_langs:
- TSQL
helpviewer_keywords:
- sp_special_columns
ms.assetid: 0b0993f8-73e0-402b-8c6c-1b0963956f5d
caps.latest.revision: 38
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: ba4418e9e34d7ec45def0eaec004e3d5c8e944dd
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43069449"
---
# <a name="spspecialcolumns-transact-sql"></a>sp_special_columns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Retorna o conjunto ideal de colunas que identificam, de forma exclusiva, uma linha na tabela. Também retorna colunas atualizadas automaticamente quando qualquer valor na linha for atualizado por uma transação.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
sp_special_columns [ @table_name = ] 'table_name'     
     [ , [ @table_owner = ] 'table_owner' ]   
     [ , [ @qualifier = ] 'qualifier' ]   
     [ , [ @col_type = ] 'col_type' ]   
     [ , [ @scope = ] 'scope' ]  
     [ , [ @nullable = ] 'nullable' ]   
     [ , [ @ODBCVer = ] 'ODBCVer' ]   
[ ; ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @table_name=] '*table_name*'  
 É o nome da tabela usada para retornar informações do catálogo. *nome da* está **sysname**, sem padrão. Não há suporte para a correspondência de padrão curinga.  
  
 [ @table_owner=] '*table_owner*'  
 É o proprietário da tabela usada para retornar informações de catálogo. *proprietário* está **sysname**, com um padrão NULL. Não há suporte para a correspondência de padrão curinga. Se *proprietário* não for especificado, serão aplicadas as regras de visibilidade de tabela padrão do DBMS subjacente.  
  
 No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], se o usuário atual possuir uma tabela com o nome especificado, as colunas dessa tabela serão retornadas. Se *proprietário* não for especificado e o usuário atual não possuir uma tabela especificada *nome*, esse procedimento procurará uma tabela especificada *nome* pelo banco de dados de propriedade proprietário. Se a tabela existir, suas colunas serão retornadas.  
  
 [ @qualifier=] '*qualificador*'  
 É o nome do qualificador da tabela. *qualificador* está **sysname**, com um padrão NULL. Vários produtos DBMS dão suporte à nomenclatura de três partes para tabelas (*qualificador*). No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], essa coluna representa o nome do banco de dados. Em alguns produtos, representa o nome do servidor do ambiente de banco de dados da tabela.  
  
 [ @col_type=] '*col_type*'  
 É o tipo da coluna. *col_type* está **char (** 1 **)**, com um padrão de R. o tipo R retorna a coluna ou conjunto ideal de colunas que, pela recuperação de valores da coluna ou colunas, permite que qualquer linha especificada tabela a ser identificado exclusivamente. A coluna pode ser uma pseudocoluna especificamente projetada para esta finalidade ou a coluna ou colunas de qualquer índice exclusivo da tabela. O tipo V retorna a coluna ou as colunas da tabela especificada, se houver, que são automaticamente atualizadas pela fonte de dados quando qualquer valor na linha é atualizado por qualquer transação.  
  
 [ @scope=] '*escopo*'  
 É o escopo mínimo necessário de ROWID. *escopo* está **char (** 1 **)**, com um padrão T. o escopo C Especifica que a ROWID é válida somente quando posicionada nessa linha. O escopo T especifica que a ROWID é válida para a transação.  
  
 [ @nullable=] '*anulável*'  
 Indica se as colunas especiais podem aceitar um valor nulo. *anulável* está **char (** 1 **)**, com um padrão U. o Especifica colunas especiais que não permitem valores nulos. U especifica colunas que permitem valor parcialmente nulo.  
  
 [ @ODBCVer=] '*ODBCVer*'  
 É a versão do ODBC que está sendo utilizada. *ODBCVer* está **int (** 4 **)**, com um padrão de 2. Isso indica o ODBC versão 2.0. Para obter mais informações sobre a diferença entre ODBC versão 2.0 e ODBC versão 3.0, consulte a especificação de ODBC SQLSpecialColumns para ODBC versão 3.0.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 None  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|SCOPE|**smallint**|Escopo real da ID da linha. Pode ser 0, 1 ou 2. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Sempre retorna 0. Esse campo sempre retorna um valor.<br /><br /> 0 = SQL_SCOPE_CURROW. A ID da linha tem a garantia de ser válida somente quando posicionada nessa linha. Uma nova seleção posterior que utilize a ID da linha talvez não retorne uma linha se a linha foi atualizada ou excluída por outra transação.<br /><br /> 1 = SQL_SCOPE_TRANSACTION. A ID da linha tem a garantia de ser válida durante a transação atual.<br /><br /> 2 = SQL_SCOPE_SESSION. A ID da linha tem a garantia de ser válida durante a sessão (dentro dos limites da transação).|  
|COLUMN_NAME|**sysname**|Nome da coluna para cada coluna do *tabela*retornado. Esse campo sempre retorna um valor.|  
|DATA_TYPE|**smallint**|Tipo de dados SQL ODBC.|  
|TYPE_NAME|**sysname**|Nome do tipo de dados dependente da fonte de dados; Por exemplo, **char**, **varchar**, **money**, ou **texto**.|  
|PRECISION|**Int**|Precisão da coluna na fonte de dados. Esse campo sempre retorna um valor.|  
|LENGTH|**Int**|Comprimento em bytes, necessário para o tipo de dados em seu formato binário na fonte de dados, por exemplo, 10 para **char (** 10 **)**, 4 para **integer**e 2 para **smallint** .|  
|SCALE|**smallint**|Escala da coluna na fonte de dados. NULL é retornado para os tipos de dados para os quais a escala não é aplicável.|  
|PSEUDO_COLUMN|**smallint**|Indica se a coluna é uma pseudocoluna. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sempre retorna 1:<br /><br /> 0 = SQL_PC_UNKNOWN<br /><br /> 1 = SQL_PC_NOT_PSEUDO<br /><br /> 2 = SQL_PC_PSEUDO|  
  
## <a name="remarks"></a>Remarks  
 sp_special_columns é equivalente a SQLSpecialColumns no ODBC. Os resultados retornados são ordenados por SCOPE.  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão SELECT no esquema.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna informações sobre a coluna que identifica linhas de forma exclusiva na tabela `HumanResources.Department`.  
  
```sql  
USE AdventureWorks2012;  
GO  
EXEC sp_special_columns @table_name = 'Department'   
    ,@table_owner = 'HumanResources';  
```  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados do catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/catalog-stored-procedures-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
