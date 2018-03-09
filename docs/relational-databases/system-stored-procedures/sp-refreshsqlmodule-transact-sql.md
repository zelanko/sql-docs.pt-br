---
title: sp_refreshsqlmodule (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_refreshsqlmodule_TSQL
- sp_refreshsqlmodule
dev_langs: TSQL
helpviewer_keywords:
- metadata [SQL Server], stored procedures
- metadata [SQL Server], triggers
- metadata [SQL Server], views
- triggers [SQL Server], refreshing metadata
- views [SQL Server], refreshing metadata
- sp_refreshsqlmodule
- metadata [SQL Server], functions
- stored procedures [SQL Server], refreshing metadata
- user-defined functions [SQL Server], refreshing metadata
ms.assetid: f0022a05-50dd-4620-961d-361b1681d375
caps.latest.revision: "21"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: a95c2e905efa377edb83fd82a104758853b18271
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2017
---
# <a name="sprefreshsqlmodule-transact-sql"></a>sp_refreshsqlmodule (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Atualiza os metadados do procedimento armazenado não associado a esquema, da função definida pelo usuário, da exibição, do gatilho DML, do gatilho DDL de nível de banco de dados ou do gatilho DDL de nível de servidor especificado no banco de dados atual. Metadados persistentes desses objetos, como tipos de dados de parâmetros, podem ficar desatualizados devido a atualizações em seus objetos subjacentes.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sys.sp_refreshsqlmodule [ @name = ] 'module_name'   
    [ , [ @namespace = ] ' <class> ' ]  
  
<class> ::=  
{  
  | DATABASE_DDL_TRIGGER  
  | SERVER_DDL_TRIGGER  
}  
  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@name=** ] **'***nome_de_módulo***'**  
 É o nome do procedimento armazenado, função definida pelo usuário, exibição, gatilho DML, gatilho DDL de nível do banco de dados ou gatilho DDL do nível de servidor. *nome_de_módulo* não pode ser um tempo de execução de linguagem comum (CLR) procedimento armazenado ou uma função CLR. *nome_de_módulo* não pode ser associada a esquema. *nome_de_módulo* é **nvarchar**, sem padrão. *nome_de_módulo* pode ser um identificador de várias partes, mas só pode fazer referência a objetos no banco de dados atual.  
  
 [ **,** @**namespace** =] **'** \<classe > **'**  
 É a classe do módulo especificado. Quando *nome_de_módulo* é um gatilho DDL, \<classe > é necessária. *\<classe >* é **nvarchar**(20). As entradas válidas são:  
  
|||  
|-|-|  
|DATABASE_DDL_TRIGGER||  
|SERVER_DDL_TRIGGER|**Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou um número diferente de zero (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_refreshsqlmodule** devem ser executados quando alterações são feitas nos objetos subjacentes ao módulo que afeta sua definição. Caso contrário, o módulo pode produzir resultados inesperados quando consultado ou invocado. Para atualizar uma exibição, você pode usar **sp_refreshsqlmodule** ou **sp_refreshview** com os mesmos resultados.  
  
 **sp_refreshsqlmodule** não afeta qualquer permissões, propriedades estendidas ou definir opções que estão associadas ao objeto.  
  
 Para atualizar um gatilho DDL de nível de servidor, execute este procedimento armazenado a partir do contexto de qualquer banco de dados.  
  
> [!NOTE]  
>  Assinaturas que estão associadas ao objeto são removidas quando você executar **sp_refreshsqlmodule**.  
  
## <a name="permissions"></a>Permissões  
 Requer permissão ALTER no módulo e permissão REFERENCES em qualquer tipo CLR definido pelo usuário e coleções de esquemas XML referidas pelo objeto. Requer permissão ALTER ANY DATABASE DDL TRIGGER no banco de dados atual se o módulo especificado for um gatilho DDL de nível de banco de dados. Requer permissão CONTROL SERVER se o módulo especificado for um gatilho DDL de nível de servidor.  
  
 Além disso, em módulos definidos com a cláusula EXECUTE AS, requer permissão IMPERSONATE no principal especificado. Geralmente, atualizar um objeto não altera seu principal EXECUTE AS, a menos que o módulo tenha sido definido com EXECUTE AS USER e o nome de usuário do principal resolve, agora, um usuário diferente do que na ocasião em que o módulo foi criado.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-refreshing-a-user-defined-function"></a>A. Atualizando uma função definida pelo usuário  
 O exemplo a seguir atualiza uma função definida pelo usuário. O exemplo cria um tipo de dados de alias, `mytype`, e uma função definida pelo usuário, `to_upper`, que usa `mytype`. Em seguida, `mytype` é renomeado para `myoldtype` e um novo `mytype` é criado, com uma definição diferente. A função `dbo.to_upper` é atualizada de modo a fazer referência à nova implementação de `mytype`, em lugar da antiga.  
  
```  
-- Create an alias type.  
USE AdventureWorks2012;  
GO  
IF EXISTS (SELECT 'mytype' FROM sys.types WHERE name = 'mytype')  
DROP TYPE mytype;  
GO  
  
CREATE TYPE mytype FROM nvarchar(5);  
GO  
  
IF OBJECT_ID ('dbo.to_upper', 'FN') IS NOT NULL  
DROP FUNCTION dbo.to_upper;  
GO  
  
CREATE FUNCTION dbo.to_upper (@a mytype)  
RETURNS mytype  
WITH ENCRYPTION  
AS  
BEGIN  
RETURN upper(@a)  
END;  
GO  
  
SELECT dbo.to_upper('abcde');  
GO  
  
-- Increase the length of the alias type.  
sp_rename 'mytype', 'myoldtype', 'userdatatype';  
GO  
  
CREATE TYPE mytype FROM nvarchar(10);  
GO  
  
-- The function parameter still uses the old type.  
SELECT name, type_name(user_type_id)   
FROM sys.parameters   
WHERE object_id = OBJECT_ID('dbo.to_upper');  
GO  
  
SELECT dbo.to_upper('abcdefgh'); -- Fails because of truncation  
GO  
  
-- Refresh the function to bind to the renamed type.  
EXEC sys.sp_refreshsqlmodule 'dbo.to_upper';  
  
-- The function parameters are now bound to the correct type and the statement works correctly.  
SELECT name, type_name(user_type_id) FROM sys.parameters  
WHERE object_id = OBJECT_ID('dbo.to_upper');  
GO  
  
SELECT dbo.to_upper('abcdefgh');  
GO  
```  
  
### <a name="b-refreshing-a-database-level-ddl-trigger"></a>B. Atualizando um gatilho DDL de nível de banco de dados  
 O exemplo a seguir atualiza um gatilho DDL de nível de banco de dados.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sys.sp_refreshsqlmodule @name = 'ddlDatabaseTriggerLog' , @namespace = 'DATABASE_DDL_TRIGGER';  
GO  
```  
  
### <a name="c-refreshing-a-server-level-ddl-trigger"></a>C. Atualizando um gatilho DDL de nível de servidor  
 O exemplo a seguir atualiza um gatilho DLL de nível de servidor.  
  
||  
|-|  
|**Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
  
```  
USE master;  
GO  
EXEC sys.sp_refreshsqlmodule @name = 'ddl_trig_database' , @namespace = 'SERVER_DDL_TRIGGER';  
GO  
  
```  
  
## <a name="see-also"></a>Consulte também  
 [sp_refreshview &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-refreshview-transact-sql.md)   
 [Mecanismo de banco de dados armazenados procedimentos &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)  
  
  
