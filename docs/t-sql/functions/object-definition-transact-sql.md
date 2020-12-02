---
description: OBJECT_DEFINITION (Transact-SQL)
title: OBJECT_DEFINITION (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- OBJECT_DEFINITION_TSQL
- OBJECT_DEFINITION
dev_langs:
- TSQL
helpviewer_keywords:
- viewing source text
- source text [SQL Server]
- displaying source text
- OBJECT_DEFINITION function
ms.assetid: 2ac837c7-eca9-4d29-b06e-72e30450c68d
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 239a48b378e186e6149a31012785835939d2cde7
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2020
ms.locfileid: "91115949"
---
# <a name="object_definition-transact-sql"></a>OBJECT_DEFINITION (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Retorna o texto de origem de [!INCLUDE[tsql](../../includes/tsql-md.md)] da definição de um objeto especificado.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
OBJECT_DEFINITION ( object_id )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
 *object_id*  
 É a ID do objeto a ser usado. *object_id* é **int** e considera-se que representa um objeto no contexto de banco de dados atual.  
  
## <a name="return-types"></a>Tipos de retorno  
 **nvarchar(max)**  
  
## <a name="exceptions"></a>Exceções  
 Retornará NULL em caso de erro ou se um chamador não tiver permissão para exibir o objeto.  
  
 Um usuário só pode exibir metadados de protegíveis de sua propriedade ou para os quais recebeu permissão. Isso significa que as funções internas emissoras de metadados, como OBJECT_DEFINITION, podem retornar NULL se o usuário não tiver permissão no objeto. Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="remarks"></a>Comentários  
 O [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] supõe que *object_id* esteja no contexto do banco de dados atual. A ordenação da definição de objeto sempre corresponde ao do contexto de banco de dados que está fazendo a chamada.  
  
 OBJECT_DEFINITION se aplica aos tipos de objeto seguintes:  
  
-   C = Verificar restrições  
  
-   D = Padrão (restrição ou autônomo)  
  
-   P = Procedimento armazenado SQL  
  
-   FN = Função escalar SQL  
  
-   R = Regra  
  
-   RF = Procedimento do filtro de replicação  
  
-   TR = Gatilho SQL (gatilho DML com escopo de esquema, ou gatilho DDL no banco de dados ou no escopo de servidor)  
  
-   IF = Função SQL com valor de tabela embutida  
  
-   TF = Função SQL com valor de tabela  
  
-   V = Exibição  
  
## <a name="permissions"></a>Permissões  
 Definições de objeto de sistema são publicamente visíveis. A definição de objetos de usuário é visível ao proprietário do objeto e às entidades autorizadas que têm uma das seguintes permissões: ALTER, CONTROL, TAKE OWNERSHIP ou VIEW DEFINITION. Estas permissões são mantidas implicitamente por membros das funções fixas de banco de dados **db_owner**, **db_ddladmin** e **db_securityadmin** .  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-returning-the-source-text-of-a-user-defined-object"></a>a. Retornando o texto de origem de um objeto definido pelo usuário  
 O exemplo a seguir retorna a definição de um gatilho definido pelo usuário, `uAddress`, no esquema `Person`. A função interna `OBJECT_ID` é usada para retornar a ID do objeto do gatilho à instrução `OBJECT_DEFINITION`.  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT OBJECT_DEFINITION (OBJECT_ID(N'Person.uAddress')) AS [Trigger Definition];   
GO  
```  
  
### <a name="b-returning-the-source-text-of-a-system-object"></a>B. Retornando o texto de origem de um objeto de sistema  
 O exemplo a seguir retorna a definição do procedimento armazenado do sistema `sys.sp_columns`.  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT OBJECT_DEFINITION (OBJECT_ID(N'sys.sp_columns')) AS [Object Definition];  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Funções de metadados &#40;Transact-SQL&#41;](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [OBJECT_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/object-name-transact-sql.md)   
 [OBJECT_ID &#40;Transact-SQL&#41;](../../t-sql/functions/object-id-transact-sql.md)   
 [sp_helptext &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helptext-transact-sql.md)   
 [sys.sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [sys.server_sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-sql-modules-transact-sql.md)  
  
  
