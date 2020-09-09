---
description: sp_unbindrule (Transact-SQL)
title: sp_unbindrule (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_unbindrule_TSQL
- sp_unbindrule
dev_langs:
- TSQL
helpviewer_keywords:
- sp_unbindrule
ms.assetid: f54ee155-c3c9-4f1a-952e-632a8339f0cc
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 7ddf241acfb6e82e0cdd67315727017fb9965f77
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89547312"
---
# <a name="sp_unbindrule-transact-sql"></a>sp_unbindrule (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Desvincula uma regra de uma coluna ou de um tipo de dados de alias no banco de dados atual.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepNextDontUse](../../includes/ssnotedepnextdontuse-md.md)] Recomendamos que você crie definições padrão usando a palavra-chave DEFAULT nas instruções [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md) ou [CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md) em vez disso.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_unbindrule [ @objname = ] 'object_name'   
     [ , [ @futureonly = ] 'futureonly_flag' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @objname = ] 'object_name'` É o nome da tabela e da coluna ou do tipo de dados do alias do qual a regra está desassociada. *object_name* é **nvarchar (776)**, sem padrão. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tenta resolver identificadores de duas partes primeiro para nomes das colunas e, em seguida, para tipos de dados do alias. Ao desvincular uma regra de um tipo de dados de alias, as colunas do tipo de dados que tiverem a mesma regra também serão desvinculadas. As colunas desse tipo de dados com regras vinculadas diretamente não serão afetadas.  
  
> [!NOTE]  
>  *object_name* pode conter colchetes **[]** como caracteres de identificador delimitados. Para obter mais informações, consulte [Database Identifiers](../../relational-databases/databases/database-identifiers.md).  
  
`[ @futureonly = ] 'futureonly_flag'` É usado somente ao desassociar uma regra de um tipo de dados de alias. *futureonly_flag* é **varchar (15)**, com um padrão de NULL. Quando *futureonly_flag* é **futureonly**, as colunas existentes desse tipo de dados não perdem a regra especificada.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="remarks"></a>Comentários  
 Para exibir o texto de uma regra, execute **sp_helptext** com o nome da regra como o parâmetro.  
  
 Quando uma regra é desassociada, as informações sobre a associação são removidas da tabela **Sys. Columns** se a regra foi associada a uma coluna e da tabela **Sys. Types** se a regra foi associada a um tipo de dados de alias.  
  
 Quando uma regra é desvinculada de um tipo de dados de alias, ela também é desvinculada das colunas com esse tipo de dados de alias. A regra também pode ainda estar associada a colunas cujos tipos de dados foram alterados mais tarde pela cláusula ALTER COLUMN de uma instrução ALTER TABLE, você deve desassociar especificamente a regra dessas colunas usando **sp_unbindrule** e especificando o nome da coluna.  
  
## <a name="permissions"></a>Permissões  
 Para desvincular uma regra de uma coluna de tabela, é necessário ter a permissão ALTER na tabela. Para desvincular uma regra de um tipo de dados de alias, é necessário ter a permissão CONTROL no tipo ou a permissão ALTER no esquema ao qual o tipo pertence.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-unbinding-a-rule-from-a-column"></a>a. Desvinculando uma regra de uma coluna  
 O exemplo a seguir desvincula a regra da coluna `startdate` de uma tabela `employees`.  
  
```  
EXEC sp_unbindrule 'employees.startdate';  
```  
  
### <a name="b-unbinding-a-rule-from-an-alias-data-type"></a>B. Desvinculando uma regra de um tipo de dados de alias  
 O exemplo a seguir desvincula a regra do tipo de dados de alias `ssn`. Ele desvincula a regra de colunas desse tipo, existentes e futuras.  
  
```  
EXEC sp_unbindrule ssn;  
```  
  
### <a name="c-using-futureonly_flag"></a>C. Usando futureonly_flag  
 O exemplo a seguir desvincula a regra do tipo de dados de alias `ssn` sem afetar as colunas `ssn` existentes.  
  
```  
EXEC sp_unbindrule 'ssn', 'futureonly';  
```  
  
### <a name="d-using-delimited-identifiers"></a>D. Usando identificadores delimitados  
 O exemplo a seguir mostra o uso de identificadores delimitados no parâmetro *object_name* .  
  
```  
CREATE TABLE [t.4] (c1 int); -- Notice the period as part of the table   
-- name.  
GO  
CREATE RULE rule2 AS @value > 100;  
GO  
EXEC sp_bindrule rule2, '[t.4].c1' -- The object contains two   
-- periods; the first is part of the table name and the second   
-- distinguishes the table name from the column name.  
GO  
EXEC sp_unbindrule '[t.4].c1';  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Mecanismo de Banco de Dados procedimentos armazenados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [CREATE RULE &#40;Transact-SQL&#41;](../../t-sql/statements/create-rule-transact-sql.md)   
 [DROP RULE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-rule-transact-sql.md)   
 [sp_bindrule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-bindrule-transact-sql.md)   
 [sp_helptext &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helptext-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
