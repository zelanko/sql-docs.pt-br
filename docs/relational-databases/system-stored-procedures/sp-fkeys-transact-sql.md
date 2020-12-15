---
description: sp_fkeys (Transact-SQL)
title: sp_fkeys (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/08/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_fkeys
- sp_fkeys_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_fkeys
ms.assetid: 18110444-d38d-4cff-90d2-d1fc6236668b
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ec31170ac813f9a1901e5fe5dd6f58a66ea47475
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97439451"
---
# <a name="sp_fkeys-transact-sql"></a>sp_fkeys (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Retorna informações lógicas de chave estrangeira para o ambiente atual. Este procedimento mostra relações de chave estrangeira que incluem chaves estrangeiras desabilitadas.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql  
sp_fkeys [ @pktable_name = ] 'pktable_name'   
     [ , [ @pktable_owner = ] 'pktable_owner' ]   
     [ , [ @pktable_qualifier = ] 'pktable_qualifier' ]   
     { , [ @fktable_name = ] 'fktable_name' }   
     [ , [ @fktable_owner = ] 'fktable_owner' ]   
     [ , [ @fktable_qualifier = ] 'fktable_qualifier' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @pktable_name =] '*pktable_name*'  
 É o nome da tabela, com a chave primária, usada para retornar informações de catálogo. *pktable_name* é **sysname**, com um padrão de NULL. Não há suporte para a correspondência de padrão curinga. Esse parâmetro ou o parâmetro *fktable_name* , ou ambos, devem ser fornecidos.  
  
 [ @pktable_owner =] '*pktable_owner*'  
 É o nome do proprietário da tabela (com a chave primária) usada para retornar as informações do catálogo. *pktable_owner* é **sysname**, com um padrão de NULL. Não há suporte para a correspondência de padrão curinga. Se *pktable_owner* não for especificado, as regras de visibilidade de tabela padrão do DBMS subjacente se aplicarão.  
  
 No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], se o usuário atual possuir uma tabela com o nome especificado, as colunas dessa tabela serão retornadas. Se *pktable_owner* não for especificado e o usuário atual não possuir uma tabela com o *pktable_name* especificado, o procedimento procurará uma tabela com a *pktable_name* especificada de Propriedade do proprietário do banco de dados. Se ela existir, as colunas dessa tabela serão retornadas.  
  
 [ @pktable_qualifier =] '*pktable_qualifier*'  
 É o nome do qualificador da tabela (com a chave primária). *pktable_qualifier* é sysname, com um padrão de NULL. Vários produtos DBMS dão suporte à nomenclatura de três partes para tabelas (*Qualifier.Owner.Name*). No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o qualificador representa o nome do banco de dados. Em alguns produtos, ele representa o nome do servidor do ambiente de banco de dados da tabela.  
  
 [ @fktable_name =] '*fktable_name*'  
 É o nome da tabela (com uma chave estrangeira) usada para retornar informações de catálogo. *fktable_name* é sysname, com um padrão de NULL. Não há suporte para a correspondência de padrão curinga. Esse parâmetro ou o parâmetro *pktable_name* , ou ambos, devem ser fornecidos.  
  
 [ @fktable_owner =] '*fktable_owner*'  
 É o nome do proprietário da tabela (com uma chave estrangeira) usada para retornar informações de catálogo. *fktable_owner* é **sysname**, com um padrão de NULL. Não há suporte para a correspondência de padrão curinga. Se *fktable_owner* não for especificado, as regras de visibilidade de tabela padrão do DBMS subjacente se aplicarão.  
  
 No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], se o usuário atual possuir uma tabela com o nome especificado, as colunas dessa tabela serão retornadas. Se *fktable_owner* não for especificado e o usuário atual não possuir uma tabela com o *fktable_name* especificado, o procedimento procurará uma tabela com a *fktable_name* especificada de Propriedade do proprietário do banco de dados. Se ela existir, as colunas dessa tabela serão retornadas.  
  
 [ @fktable_qualifier =] '*FKTABLE_QUALIFIER*'  
 É o nome do qualificador da tabela (com uma chave estrangeira). *FKTABLE_QUALIFIER* é **sysname**, com um padrão de NULL. No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o qualificador representa o nome do banco de dados. Em alguns produtos, ele representa o nome do servidor do ambiente de banco de dados da tabela.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 Nenhum  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|PKTABLE_QUALIFIER|**sysname**|Nome do qualificador da tabela (com a chave primária). Esse campo pode ser NULL.|  
|PKTABLE_OWNER|**sysname**|Nome do proprietário da tabela (com a chave primária). Esse campo sempre retorna um valor.|  
|PKTABLE_NAME|**sysname**|Nome da tabela (com a chave primária). Esse campo sempre retorna um valor.|  
|PKCOLUMN_NAME|**sysname**|Nome das colunas de chave primária, para cada coluna do TABLE_NAME retornado. Esse campo sempre retorna um valor.|  
|FKTABLE_QUALIFIER|**sysname**|Nome do qualificador da tabela (com uma chave estrangeira). Esse campo pode ser NULL.|  
|FKTABLE_OWNER|**sysname**|Nome do proprietário da tabela (com uma chave estrangeira). Esse campo sempre retorna um valor.|  
|FKTABLE_NAME|**sysname**|Nome da tabela (com a chave estrangeira). Esse campo sempre retorna um valor.|  
|FKCOLUMN_NAME|**sysname**|Nome da coluna de chave estrangeira, para cada coluna do TABLE_NAME retornado. Esse campo sempre retorna um valor.|  
|KEY_SEQ|**smallint**|Número de sequência da coluna em uma chave primária de várias colunas. Esse campo sempre retorna um valor.|  
|UPDATE_RULE|**smallint**|Ação aplicada à chave estrangeira quando a operação SQL é uma atualização.  Valores possíveis:<br /> 0=CASCADE altera para chave estrangeira.<br /> 1=NO ACTION altera se a chave estrangeira estiver presente.<br />   2 = definir nulo <br /> 3 = definir padrão |  
|DELETE_RULE|**smallint**|Ação aplicada à chave estrangeira quando a operação SQL é uma exclusão. Valores possíveis:<br /> 0=CASCADE altera para chave estrangeira.<br /> 1=NO ACTION altera se a chave estrangeira estiver presente.<br />   2 = definir nulo <br /> 3 = definir padrão |  
|FK_NAME|**sysname**|Identificador de chave estrangeira. Será NULL se não for aplicável à fonte de dados. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retorna o nome da restrição de FOREIGN KEY.|  
|PK_NAME|**sysname**|Identificador da chave primária. Será NULL se não for aplicável à fonte de dados. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retorna o nome da restrição de PRIMARY KEY.|  
  
 Os resultados retornados são ordenados por FKTABLE_QUALIFIER, FKTABLE_OWNER, FKTABLE_NAME e KEY_SEQ.  
  
## <a name="remarks"></a>Comentários  
 A codificação de aplicativo incluindo tabelas com chaves estrangeiras desabilitadas pode ser implementada pelo seguinte:  
  
-   Desabilitando temporariamente a verificação de restrições (ALTER TABLE NOCHECK ou CREATE TABLE NOT FOR REPLICATION) ao trabalhar com tabelas e habilitando-a novamente mais tarde.  
  
-   Usando gatilhos ou código de aplicativo para impor relações.  
  
Se o nome da tabela de chave primária for fornecido e se o nome da tabela de chave estrangeira for NULL, sp_fkeys retornará todas as tabelas que incluam uma chave estrangeira para a tabela especificada. Se o nome da tabela de chave estrangeira for fornecido e se o nome da tabela de chave primária for NULL, sp_fkeys retornará todas as tabelas associadas por uma relação de chave primária/chave estrangeira com chaves estrangeiras na tabela de chave estrangeira.  
  
O procedimento armazenado de sp_fkeys é equivalente a SQLForeignKeys em ODBC.  
  
## <a name="permissions"></a>Permissões  
 Requer `SELECT` a permissão no esquema.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir recupera uma lista de chaves estrangeiras para a tabela `HumanResources.Department` no banco de dados `AdventureWorks2012`.  
  
```sql  
USE AdventureWorks2012;  
GO  
EXEC sp_fkeys @pktable_name = N'Department'  
    ,@pktable_owner = N'HumanResources';  
```  
  
## <a name="examples-sssdwfull-and-sspdw"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 O exemplo a seguir recupera uma lista de chaves estrangeiras para a tabela `DimDate` no banco de dados `AdventureWorksPDW2012`. Nenhuma linha é retornada porque [!INCLUDE[ssDW](../../includes/ssdw-md.md)] o não oferece suporte a chaves estrangeiras.  
  
```sql  
EXEC sp_fkeys @pktable_name = N'DimDate';  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Procedimentos armazenados de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/catalog-stored-procedures-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_pkeys ](../../relational-databases/system-stored-procedures/sp-pkeys-transact-sql.md)  
  
  

