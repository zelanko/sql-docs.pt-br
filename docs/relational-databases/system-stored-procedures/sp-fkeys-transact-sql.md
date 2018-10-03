---
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
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a30016240c6cfd34cd2e21d6987ea04a0bc27537
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47705964"
---
# <a name="spfkeys-transact-sql"></a>sp_fkeys (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Retorna informações lógicas de chave estrangeira para o ambiente atual. Este procedimento mostra relações de chave estrangeira que incluem chaves estrangeiras desabilitadas.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
sp_fkeys [ @pktable_name = ] 'pktable_name'   
     [ , [ @pktable_owner = ] 'pktable_owner' ]   
     [ , [ @pktable_qualifier = ] 'pktable_qualifier' ]   
     { , [ @fktable_name = ] 'fktable_name' }   
     [ , [ @fktable_owner = ] 'fktable_owner' ]   
     [ , [ @fktable_qualifier = ] 'fktable_qualifier' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @pktable_name=] '*pktable_name*'  
 É o nome da tabela, com a chave primária, usada para retornar informações de catálogo. *pktable_name* está **sysname**, com um padrão NULL. Não há suporte para a correspondência de padrão curinga. Esse parâmetro ou o *fktable_name* parâmetro, ou ambos, devem ser fornecidos.  
  
 [ @pktable_owner=] '*pktable_owner*'  
 É o nome do proprietário da tabela (com a chave primária) usada para retornar informações de catálogo. *pktable_owner* está **sysname**, com um padrão NULL. Não há suporte para a correspondência de padrão curinga. Se *pktable_owner* não for especificado, serão aplicadas as regras de visibilidade de tabela padrão do DBMS subjacente.  
  
 No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], se o usuário atual possuir uma tabela com o nome especificado, as colunas dessa tabela serão retornadas. Se *pktable_owner* não for especificado e o usuário atual não possuir uma tabela com especificado *pktable_name*, o procedimento procurará uma tabela com especificado *pktable_name* pertencente ao proprietário do banco de dados. Se ela existir, as colunas dessa tabela serão retornadas.  
  
 [ @pktable_qualifier =] '*pktable_qualifier*'  
 É o nome do qualificador da tabela (com a chave primária). *pktable_qualifier* é sysname, com um padrão NULL. Vários produtos DBMS dão suporte à nomenclatura de três partes para tabelas (*qualificador*). No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o qualificador representa o nome do banco de dados. Em alguns produtos, ele representa o nome do servidor do ambiente de banco de dados da tabela.  
  
 [ @fktable_name=] '*fktable_name*'  
 É o nome da tabela (com uma chave estrangeira) usada para retornar informações de catálogo. *fktable_name* é sysname, com um padrão NULL. Não há suporte para a correspondência de padrão curinga. Esse parâmetro ou o *pktable_name* parâmetro, ou ambos, devem ser fornecidos.  
  
 [ @fktable_owner =] '*fktable_owner*'  
 É o nome do proprietário da tabela (com uma chave estrangeira) usada para retornar informações de catálogo. *fktable_owner* está **sysname**, com um padrão NULL. Não há suporte para a correspondência de padrão curinga. Se *fktable_owner* não for especificado, serão aplicadas as regras de visibilidade de tabela padrão do DBMS subjacente.  
  
 No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], se o usuário atual possuir uma tabela com o nome especificado, as colunas dessa tabela serão retornadas. Se *fktable_owner* não for especificado e o usuário atual não possuir uma tabela com especificado *fktable_name*, o procedimento procurará uma tabela com especificado *fktable_name* pertencente ao proprietário do banco de dados. Se ela existir, as colunas dessa tabela serão retornadas.  
  
 [ @fktable_qualifier=] '*fktable_qualifier*'  
 É o nome do qualificador da tabela (com uma chave estrangeira). *fktable_qualifier* está **sysname**, com um padrão NULL. No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o qualificador representa o nome do banco de dados. Em alguns produtos, ele representa o nome do servidor do ambiente de banco de dados da tabela.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 None  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Description|  
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
|UPDATE_RULE|**smallint**|Ação aplicada à chave estrangeira quando a operação SQL é uma atualização.  Valores possíveis:<br /> 0=CASCADE altera para chave estrangeira.<br /> 1=NO ACTION altera se a chave estrangeira estiver presente.<br />   2 = definido como nulo <br /> 3 = Definir como padrão |  
|DELETE_RULE|**smallint**|Ação aplicada à chave estrangeira quando a operação SQL é uma exclusão. Valores possíveis:<br /> 0=CASCADE altera para chave estrangeira.<br /> 1=NO ACTION altera se a chave estrangeira estiver presente.<br />   2 = definido como nulo <br /> 3 = Definir como padrão |  
|FK_NAME|**sysname**|Identificador de chave estrangeira. Será NULL se não for aplicável à fonte de dados. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retorna o nome da restrição de FOREIGN KEY.|  
|PK_NAME|**sysname**|Identificador da chave primária. Será NULL se não for aplicável à fonte de dados. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retorna o nome da restrição de PRIMARY KEY.|  
  
 Os resultados retornados são ordenados por FKTABLE_QUALIFIER, FKTABLE_OWNER, FKTABLE_NAME e KEY_SEQ.  
  
## <a name="remarks"></a>Comentários  
 A codificação de aplicativo incluindo tabelas com chaves estrangeiras desabilitadas pode ser implementada pelo seguinte:  
  
-   Desabilitando temporariamente a verificação de restrições (ALTER TABLE NOCHECK ou CREATE TABLE NOT FOR REPLICATION) ao trabalhar com tabelas e habilitando-a novamente mais tarde.  
  
-   Usando gatilhos ou código de aplicativo para impor relações.  
  
Se o nome da tabela de chave primária for fornecido e se o nome da tabela de chave estrangeira for NULL, sp_fkeys retornará todas as tabelas que incluam uma chave estrangeira para a tabela especificada. Se o nome da tabela de chave estrangeira for fornecido e se o nome da tabela de chave primária for NULL, sp_fkeys retornará todas as tabelas associadas por uma relação de chave primária/chave estrangeira com chaves estrangeiras na tabela de chave estrangeira.  
  
O procedimento armazenado de sp_fkeys é equivalente a SQLForeignKeys no ODBC.  
  
## <a name="permissions"></a>Permissões  
 Requer `SELECT` permissão no esquema.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir recupera uma lista de chaves estrangeiras para a tabela `HumanResources.Department` no banco de dados `AdventureWorks2012`.  
  
```sql  
USE AdventureWorks2012;  
GO  
EXEC sp_fkeys @pktable_name = N'Department'  
    ,@pktable_owner = N'HumanResources';  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 O exemplo a seguir recupera uma lista de chaves estrangeiras para a tabela `DimDate` no banco de dados `AdventureWorksPDW2012`. Nenhuma linha é retornada porque [!INCLUDE[ssDW](../../includes/ssdw-md.md)] não oferece suporte a chaves estrangeiras.  
  
```sql  
EXEC sp_fkeys @pktable_name = N'DimDate;  
```  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados do catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/catalog-stored-procedures-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sp_pkeys &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-pkeys-transact-sql.md)  
  
  

