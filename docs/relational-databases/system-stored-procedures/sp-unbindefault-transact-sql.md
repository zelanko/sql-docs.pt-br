---
description: sp_unbindefault (Transact-SQL)
title: sp_unbindefault (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_unbindefault_TSQL
- sp_unbindefault
dev_langs:
- TSQL
helpviewer_keywords:
- sp_unbindefault
ms.assetid: c96a6c5e-f3ca-4c1e-b64b-0d8ef6986af8
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 2a78e7ac859e4750f543befd2e574214dae35386
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88492957"
---
# <a name="sp_unbindefault-transact-sql"></a>sp_unbindefault (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Desvincula, ou remove, um padrão de uma coluna ou de um tipo de dados de alias no banco de dados atual.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepNextDontUse](../../includes/ssnotedepnextdontuse-md.md)] Recomendamos que você crie definições padrão usando a palavra-chave DEFAULT nas instruções [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md) ou [CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md) em vez disso.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_unbindefault [ @objname = ] 'object_name'   
     [ , [ @futureonly = ] 'futureonly_flag' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @objname = ] 'object_name'` É o nome da tabela e da coluna ou do tipo de dados do alias do qual o padrão deve ser desassociado. *object_name* é **nvarchar (776)**, sem padrão. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tenta resolver identificadores de duas partes primeiro para nomes das colunas e, em seguida, para tipos de dados do alias.  
  
 Ao desvincular um padrão de um tipo de dados de alias, as colunas desse tipo de dados que tiverem o mesmo padrão também serão desvinculadas. As colunas desse tipo de dados com padrões vinculados diretamente não serão afetadas.  
  
> [!NOTE]  
>  *object_name* pode conter colchetes **[]** como caracteres de identificador delimitados. Para obter mais informações, consulte [Database Identifiers](../../relational-databases/databases/database-identifiers.md).  
  
`[ @futureonly = ] 'futureonly_flag'` É usado somente ao desassociar um padrão de um tipo de dados de alias. *futureonly_flag* é **varchar (15)**, com um padrão de NULL. Quando *futureonly_flag* é **futureonly**, as colunas existentes do tipo de dados não perdem o padrão especificado.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="remarks"></a>Comentários  
 Para exibir o texto de um padrão, execute **sp_helptext** com o nome do padrão como o parâmetro.  
  
## <a name="permissions"></a>Permissões  
 Para desvincular um padrão de uma coluna de tabela é necessário ter a permissão ALTER na tabela. Para desvincular um padrão de um tipo de dados de alias, é necessário ter a permissão CONTROL no tipo ou a permissão ALTER no esquema ao qual o tipo pertence.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-unbinding-a-default-from-a-column"></a>a. Desvinculando um padrão de uma coluna  
 O exemplo a seguir desvincula o padrão da coluna `hiredate` de uma tabela `employees`.  
  
```  
EXEC sp_unbindefault 'employees.hiredate';  
```  
  
### <a name="b-unbinding-a-default-from-an-alias-data-type"></a>B. Desvinculando um padrão de um tipo de dados de alias  
 O exemplo a seguir desvincula o padrão do tipo de dados de alias `ssn`. Ele desvincula as colunas existentes e futuras desse tipo.  
  
```  
EXEC sp_unbindefault 'ssn';  
```  
  
### <a name="c-using-the-futureonly_flag"></a>C. Usando o futureonly_flag  
 O exemplo a seguir desvincula usos futuros do tipo de dados de alias `ssn` sem afetar as colunas `ssn` existentes.  
  
```  
EXEC sp_unbindefault 'ssn', 'futureonly';  
```  
  
### <a name="d-using-delimited-identifiers"></a>D. Usando identificadores delimitados  
 O exemplo a seguir mostra o uso de identificadores delimitados no parâmetro *object_name* .  
  
```  
CREATE TABLE [t.3] (c1 int); -- Notice the period as part of the table   
-- name.  
CREATE DEFAULT default2 AS 0;  
GO  
EXEC sp_bindefault 'default2', '[t.3].c1' ;  
-- The object contains two periods;  
-- the first is part of the table name and the second   
-- distinguishes the table name from the column name.  
EXEC sp_unbindefault '[t.3].c1';  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Procedimentos armazenados do sistema &#40;&#41;Transact-SQL ](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Mecanismo de Banco de Dados procedimentos armazenados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [CREATE DEFAULT &#40;Transact-SQL&#41;](../../t-sql/statements/create-default-transact-sql.md)   
 [Descartar padrão &#40;Transact-SQL&#41;](../../t-sql/statements/drop-default-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_bindefault ](../../relational-databases/system-stored-procedures/sp-bindefault-transact-sql.md)   
 [sp_helptext &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helptext-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
